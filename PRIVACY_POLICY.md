# Privacy Policy / Политика конфиденциальности

**Babyline** · _The first year. Together._
Last updated / Последнее обновление: 2026-04-28

> ⚠️ **Important — Read First / Важно — Прочитайте первым**
>
> Babyline is a **personal tracker** for parents. It is **NOT a medical
> device, medical software, or source of medical advice**. Any data,
> schedules, checklists, or suggestions shown in the app are general
> reference information from public sources and may be inaccurate,
> outdated, or inapplicable to your child. **Always consult a licensed
> pediatrician before making any decision about your child's health,
> nutrition, vaccinations, medications, sleep, or development.**
>
> Babyline — это **личный трекер** для родителей. Он **НЕ является
> медицинским устройством, медицинским программным обеспечением или
> источником медицинских рекомендаций**. Любые данные, графики, чек-листы
> и подсказки в приложении — общая справочная информация из открытых
> источников, которая может быть неточной, устаревшей или неприменимой
> к вашему ребёнку. **Всегда консультируйтесь с педиатром перед принятием
> любых решений о здоровье, питании, прививках, лекарствах, сне и
> развитии вашего ребёнка.**

---

## English version

### 1. Who we are

Babyline ("the App") is a private project. The data controller is the
individual operator of the App ("we", "us"). For privacy questions or
data deletion requests, contact: **nikita.metlitskiy@gmail.com**.

### 2. What we collect

When you create an account and use Babyline, we collect:

- **Account data:** email address, your chosen display name, optional
  avatar photo, role (mom / dad / other), authentication metadata.
- **Family data:** baby's name, gender, date of birth, optional initial
  height and weight, country (used to pick a vaccination schedule).
- **Activity data you log:** sleep, feedings, walks, food tries,
  vaccinations, growth measurements, tooth records, milestones,
  comments, calendar events, medications, checklist progress.
- **Family-sharing data:** your invite code redemptions, family member
  list, partner activity timestamps.
- **Device data:** APNs push token (so we can send you partner-activity
  notifications), device locale, app build, last-seen timestamp.
- **Diagnostic logs:** anonymous error traces (no personal content) when
  the app encounters a bug.

We **do not collect**: contacts, location, photos other than ones you
explicitly upload as an avatar, advertising identifiers, biometric
data, microphone, camera (other than avatar capture), call records,
SMS, calendar (other than events you create inside the App).

### 3. Where data is stored

All data is stored on **Supabase** (PostgreSQL + Storage), hosted in the
EU (eu-west-1, Ireland). Push notifications are delivered via **Apple
Push Notification service** (APNs). Authentication (Sign in with Apple,
email magic-link, password) is processed by **Supabase Auth**.

We do not sell or share your data with third parties for advertising or
analytics. The only third parties involved are infrastructure
providers acting as data processors:

- **Supabase Inc.** — database, auth, storage, push fan-out.
- **Apple Inc.** — APNs delivery and Sign in with Apple.

### 4. How long we keep data

- **Active data:** kept while your account exists.
- **Soft-deleted data (archive):** kept for **30 days**, then permanently
  removed by an automated job.
- **Backups:** Supabase keeps 7 days of point-in-time recovery snapshots.
- **Account deletion:** when you delete your account from the App
  (Settings → Sign out → "Erase ALL data"), every row associated with
  your family is removed within 24 hours, including from the archive.
  Backups age out within 7 days.

### 5. Your rights

You can, at any time:

- **Access** your data via the App itself or by emailing
  nikita.metlitskiy@gmail.com.
- **Export** all your data as a PDF (Settings → Export PDF).
- **Correct** any record by editing it in the App.
- **Delete** all your data (Settings → Delete data → ERASE).
- **Withdraw consent** by deleting your account.

If you are an EU/UK resident, you also have the right to lodge a
complaint with your data protection authority.

### 6. Children's data

Babyline is intended for **adult parents and guardians** to track their
own children. The App is not directed at children, and children
themselves are not the users. Records about your child (name, DOB,
height, weight, etc.) are personal data of minors that you, as the
parent/guardian, voluntarily provide. We process this data only for
the purpose of letting you and invited family members track your
child. We never share it with third parties for marketing.

