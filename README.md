<div align="center">

<!-- Animated Banner SVG -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=VINSS%20BOTZ%20REPORT&fontSize=48&fontColor=ffffff&fontAlignY=38&desc=Mass%20Reporter%20Bot%20%7C%20Telegram%20%7C%20Node.js%20v2.0.0&descAlignY=58&descSize=16&animation=fadeIn" width="100%"/>

<!-- Animated Typing -->
<img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=700&size=22&duration=3000&pause=800&color=A855F7&center=true&vCenter=true&multiline=true&repeat=true&width=600&height=80&lines=🚀+Mass+Report+%7C+Multi+Akun+%7C+Cloud+DB;⚡+Powered+by+Telegram+MTProto+%2B+Supabase;🔐+Premium+Access+Control+System" alt="Typing SVG" />

<br/>

<!-- Badges -->
![Node.js](https://img.shields.io/badge/Node.js-≥18.0.0-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-Database-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Version](https://img.shields.io/badge/Version-2.0.0-A855F7?style=for-the-badge&logo=github&logoColor=white)
![License](https://img.shields.io/badge/License-Private-FF4444?style=for-the-badge&logo=opensourceinitiative&logoColor=white)

<br/>

<!-- Snake animation (GitHub only) -->
<!-- <img src="https://raw.githubusercontent.com/platane/platane/output/github-contribution-grid-snake-dark.svg" width="100%"/> -->

</div>

---

<div align="center">

## ✨ Feature Showcase

</div>

```
╔══════════════════════════════════════════════════════════════════╗
║                                                                  ║
║   📢  Report Channel      👤  Report Profile Photo               ║
║   👥  Mass Report         🔐  Multi-Account Login                ║
║   🔒  2FA Support         💎  Premium Access System              ║
║   👑  Owner Panel         ☁️   Supabase Cloud Database            ║
║   📄  JSON Fallback       🔄  Auto Session Restore               ║
║   ✏️   Edit Message UI     ⚡  Async Mass Execution               ║
║                                                                  ║
╚══════════════════════════════════════════════════════════════════╝
```

<div align="center">

<!-- Stats cards -->
<img src="https://img.shields.io/badge/📢_Report_Channel-✅_Active-0f0c29?style=flat-square&labelColor=302b63"/>
<img src="https://img.shields.io/badge/👤_Report_Photo-✅_Active-0f0c29?style=flat-square&labelColor=302b63"/>
<img src="https://img.shields.io/badge/⚡_Mass_Execute-✅_Active-0f0c29?style=flat-square&labelColor=302b63"/>
<img src="https://img.shields.io/badge/☁️_Cloud_DB-✅_Active-0f0c29?style=flat-square&labelColor=302b63"/>

</div>

---

## 📋 Table of Contents

<div align="center">

| | Section |
|:---:|:---|
| 🏗️ | [Struktur Proyek](#%EF%B8%8F-struktur-proyek) |
| 🔧 | [Persyaratan](#-persyaratan) |
| 📦 | [Instalasi](#-instalasi) |
| ⚙️ | [Konfigurasi](#%EF%B8%8F-konfigurasi) |
| ☁️ | [Setup Supabase](#%EF%B8%8F-setup-supabase) |
| 🚀 | [Menjalankan Bot](#-menjalankan-bot) |
| 🔑 | [Sistem Akses](#-sistem-akses) |
| 📖 | [Cara Pakai](#-cara-pakai) |
| 🚩 | [Metode Report](#-metode-report) |
| 🗄️ | [Arsitektur Database](#%EF%B8%8F-arsitektur-database) |
| 📚 | [API Database](#-api-database-dbjs) |
| 🔄 | [Alur Bot](#-alur-bot) |
| 🛠️ | [Troubleshooting](#%EF%B8%8F-troubleshooting) |

</div>

---

## 🏗️ Struktur Proyek

```
📦 script-report-telegram/
│
├── 🤖  telegram_bot.js          ← File utama bot (handler, UI, logic)
├── ⚙️   config.js                ← Konfigurasi (token, keys, Supabase)
├── 📋  package.json              ← Dependencies & scripts
├── 📖  README.md                 ← Dokumentasi ini
│
└── 📁 database/
    ├── 🗄️  db.js                 ← Abstraksi database (Supabase + JSON)
    ├── 👥  premium_users.json    ← Cache lokal premium user
    └── 🔐  user_sessions.json    ← Cache lokal session Telegram
```

---

## 🔧 Persyaratan

<div align="center">

| Kebutuhan | Versi | Link |
|:---:|:---:|:---:|
| ![Node](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white) | >= 18.0.0 | [nodejs.org](https://nodejs.org) |
| ![Telegram](https://img.shields.io/badge/Bot_Token-2CA5E0?style=flat&logo=telegram&logoColor=white) | — | [@BotFather](https://t.me/BotFather) |
| ![API](https://img.shields.io/badge/Telegram_API-2CA5E0?style=flat&logo=telegram&logoColor=white) | — | [my.telegram.org](https://my.telegram.org) |
| ![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=flat&logo=supabase&logoColor=white) | — | [supabase.com](https://supabase.com) *(opsional)* |

</div>

---

## 📦 Instalasi

```bash
# 📥 Clone atau download proyek
git clone <repo-url>
cd script-report-telegram

# 📦 Install semua dependencies
npm install
```

<details>
<summary>📋 <b>Lihat daftar dependencies lengkap</b></summary>

<br/>

| Package | Versi | Fungsi |
|---|:---:|---|
| `node-telegram-bot-api` | `0.66.0` | Bot Telegram via polling |
| `telegram` (gramjs) | `2.26.22` | Telegram MTProto client untuk report |
| `@supabase/supabase-js` | `^2.45.4` | Supabase cloud database client |

</details>

---

## ⚙️ Konfigurasi

Edit file **`config.js`**:

```js
module.exports = {
  // ┌─────────────────────────────────────────┐
  // │  🤖  BOT IDENTITY                       │
  // └─────────────────────────────────────────┘
  BOT_TOKEN:      'YOUR_BOT_TOKEN',        // dari @BotFather
  OWNER_ID:       [123456789, 987654321],  // Telegram User ID owner
  OWNER_USERNAME: ['username1', 'username2'],

  // ┌─────────────────────────────────────────┐
  // │  ☁️   SUPABASE  (opsional)              │
  // └─────────────────────────────────────────┘
  SUPABASE_URL: 'https://xxxx.supabase.co',
  SUPABASE_KEY: 'eyJhbGci...',

  // ┌─────────────────────────────────────────┐
  // │  📄  JSON FALLBACK                      │
  // └─────────────────────────────────────────┘
  PREMIUM_USERS_FILE: 'database/premium_users.json',
  SESSIONS_FILE:      'database/user_sessions.json',

  // ┌─────────────────────────────────────────┐
  // │  🖼️   TAMPILAN                          │
  // └─────────────────────────────────────────┘
  THUMBNAIL_URL: 'https://link-gambar.jpg',

  // ┌─────────────────────────────────────────┐
  // │  📡  TELEGRAM API (my.telegram.org)     │
  // └─────────────────────────────────────────┘
  DEFAULT_API_ID:   '12345678',
  DEFAULT_API_HASH: 'abcdef1234567890abcdef1234567890',

  // ┌─────────────────────────────────────────┐
  // │  ⚡  PENGATURAN REPORT                  │
  // └─────────────────────────────────────────┘
  MAX_REPORTS_PER_SESSION: 100,
  REPORT_DELAY:            500,   // ms antar report
  SESSION_TIMEOUT:         3600,  // detik
};
```

<details>
<summary>💡 <b>Cara dapat Telegram User ID</b></summary>

<br/>

Forward pesan apapun ke **[@userinfobot](https://t.me/userinfobot)** — bot itu akan balas dengan User ID kamu.

</details>

<details>
<summary>💡 <b>Cara dapat API ID & Hash</b></summary>

<br/>

1. Buka **[my.telegram.org](https://my.telegram.org)**
2. Login dengan nomor HP Telegram kamu
3. Klik **API development tools**
4. Isi form → catat `api_id` dan `api_hash`

</details>

---

## ☁️ Setup Supabase

> ⚠️ **Opsional** — bot tetap jalan pakai JSON lokal jika Supabase tidak dikonfigurasi.

<details>
<summary>📖 <b>Langkah Setup Supabase (klik untuk expand)</b></summary>

<br/>

### Step 1 — Buat Project

1. Buka **[supabase.com](https://supabase.com)** → **New Project**
2. Catat **Project URL** dan **anon public key** dari  
   `Settings → API → Project API keys`

### Step 2 — Buat Tabel

Jalankan SQL berikut di **Supabase → SQL Editor**:

```sql
-- 👥 Tabel daftar premium user
CREATE TABLE IF NOT EXISTS premium_users (
  user_id    BIGINT PRIMARY KEY,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- 🔐 Tabel session Telegram tersimpan
CREATE TABLE IF NOT EXISTS user_sessions (
  user_id        BIGINT PRIMARY KEY,
  phone          TEXT,
  api_id         TEXT,
  api_hash       TEXT,
  string_session TEXT,
  updated_at     TIMESTAMPTZ DEFAULT NOW()
);
```

### Step 3 — Isi Config

```js
SUPABASE_URL: 'https://xxxx.supabase.co',  // ← Project URL
SUPABASE_KEY: 'eyJhbGci...',               // ← anon public key
```

</details>

### 🔄 Strategi Failover Database

```
┌──────────────────────────────────────────────────────────┐
│                                                          │
│   BACA:  Supabase → (error?) → JSON Lokal               │
│                                                          │
│   TULIS: Supabase → sync → JSON Lokal (selalu keduanya) │
│                                                          │
│   RESULT: Bot TIDAK PERNAH crash karena DB error ✅      │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

---

## 🚀 Menjalankan Bot

```bash
npm start
```

**Output normal:**

```
🤖 Vinss Botz Report v2.0.0 started!
[DB] Supabase client initialized: https://xxxx.supabase.co
📂 Loading existing sessions...
[DB] Premium users loaded from Supabase: 3
[DB] Sessions loaded from Supabase: 2
✅ Restored: 1234567890 (+6281234567890)
✅ Restored: 9876543210 (+6289876543210)
✅ Vinss Botz Report v2.0.0 running! 2 active session(s).
```

---

## 🔑 Sistem Akses

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  👑  OWNER     →  Akses penuh dari MANA SAJA               │
│                   (private chat, group manapun)             │
│                                                             │
│  💎  PREMIUM   →  Akses penuh dari MANA SAJA               │
│                   (ditambahkan owner via Owner Panel)        │
│                                                             │
│  🚫  USER BIASA →  DITOLAK                                  │
│                   "Hubungi owner untuk beli akses"           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

> Owner otomatis dianggap premium — tidak perlu ditambahkan ke daftar.

---

## 📖 Cara Pakai

### 👤 Untuk User / Premium

<table>
<tr>
<td>

```
/start
  │
  ▼
[🔐 Login Sekarang]
  │
  ▼
Kirim nomor HP
+6281234567890
  │
  ▼
Kirim kode OTP
1 2 3 4 5
  │
  ├─ (ada 2FA?) → kirim password
  │
  ▼
✅ Login berhasil!
/start → pilih menu report
```

</td>
<td>

**Tips:**
- Nomor harus diawali kode negara (`+62`)
- OTP bisa dipisah spasi atau tidak
- Jika akun 2FA, siapkan passwordnya
- Session tersimpan otomatis, tidak perlu login ulang kecuali logout
- Bisa login banyak akun — semuanya ikut report

</td>
</tr>
</table>

### 👑 Untuk Owner — Kelola Premium

| Aksi | Langkah |
|---|---|
| **Tambah premium** | `/start` → `[👑 Owner Panel]` → `[➕ Add Premium]` → kirim User ID |
| **Hapus premium** | `/start` → `[👑 Owner Panel]` → `[➖ Remove Premium]` → kirim User ID |
| **Lihat daftar** | `/start` → `[👑 Owner Panel]` → `[📋 List Premium]` |

---

## 🚩 Metode Report

<div align="center">

| # | Badge | Label | Digunakan untuk |
|:---:|---|---|---|
| 1 | ![](https://img.shields.io/badge/🗑️_Spam-FF4444?style=flat-square) | Spam | Konten spam berulang |
| 2 | ![](https://img.shields.io/badge/🔫_Kekerasan-FF6B35?style=flat-square) | Kekerasan | Konten kekerasan/gore |
| 3 | ![](https://img.shields.io/badge/🔞_Pornografi-FF1493?style=flat-square) | Pornografi | Konten seksual eksplisit |
| 4 | ![](https://img.shields.io/badge/👶_Kekerasan_Anak-CC0000?style=flat-square) | Kekerasan Anak | Child abuse content |
| 5 | ![](https://img.shields.io/badge/💊_Narkotika-8B4513?style=flat-square) | Narkotika | Promosi narkoba |
| 6 | ![](https://img.shields.io/badge/🆔_Data_Pribadi-FF8C00?style=flat-square) | Data Pribadi | Doxing / kebocoran data |
| 7 | ![](https://img.shields.io/badge/😞_Akun_Palsu-696969?style=flat-square) | Akun Palsu | Scam / impersonation |
| 8 | ![](https://img.shields.io/badge/©️_Hak_Cipta-4169E1?style=flat-square) | Hak Cipta | Pelanggaran copyright |
| 9 | ![](https://img.shields.io/badge/🌍_Tdk_Relevan-228B22?style=flat-square) | Konten Tdk Relevan | Geo irrelevant |
| 10 | ![](https://img.shields.io/badge/❗_Custom-A855F7?style=flat-square) | Lainnya (Custom) | Alasan bebas/custom |

</div>

---

## 🗄️ Arsitektur Database

```
                     ┌──────────────────────┐
                     │   telegram_bot.js     │
                     │  (main application)   │
                     └──────────┬───────────┘
                                │  require('./database/db')
                     ┌──────────▼───────────┐
                     │     database/db.js    │
                     │  (abstraction layer)  │
                     └────────┬──────┬───────┘
                              │      │
               ┌──────────────▼      ▼──────────────┐
               │                                    │
  ┌────────────▼────────────┐    ┌──────────────────▼──────┐
  │       ☁️  SUPABASE       │    │      📄  JSON LOCAL      │
  │     (cloud · utama)     │    │   (fallback · cache)     │
  │                         │    │                          │
  │  table: premium_users   │◄──►│  premium_users.json      │
  │  table: user_sessions   │◄──►│  user_sessions.json      │
  │                         │    │                          │
  │  ✅ real-time sync       │    │  ✅ always available     │
  └─────────────────────────┘    └──────────────────────────┘
```

---

## 📚 API Database (db.js)

<details>
<summary>🔍 <b>loadPremiumUsers()</b> → <code>Promise&lt;Set&lt;number&gt;&gt;</code></summary>

Load semua ID premium user. Prioritas Supabase → JSON fallback.

```js
const premiumUsers = await db.loadPremiumUsers();
// → Set { 1234567890, 9876543210 }
```
</details>

<details>
<summary>➕ <b>addPremiumUser(userId)</b> → <code>Promise&lt;void&gt;</code></summary>

Tambah user ke daftar premium (Supabase + JSON).

```js
await db.addPremiumUser(1234567890);
```
</details>

<details>
<summary>➖ <b>removePremiumUser(userId)</b> → <code>Promise&lt;void&gt;</code></summary>

Hapus user dari daftar premium.

```js
await db.removePremiumUser(1234567890);
```
</details>

<details>
<summary>🔐 <b>loadSessions()</b> → <code>Promise&lt;Object&gt;</code></summary>

Load semua session tersimpan.

```js
const sessions = await db.loadSessions();
// → { '1234567890': { phone, api_id, api_hash, stringSession } }
```
</details>

<details>
<summary>💾 <b>saveSession(userId, data)</b> → <code>Promise&lt;void&gt;</code></summary>

Simpan satu session setelah login berhasil.

```js
await db.saveSession(userId, {
  phone:         '+6281234567890',
  api_id:        '12345678',
  api_hash:      'abcdef...',
  stringSession: '1AQAAABc...',
});
```
</details>

<details>
<summary>🗑️ <b>deleteSession(userId)</b> → <code>Promise&lt;void&gt;</code></summary>

Hapus session saat logout.

```js
await db.deleteSession(userId);
```
</details>

<details>
<summary>📦 <b>saveAllSessions(userSessions)</b> → <code>Promise&lt;void&gt;</code></summary>

Bulk upsert semua session aktif (dipakai saat startup).

```js
await db.saveAllSessions(userSessions);
```
</details>

<details>
<summary>✅ <b>supabaseReady()</b> → <code>boolean</code></summary>

Cek apakah Supabase aktif dan terkonfigurasi.

```js
if (db.supabaseReady()) {
  console.log('Cloud database aktif');
} else {
  console.log('Mode JSON lokal');
}
```
</details>

---

## 🔄 Alur Bot

### 🔐 Alur Login

```
User kirim /start
        │
        ▼
┌───────────────────────┐
│  hasAccess(userId) ?  │
└──────┬──────────┬─────┘
       │ YES      │ NO
       ▼          ▼
  Sudah login?  ❌ Akses ditolak
  │YES  │NO      "Hubungi owner"
  ▼     ▼
Menu  Login Screen
      [🔐 Login Sekarang]
              │
              ▼
      Input nomor HP
              │
              ▼
      sendCode() → phoneCodeHash
              │
              ▼
      Input kode OTP
              │
         ┌────┴─────┐
         │          │
         ▼          ▼
      ✅ Sukses   SESSION_PASSWORD_NEEDED
      Simpan          │
      session         ▼
         │      Input password 2FA
         │      computeCheck() → CheckPassword()
         │            │
         └────────────┘
                  │
                  ▼
             ✅ Login berhasil
             Session tersimpan ke DB
```

### 🚩 Alur Report

```
Menu Utama
    │
    ├─[📢 Report Channel]─────┐
    └─[👤 Report Profile]─────┤
                              │ edit pesan
                              ▼
                    ┌─────────────────┐
                    │  Pilih Metode   │
                    │   (1 – 10)      │
                    └────────┬────────┘
                             │ edit pesan
                    ┌────────▼────────┐
                    │  Metode = 10?   │
                    │  Input custom   │
                    └────────┬────────┘
                             │ edit pesan
                    ┌────────▼────────┐
                    │  Input username │
                    │     target      │
                    └────────┬────────┘
                             │ edit pesan
                    ┌────────▼────────┐
                    │  Input jumlah   │
                    │  report per akun│
                    └────────┬────────┘
                             │ edit pesan
                    ┌────────▼────────────────────────┐
                    │  🔄 runMassReport()              │
                    │  Promise.allSettled([            │
                    │    akun1.report(), ← parallel   │
                    │    akun2.report(), ← parallel   │
                    │    akun3.report(), ← parallel   │
                    │  ])                              │
                    └────────┬────────────────────────┘
                             │ edit pesan
                    ┌────────▼────────┐
                    │  ✅ Hasil Report │
                    │  [🔄 Lagi]      │
                    │  [🏠 Menu]      │
                    └─────────────────┘
```

---

## 🛠️ Troubleshooting

<details>
<summary>❌ <b>TypeError: fetch failed (Supabase)</b></summary>

**Penyebab:** URL/Key Supabase salah atau tidak ada koneksi internet.

**Solusi:**
- Cek `SUPABASE_URL` dan `SUPABASE_KEY` di `config.js`
- Pastikan koneksi internet aktif
- Bot tetap berjalan normal menggunakan **JSON lokal** sebagai fallback ✅

</details>

<details>
<summary>❌ <b>signIn is not a function</b></summary>

**Penyebab:** gramjs v2 tidak memiliki `client.signIn()`.

**Solusi:** Sudah diperbaiki. Bot menggunakan:
- `Api.auth.SignIn` untuk OTP
- `Api.auth.CheckPassword` untuk 2FA

</details>

<details>
<summary>❌ <b>⚠️ Expired: userId saat startup</b></summary>

**Penyebab:** String session kedaluwarsa — akun logout dari perangkat lain atau password berubah.

**Solusi:** User login ulang via bot. Session lama otomatis dihapus dari DB.

</details>

<details>
<summary>❌ <b>Bot tidak merespons</b></summary>

Cek urutan berikut:
1. `BOT_TOKEN` benar di `config.js`
2. Tidak ada instance bot lain yang running (konflik polling)
3. Bot tidak di-block Telegram
4. Restart: `npm start`

</details>

<details>
<summary>❌ <b>Akses Ditolak padahal sudah login</b></summary>

**Penyebab:** User belum ditambahkan ke daftar premium.

**Solusi:** Owner tambahkan User ID via:
```
/start → [👑 Owner Panel] → [➕ Add Premium] → kirim User ID
```

</details>

---

## 📝 Error Log Reference

<div align="center">

| Log | Status | Tindakan |
|---|:---:|---|
| `[DB] Supabase client initialized` | ✅ Normal | Supabase aktif |
| `[DB] Supabase belum dikonfigurasi` | ⚠️ Info | Isi config atau biarkan (pakai JSON) |
| `[DB] Supabase saveAllSessions error: fetch failed` | ⚠️ Warning | Cek URL/KEY, bot tetap jalan via JSON |
| `✅ Restored: <userId>` | ✅ Normal | Session berhasil dipulihkan |
| `⚠️ Expired: <userId>` | ⚠️ Warning | Session kedaluwarsa, user login ulang |
| `Polling error: ...` | ⚠️ Warning | Error koneksi, bot retry otomatis |
| `doReport [uid]: <error>` | ❌ Error | Satu akun gagal report, akun lain tetap jalan |

</div>

---

<div align="center">

<!-- Footer Wave -->
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:24243e,50:302b63,100:0f0c29&height=120&section=footer" width="100%"/>

**Vinss Botz Report** `v2.0.0`

Made with ❤️ by [@VinssDev](https://t.me/VinssDev) & [@VinssBoyz](https://t.me/VinssBoyz)

![Visitors](https://visitor-badge.laobi.icu/badge?page_id=vinssbotz.report&left_color=302b63&right_color=A855F7&left_text=Views)
&nbsp;
![Stars](https://img.shields.io/github/stars/vinssdev/report-bot?style=social)

*Dokumentasi ini untuk versi **v2.0.0** — Dilarang disebar tanpa izin*

</div>
