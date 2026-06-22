# 📋 "1 Oylik Rivojlanish Jadvali" — To'liq Mahsulot Reja

> Bu fayl loyihaning to'liq spec'i. Yangi chatda shu faylni yuklab: "mana loyiha reja, davom ettiramiz" deyish kifoya.
>
> **Versiya tarixi:** Reja bir necha marta yangilandi (pastga qarang — 9-bo'lim, "Qaror tarixi"). Bu — ENG SO'NGGI, AMALDAGI reja.

---

## 1. Umumiy g'oya

Foydalanuvchilar **kunlik, oylik, yillik** rivojlanish rejalarini o'zlari yaratadi (vazifalar ro'yxati), har kuni bajargan vazifalarini belgilaydi, va har bir reja turi uchun **alohida** progress-grafik (0 dan reja vazifalar soniga teng max qiymatgacha) ko'radi — trading-style ko'tarilish/pasayish chizig'i bilan.

**Yakuniy maqsad:** to'liq biznes mahsulot, ko'p foydalanuvchili, login bilan, oxir-oqibat App Store/Play Store'da.
**Boshlanish bosqichi:** veb-sayt (link orqali ochiladigan), App Store/Play Store'siz — pastga qarang, 2-bo'lim.

---

## 2. Tanlangan texnik stack — AMALDAGI YAKUNIY QAROR

> ⚠️ Bu reja 3 marta o'zgardi (React+Vite → React Native+Expo → yana React+Vite). Sabab va tafsilotlar 9-bo'limda. **Hozir amalda bo'lgan qaror — pastdagi jadval.**

### Bosqich 1 — HOZIR boshlanadigan (web / PWA)

```
Frontend:   React + Vite
Backend:    Node.js + Express
Database:   MongoDB Atlas (bulutda)
Auth:       Email/parol (JWT) + Google OAuth
Joylashuv:  Veb-sayt (domen + hosting), link orqali ochiladi
            "Bosh ekranga qo'shish" (PWA) — ilova kabi ko'rinishi uchun
```

**Nima uchun bu yo'l tanlandi:**
- App Store/Play Store, Apple Developer ($99/yil), Mac, Expo EAS Build — bularning HECH BIRI hozir kerak emas
- Eng tez, eng arzon, eng oson boshlash yo'li
- Google orqali qidirib topiladi, linkni bosib ochiladi, "ilova" kabi ishlatiladi (PWA "bosh ekranga qo'shish" funksiyasi orqali)