### 7. Security

- All network traffic is HTTPS/TLS.
- Passwords are stored hashed (bcrypt) by Supabase Auth — we never see
  your plain-text password.
- Database access is gated by Row-Level Security (RLS) — every table
  enforces that you can only read your own family's data.
- We follow industry best practices but no system is 100% secure. If
  you suspect a breach, contact **nikita.metlitskiy@gmail.com** immediately.

### 8. Disclaimer of liability

**THE APP IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE, MEDICAL ACCURACY, OR
NON-INFRINGEMENT.**

By installing and using Babyline you acknowledge that:

1. The App is a **tracker only** — it does **not** provide medical
   advice, diagnosis, or treatment.
2. **All medical decisions must be made in consultation with a licensed
   pediatrician.** Never rely on the App for clinical decision-making.
3. The country-specific vaccination and check-up schedules shown in the
   App are reference information from public health sources and may be
   incomplete or out of date. **Verify the actual schedule with your
   doctor.**
4. Reminders are best-effort; the App may fail to deliver a
   notification due to OS, network, or server issues. **Do not rely on
   Babyline as the sole reminder for time-critical medical events.**
5. **The App's operator accepts no liability** for any direct,
   indirect, incidental, special, consequential, or punitive damages
   arising from your use of the App, including but not limited to
   missed vaccinations, wrong medication doses, allergic reactions,
   developmental delays, or any health outcome whatsoever. **Use of the
   App is at your sole risk.**

### 9. Changes

We may update this policy. Changes are posted at this URL with a new
"Last updated" date. Material changes will also be announced inside
the App.

### 10. Contact

📧 **nikita.metlitskiy@gmail.com**

---

## Русская версия

### 1. Кто мы

Babyline («Приложение») — это частный проект. Контролёр данных —
индивидуальный оператор Приложения («мы»). По вопросам
конфиденциальности и удаления данных пишите: **nikita.metlitskiy@gmail.com**.

### 2. Какие данные мы собираем

При создании аккаунта и использовании Babyline мы собираем:

- **Данные аккаунта:** email, имя профиля, опциональное фото профиля,
  роль (мама / папа / другое), метаданные аутентификации.
- **Данные семьи:** имя ребёнка, пол, дата рождения, опциональные
  начальный рост и вес, страна (для выбора графика прививок).
- **События, которые вы записываете:** сон, кормления, прогулки, пробы
  продуктов, прививки, измерения роста, зубы, достижения, комментарии,
  события календаря, лекарства, прогресс по чек-листам.
- **Данные семейного доступа:** приглашения, список членов семьи,
  отметки активности партнёра.
- **Данные устройства:** APNs push-токен (чтобы мы могли отправлять
  уведомления об активности партнёра), локаль устройства, версия
  приложения.
- **Диагностические логи:** анонимные трассировки ошибок (без личных
  данных), когда приложение сталкивается с багом.

Мы **не собираем**: контакты, геолокацию, фотографии (кроме тех, что вы
явно загружаете как аватар), рекламные идентификаторы, биометрию,
микрофон, камеру (кроме съёмки аватара), журналы звонков, SMS,
календарь телефона (кроме событий, которые вы создаёте внутри
Приложения).

### 3. Где хранятся данные

Все данные хранятся на платформе **Supabase** (PostgreSQL + Storage),
размещённой в ЕС (eu-west-1, Ирландия). Push-уведомления доставляются
через **Apple Push Notification service** (APNs). Аутентификация (вход
через Apple, magic-link, пароль) обрабатывается **Supabase Auth**.

Мы не продаём и не передаём ваши данные третьим лицам для рекламы или
аналитики. Единственные третьи стороны — это поставщики
инфраструктуры:

- **Supabase Inc.** — база данных, аутентификация, хранилище, push.
- **Apple Inc.** — APNs и «Войти через Apple».

### 4. Как долго хранятся данные

- **Активные данные:** пока существует ваш аккаунт.
- **Архив (мягко удалённое):** **30 дней**, потом окончательно удаляется
  автоматическим заданием.
