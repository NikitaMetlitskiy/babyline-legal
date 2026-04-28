# Babyline · Release Checklist

A practical to-do list for the first App Store submission. Items marked
**❗** require manual action — only you can do them. Items marked **🤖**
can be automated by the assistant on request.

---

## A. App Store Connect setup ❗

### A.1. Apple Developer & App ID
- [ ] Apple Developer Program membership active ($99/yr).
- [ ] App ID `com.babyline2.app` registered with capabilities:
      Push Notifications ✅, Sign in with Apple ✅, Associated Domains
      (only if you add Universal Links later).
- [ ] **Sign in with Apple** legal agreement accepted in Developer
      Account → Agreements (one-time).

### A.2. App in App Store Connect
- [ ] New app created with bundle id `com.babyline2.app`.
- [ ] **App information** → primary language Russian or English (pick
      one — you can add additional locales later).
- [ ] **Categories**: Primary "Health & Fitness", Secondary "Lifestyle"
      (or "Medical" — but Medical category triggers stricter review).
- [ ] **Age rating**: 4+ (no age gate needed).
- [ ] **Privacy Policy URL** — host `PRIVACY_POLICY.md` somewhere
      (see section D below).
- [ ] **Support URL** — host `SUPPORT.md` somewhere.
- [ ] **Marketing URL** — optional, can be a single landing page.

### A.3. App Privacy questionnaire
The Privacy nutrition label asks what data you collect. Answer:

- **Contact Info** → Email Address (linked to user, used for app
  functionality, not tracking).
- **User Content** → "Other User Content" (baby diary entries),
  "Photos or Videos" (only avatar, optional), linked to user, used for
  app functionality.
- **Identifiers** → User ID (Supabase user_id), linked to user, used
  for app functionality.
- **Health & Fitness** → "Health" (vaccinations, growth, etc.), linked
  to user, used for app functionality.
- **Diagnostics** → "Crash Data" (only if you wire a crash reporter
  later — currently NO).