**Hozircha QILINMAYDIGAN narsalar (ataylab kechiktirilgan):**
- ❌ Push-notification (ilova yopiq bo'lganda xabar kelishi) — web'da to'liq ishlamaydi, ayniqsa iPhone'da
- ❌ Face ID / Touch ID orqali qulflash — web cheklovi, ishlamaydi
- ❌ App Store / Play Store'ga joylashtirish

### Bosqich 2 — KELAJAKDA (agar va qachon kerak bo'lsa)

Agar push-notification yoki Face ID/Touch ID zarur bo'lib qolsa, native ilovaga o'tish kerak bo'ladi:

```
Mobil ilova:  React Native + Expo
Push:         Firebase Cloud Messaging (FCM)
Build:        Expo EAS Build (Windows'dan turib bulutda build qilish — Mac kerak emas)
```

**Windows + iOS masalasi (agar Bosqich 2'ga o'tilsa):**
- Xcode faqat macOS'da ishlaydi, lekin **Expo EAS Build** orqali Windows'dan turib bulutda build qilish mumkin, Mac sotib olish shart emas
- EAS Build bepul tarifi: oyiga 15 Android + 15 iOS build (MVP uchun yetarli)
- **Apple Developer hisobi — $99/yil** — bu hech qachon, hech qanday usulda bepul bo'lmaydi (Mac bilan ham, EAS bilan ham), Apple'ning o'zi talab qiladi
- Google Play Developer — $25 (bir martalik)
- Agar foydalanuvchida Mac bo'lsa: EAS Build pulini tejaydi (lokal build bepul), lekin Apple Developer $99/yil baribir qoladi

---

## 3. Funksional talablar

### 3.1 Auth va xavfsizlik
- [ ] Ro'yxatdan o'tish / kirish: email + parol
- [ ] Google orqali kirish
- [ ] JWT token uzoq muddatli (masalan 30 kun) — har safar qayta login so'ralmasin
- [ ] Ilova ichida qo'shimcha qulflash qatlami: PIN-kod (4-6 xonali)
- [ ] *(Bosqich 2, native ilovada)* Face ID / Touch ID orqali qulfni ochish

### 3.2 Reja turlari — uchtasi alohida
- [ ] **Kunlik reja** — bugungi kun uchun vazifalar
- [ ] **Oylik reja** — oy davomida kuzatiladigan vazifalar (hozirgi prototipdagi kabi)
- [ ] **Yillik reja** — yil davomida kuzatiladigan vazifalar
- [ ] Uchtasi mustaqil: ma'lumotlari, grafiklari, hisoblari bir-biriga aralashmaydi

### 3.3 Reja va vazifalarni boshqarish (CRUD)
- [ ] Foydalanuvchi o'zi vazifalar ro'yxatini kiritadi (nomi, ehtimol emoji/belgisi)
- [ ] Har bir vazifani **tahrirlash** (edit) imkoni
- [ ] Har bir vazifani **o'chirish** (delete) imkoni — bittalab
- [ ] **Hammasini birdan o'chirish** imkoni — albatta tasdiqlash (confirm) oynasi bilan

### 3.4 Progress-grafik mantig'i (muhim qoida)
- Grafikning maksimal qiymati = shu kundagi/davrdagi **vazifalar soni**
  - Misol: foydalanuvchi 10 ta vazifa qo'ygan kun uchun → grafik 0–10 oralig'ida
  - Misol: 5 ta vazifa qo'ygan kun uchun → grafik 0–5 oralig'ida (5 ham bor)
- Har kuni nechta vazifa bajarilgan bo'lsa (checkbox bosilgan), grafikdagi shu kunning ball avtomatik shu songa teng bo'ladi (foydalanuvchi qo'lda alohida ball tanlamaydi — checkboxlar sonidan hisoblanadi)
- Bajarilmagan kun → 0
- Kunlik / Oylik / Yillik — har birining grafigi alohida chiziladi, qo'shilib ketmaydi

### 3.5 Vizualizatsiya
- [ ] Trading-style chiziq: ko'tarilganda yashil, pasayganda qizil segment
- [ ] **Haftalik trend** — oxirgi 7 kunlik ko'tarilish/pasayish ko'rinishi (mini-sparkline yoki kattaroq grafik)
- [ ] To'liq responsive: katta ekranda dashboard, kichik ekranda (≤280–380px) "kunlik kartochka" rejimi (oldingi prototipdagi naqsh — ‹›navigatsiya, swipe, katta checkboxlar)

### 3.6 Ma'lumotlar saqlanishi
- Hammasi **MongoDB**da, foydalanuvchi hisobiga bog'langan (boshqa qurilmadan kirsa ham ma'lumot bir xil bo'ladi — `localStorage` emas, real backend)

### 3.7 Bildirishnoma — HOZIRCHA KECHIKTIRILDI
- Push-notification g'oyasi yoqdi, lekin bu **Bosqich 2** (native ilova) talab qiladi
- Hozirgi web bosqichida muqobil: **in-app eslatma** (foydalanuvchi sahifani ochganda, "bugun hali N ta vazifa belgilanmagan" banner) — bu web'da to'liq ishlaydi, qo'shimcha infrastruktura kerak emas
- Email eslatma (kuniga bir marta, backend cron job orqali) — bu ham web bosqichida qo'shilishi mumkin, agar xohlansa

---

## 4. Ma'lumotlar modeli (MongoDB, dastlabki versiya)

```js
// User
{
  _id, email, passwordHash (agar email/parol bilan),
  googleId (agar Google orqali),
  pinHash, // ilova-ichi qulflash uchun
  createdAt
}

// Plan  (kunlik / oylik / yillik — barchasi shu model, "type" maydoni bilan ajratiladi)
{
  _id, userId, type: "daily" | "monthly" | "yearly",
  title, startDate, endDate,
  tasks: [
    { _id, label, emoji }
  ],
  createdAt, updatedAt
}

// DailyLog  (har bir reja uchun, har kun uchun, qaysi tasklar bajarilgani)
{
  _id, planId, date,
  completedTaskIds: [taskId, taskId, ...],
  // score = completedTaskIds.length, maxScore = tasks.length (shu kunga tegishli)
}
```

---

## 5. API endpointlar (dastlabki versiya)

```
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/google
GET    /api/auth/me
POST   /api/auth/set-pin
POST   /api/auth/verify-pin

GET    /api/plans?type=daily|monthly|yearly
POST   /api/plans
PUT    /api/plans/:id
DELETE /api/plans/:id
DELETE /api/plans            (hammasini o'chirish, type bo'yicha, confirm bilan)

POST   /api/plans/:id/tasks
PUT    /api/plans/:id/tasks/:taskId
DELETE /api/plans/:id/tasks/:taskId

GET    /api/plans/:id/log?date=YYYY-MM-DD
PUT    /api/plans/:id/log     (shu kun uchun completedTaskIds yangilash)

GET    /api/plans/:id/trend?days=7   (grafik/sparkline uchun)
```

---

## 6. Ishlab chiqish tartibi (MVP bosqichlari — AMALDAGI)

1. **Auth** — register/login (email+parol), Google OAuth, JWT, "meni eslab qol"
2. **Bitta reja turi to'liq** (masalan kunlik) — CRUD + checkbox + avtomatik grafik
3. **Oylik va yillikni** xuddi shu naqsh asosida qo'shish
4. **PIN-qulflash** ilova ichida
5. **Haftalik trend** va statistikalar
6. **Deploy** — domen + hosting (frontend va backend uchun), MongoDB Atlas ulanishi
7. *(Bosqich 2, kelajakda)* React Native ilovaga ko'chirish + Push-notification + Face ID/Touch ID + App Store/Play Store

---

## 7. Hozircha ochiq qolgan savollar

- [ ] Dizayn yo'nalishi: hozirgi "dark dashboard / terminal" estetikasi davom etadimi, yoki yangi reja uchun qayta ko'riladimi?
- [ ] Bitta foydalanuvchi bir nechta **kunlik reja shabloni** yaratishi mumkinmi (masalan "ish kuni" va "dam olish kuni" uchun alohida), yoki har kun uchun bitta umumiy ro'yxat?
- [ ] Oylik/yillik rejalarda kunlik checkbox tracking qanday ishlaydi — har kuni alohida belgilash kerak bo'ladimi (hozirgi prototipdagi kabi), yoki davr oxirida bir martalik baholash?
- [ ] In-app eslatma yoki email eslatma — qaysi birini (yoki ikkisini ham) qo'shamiz?
- [ ] Til: faqat o'zbek tilida qoladimi, yoki ko'p tillilik (i18n) kerak bo'ladimi?
- [ ] Domen nomi va hosting xizmati qaysi bo'ladi (masalan Vercel/Netlify frontend uchun, Render/Railway backend uchun)?

---

## 8. Joriy holat (qaerda to'xtagan edik)

Hali kod yozilmagan — faqat reja va qarorlar tasdiqlangan. Keyingi qadam:
1. `backend/` papkasida `package.json`, `.env` namunasi, MongoDB ulanish kodi (`config/db.js`)
2. `User` va `Plan` MongoDB modellari
3. Auth route'lar (`register`, `login`, `google`)
4. `frontend/` papkasida Vite loyihasi, login/register sahifalari

---

## 9. Qaror tarixi (nima uchun stack o'zgargan — eslatma uchun)

1. **Boshlanish:** React + Vite + Node + Express + MongoDB Atlas + Google OAuth — oddiy web app sifatida
2. **O'zgarish 1:** Foydalanuvchi "to'liq biznes, App Store/Play Store'da" dedi → talablar kengaydi (login + PIN/biometrika, kunlik/oylik/yillik alohida rejalar, edit/delete, haftalik trend)
3. **O'zgarish 2:** Push-notification "ilova yopiq bo'lsa ham kelsin" deyilgani sababli → stack React Native + Expo + FCM'ga o'zgartirildi (chunki bu faqat native ilovada to'liq ishlaydi)
4. **Windows muammosi aniqlandi:** Foydalanuvchi noutbuki Windows, iOS uchun Xcode/Mac kerak → Expo EAS Build yechimi taklif qilindi (Mac kerak emas, lekin Apple Developer $99/yil baribir kerak)
5. **Mac haqida savol:** Agar Mac bo'lsa — EAS Build pulini tejaydi, lekin Apple Developer $99/yil baribir qoladi
6. **YAKUNIY QAROR:** Foydalanuvchi murakkablik va xarajatni ko'rib, **"link bilan boshlaymiz, push/Face ID'ni keyinroq qo'shamiz"** dedi → stack yana React + Vite (web/PWA)ga qaytarildi, App Store/Play Store va native funksiyalar "Bosqich 2" sifatida kelajakka surildi