- **Резервные копии:** Supabase хранит 7 дней point-in-time снапшотов.
- **Удаление аккаунта:** при удалении данных из Приложения
  (Настройки → Удалить данные → СТЕРЕТЬ) все строки, связанные с вашей
  семьёй, удаляются в течение 24 часов, включая архив. Резервные копии
  естественно ротируются за 7 дней.

### 5. Ваши права

В любой момент вы можете:

- **Получить доступ** к своим данным через Приложение или по запросу
  на nikita.metlitskiy@gmail.com.
- **Экспортировать** все данные в PDF (Настройки → Экспорт PDF).
- **Изменить** любую запись прямо в Приложении.
- **Удалить** все данные (Настройки → Удалить данные → СТЕРЕТЬ).
- **Отозвать согласие**, удалив аккаунт.

Если вы резидент ЕС/Великобритании, вы также имеете право обратиться
в надзорный орган по защите данных.

### 6. Данные о детях

Babyline предназначен для **взрослых родителей и опекунов**, которые
ведут учёт о своих детях. Приложение не направлено на детей, и сами
дети не являются пользователями. Данные о вашем ребёнке (имя, дата
рождения, рост, вес и т.д.) — это персональные данные
несовершеннолетних, которые вы как родитель/опекун предоставляете
добровольно. Мы обрабатываем эти данные исключительно для того, чтобы
вы и приглашённые члены семьи могли вести записи о вашем ребёнке. Мы
никогда не передаём их третьим лицам для маркетинга.

### 7. Безопасность

- Весь сетевой трафик — HTTPS/TLS.
- Пароли хранятся в виде хэшей (bcrypt) в Supabase Auth — мы никогда
  не видим ваш пароль в открытом виде.
- Доступ к базе ограничен Row-Level Security (RLS) — каждая таблица
  гарантирует, что вы можете читать только данные своей семьи.
- Мы следуем индустриальным практикам, но 100% безопасности не бывает.
  При подозрении на утечку срочно пишите на **nikita.metlitskiy@gmail.com**.

### 8. Отказ от ответственности

**ПРИЛОЖЕНИЕ ПРЕДОСТАВЛЯЕТСЯ «КАК ЕСТЬ», БЕЗ КАКИХ-ЛИБО ГАРАНТИЙ —
ЯВНЫХ ИЛИ ПОДРАЗУМЕВАЕМЫХ — ВКЛЮЧАЯ, НО НЕ ОГРАНИЧИВАЯСЬ ГАРАНТИЯМИ
КОММЕРЧЕСКОЙ ПРИГОДНОСТИ, ПРИГОДНОСТИ ДЛЯ ОПРЕДЕЛЁННОЙ ЦЕЛИ,
МЕДИЦИНСКОЙ ТОЧНОСТИ ИЛИ НЕНАРУШЕНИЯ ПРАВ.**

Устанавливая и используя Babyline, вы подтверждаете, что:

1. Приложение является **только трекером** — оно **не предоставляет**
   медицинских рекомендаций, диагнозов или лечения.
2. **Все медицинские решения должны приниматься в консультации с
   лицензированным педиатром.** Никогда не полагайтесь на Приложение
   для клинических решений.
3. Графики прививок и осмотров по странам, отображаемые в Приложении,
   являются справочной информацией из открытых источников
   общественного здравоохранения и могут быть неполными или
   устаревшими. **Сверяйте фактический график с вашим врачом.**
4. Напоминания работают по принципу best-effort — Приложение может не
   доставить уведомление из-за проблем с ОС, сетью или сервером. **Не
   полагайтесь на Babyline как на единственное напоминание о
   критичных по времени медицинских событиях.**
5. **Оператор Приложения не несёт ответственности** за любой прямой,
   косвенный, случайный, специальный, последующий или штрафной ущерб,
   возникший из-за использования Приложения, включая, но не
   ограничиваясь: пропущенные прививки, ошибки в дозировках лекарств,
   аллергические реакции, задержки развития или любые иные последствия
   для здоровья. **Использование Приложения происходит исключительно
   на ваш страх и риск.**

### 9. Изменения

Мы можем обновлять эту политику. Изменения публикуются по этому URL с
новой датой «Последнее обновление». О существенных изменениях мы также
уведомим внутри Приложения.

### 10. Контакты

📧 **nikita.metlitskiy@gmail.com**