- Tracking: **No** (we don't track across apps).

### A.4. In-App Purchases
StoreKit products you must create:
- [ ] **Lifetime** — Non-Consumable, product id
      `com.babyline2.app.plus.year`, price tier $39.99.
- [ ] **3 months** — Auto-Renewable Subscription, product id
      `com.babyline2.app.plus.quarterly`, $9.99/quarter.
- [ ] **Monthly** — Auto-Renewable Subscription, product id
      `com.babyline2.app.plus.monthly`, $4.99/month.
- [ ] Subscription group: e.g. "Babyline Plus".
- [ ] Localized display names + descriptions per product (RU + EN).
- [ ] Promotional offers (intro / free trial) — optional. The 7-day
      trial is currently driven by our own DB (`families.trial_ends_at`,
      no StoreKit involvement) — keep that, it's simpler.

> ⚠️ **Heads up:** the in-app paywall currently has no real StoreKit
> purchase wiring. The `Continue` button in `PaywallView` does nothing.
> See section C.1 below.

### A.5. Marketing assets
- [ ] App icon **1024×1024 PNG** (already in repo).
- [ ] Screenshots for **6.7"** (iPhone 15 Pro Max), **6.1"** (iPhone 15
      Pro), and **iPad 13"** (if you target iPad). Minimum 3, max 10
      per size.
- [ ] App preview video — optional but boosts conversion.
- [ ] App description + keywords + promotional text — RU and/or EN.
      Keep description ≤ 4000 chars; keywords are a single 100-char
      comma-separated string.
- [ ] What's new (release notes) for v2.1 build 24.

### A.6. Tax & Banking
- [ ] **Paid Applications agreement** signed in
      Agreements, Tax & Banking.
- [ ] Bank account + W-8 / W-9 tax form on file.

---

## B. Apple Push Notifications ❗

- [x] APNs Auth Key (P8) created with Sandbox & Production scope —
      `LZ8B6W4T8J`.
- [x] `APNS_KEY` stored in Supabase function secrets (not in repo).
- [x] `notify-push` edge function deployed and reading `APNS_KEY` from
      `Deno.env`.
- [x] DB trigger `notifications_apns_push` fires on `notifications`
      INSERT.
- [ ] Revoke the **two old** APNs keys you no longer use
      (`B4TRVCGYN7`, `V9LMCC3VMD`) on developer.apple.com → Keys.

---

## C. Code gaps to close before release ❗

### C.1. **CRITICAL — StoreKit purchase wiring is missing**
`PaywallView.swift` has the UI but the **Continue** button currently
just toggles `app.isPaid = true` locally. No real Apple purchase.
Without this, users can't pay, and Apple **will reject** the build for
guideline 2.1 (apps that show a paywall must use real StoreKit).

What's needed:
- StoreKit 2 `Product.products(for: ids)` to fetch live prices.
- `product.purchase()` flow with transaction verification.
- Call backend (or check entitlement locally) to mark `isPaid = true`
  and `families.is_paid = true`.
- Restore Purchases handler.
- Receipt validation server-side (Supabase edge function reading
  `App Store Server API`).

This is its own feature (~1–2 days of work). Tell me when to start.

### C.2. **In-app account deletion path**
Apple guideline 5.1.1(v) requires the user to delete their **account**
in-app, not just their data. Currently we have "Erase ALL data" which
keeps `auth.users` row + family. Need a real "Delete account" button
that calls a server-side function to delete `auth.users` + cascade.

Action: I can add this in 30 minutes.

### C.3. App Store URL placeholder
`Cloud.appStoreURL` still points to fake `id0000000000`. Must be
replaced with real numeric App Store ID once your app gets one (after
first submission Apple assigns it). You'll edit this in
`Babyline/Cloud/SupabaseClient.swift` and ship a hotfix.

### C.4. Cron-schedule `purge_archived_rows()`
The function exists but I never scheduled it. Without a cron, archived
rows pile up forever. Need a Supabase scheduled job:

```sql
select cron.schedule(
    'babyline-purge-archive', '0 4 * * *',  -- 04:00 UTC daily
    $$select public.purge_archived_rows()$$
);
```

🤖 Tell me — I'll apply it.

### C.5. Photo library permission text
We let users pick an avatar from photos. The app needs
`NSPhotoLibraryUsageDescription` (and possibly
`NSPhotoLibraryAddUsageDescription`) in Info.plist, otherwise iOS will
crash on first photo-pick. **Quick check needed.**

🤖 I'll verify and add if missing.

### C.6. Localized App Store metadata
App Store Connect lets you have separate metadata per locale (RU, EN).
Even though the app strings are localized, the App Store description
+ screenshots need separate per-locale uploads.

---

## D. Where to host privacy/support pages ❗

You need PUBLIC URLs to point Apple at. Options:

1. **GitHub Pages** (free): push the `legal/` folder to a public repo
   `babyline-legal`, enable Pages, Apple uses
   `https://<user>.github.io/babyline-legal/PRIVACY_POLICY.html`.
   You'd convert MD → HTML (one `pandoc` command).
2. **Supabase Storage** (you already pay for it): upload as public
   files, point at `https://<project>.supabase.co/storage/v1/object/public/...`.
3. **Custom domain** (e.g. `babyline.app/privacy`): cleanest, but you
   need to own a domain.

Cheapest fastest: GitHub Pages. I can scaffold it if you want.

---

## E. Things you might not have thought about

### E.1. Domain & email
You list `nikita.metlitskiy@gmail.com` everywhere. **Buy the domain** (e.g.
namecheap, cloudflare-registrar) and set up a forwarding email so the
support address actually delivers to your real mailbox. ~$10/year.

### E.2. Refund / chargeback policy
Apple processes refunds for in-app purchases. For the **Lifetime**
plan, expect occasional buyer-remorse refund requests; Apple usually
auto-approves within 14 days. You don't need to do anything but be
aware Apple can claw back the payment.

### E.3. GDPR / Russian "Roskomnadzor" data localization
- **GDPR (EU)**: with Supabase eu-west-1 you store data in the EU,
  which is fine for EU users. Privacy Policy already covers
  GDPR-required rights.
- **Russia (152-ФЗ)**: Russian law technically requires personal data
  of Russian citizens to be stored on servers physically in Russia.
  Supabase Ireland is **non-compliant**. Realistic enforcement on a
  small consumer app is low, but if you ever get a Russian
  data-protection notice, that's the issue. Mitigation if it ever
  comes up: deploy a Russia-region replica or restrict Russian users.

### E.4. App Tracking Transparency
You don't track across apps, so you don't need the ATT prompt. But
your App Privacy answer **must** declare "Tracking: No". Don't add
analytics SDKs (Firebase, Amplitude) without re-evaluating this.

### E.5. Children's category & COPPA
You collect personal data **about children** (your user's child) but
not **from children**. Apple's "Kids Category" is for apps where the
end user is a child. **Do not opt into Kids Category** — you'll get
extra restrictions for nothing. Just keep the 4+ age rating.

### E.6. Reviews / ratings prompt
Right now you don't prompt for App Store reviews. Consider adding
`SKStoreReviewController.requestReview()` after a positive milestone
(e.g. user logged 30+ entries). 🤖 Easy add.

### E.7. Crash reporting
You have no crash reporter. Highly recommend **Sentry** or
**Apple's own Xcode Organizer crashes** (free). Without one, you'll
ship bugs and not know about them. 🤖 I can wire Sentry.

### E.8. Backups
Supabase free tier keeps 7 days of automatic snapshots. If you need
more, upgrade to Pro ($25/mo) — it gives 14 days + point-in-time
recovery to any second.

### E.9. Realtime quotas
Free tier: 2 concurrent realtime connections per project, then
limited. As soon as you have ~50 active users you'll need Pro tier.
Watch the dashboard.

### E.10. Email deliverability
Supabase Auth uses its built-in email sender by default which has
poor deliverability and gets stuck in spam. **Strongly recommend**
hooking up a custom SMTP (Resend.com — 3000/mo free, or Postmark
$15/mo). Otherwise users will report "I never got the magic link".

### E.11. Customer-facing analytics
Optional: PostHog or Mixpanel to see funnel drop-off in onboarding,
paywall conversion, etc. **Privacy implications**: would change your
App Privacy answer to include analytics tracking. Defer until after
launch.

### E.12. Sign in with Apple email relay
When users sign in with Apple, they may pick "Hide my email" — Apple
gives you a relay address (`xxxx@privaterelay.appleid.com`). To send
real emails (e.g. password reset) to those users, you must register
your sending domain in Apple Developer → Sign in with Apple →
Configure → "Email Sources". Otherwise relay-protected users won't
receive Babyline emails.

### E.13. TestFlight beta first
Don't go straight to App Store. Push to TestFlight, invite 5-10
people, watch for 1 week. Crashes, copy bugs, sign-in failures, push
delivery — you'll find them.

### E.14. App Review notes
When submitting, in the App Review Information field, give Apple:
- A **demo account** they can sign in with (email + password).
- A note explaining "this app is a personal tracker, not a medical
  device. Disclaimer is shown to user during onboarding (Disclaimer
  step) and in Privacy Policy section 8."

This dramatically reduces review rejections.

---

## F. Today's quick wins (10 minutes each)

- [ ] Buy `babyline.app` domain + set up email forwarding for
      `nikita.metlitskiy@gmail.com`.
- [ ] Push `legal/` folder to a public GitHub repo + enable Pages.
- [ ] Take screenshots of 6 main screens on simulator (Home, Diary,
      Food, Health, Settings, Paywall) at iPhone 15 Pro Max size.
- [ ] Write 4-sentence app description in EN + RU.
- [ ] Reply to me with whether to start StoreKit wiring (the big one
      that will block submission).

📧 When you're ready to ship — ping me with what you tackled and what
you want me to do next.
