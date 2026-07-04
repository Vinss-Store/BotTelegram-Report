# 🤖 Vinss Botz Report — Dokumentasi Lengkap

> Mass Reporter Bot berbasis Telegram | Node.js v2.0.0  
> Dibuat oleh: [@VinssDev](https://t.me/VinssDev) & [@VinssBoyz](https://t.me/VinssBoyz)

---

## 📋 Daftar Isi

1. [Fitur](#-fitur)
2. [Struktur Proyek](#-struktur-proyek)
3. [Persyaratan](#-persyaratan)
4. [Instalasi](#-instalasi)
5. [Konfigurasi](#-konfigurasi)
6. [Setup Supabase](#-setup-supabase)
7. [Menjalankan Bot](#-menjalankan-bot)
8. [Sistem Akses](#-sistem-akses)
9. [Cara Pakai](#-cara-pakai)
10. [Metode Report](#-metode-report)
11. [Arsitektur Database](#-arsitektur-database)
12. [API Database (db.js)](#-api-database-dbjs)
13. [Alur Bot](#-alur-bot)
14. [Troubleshooting](#-troubleshooting)
15. [Error Log Umum](#-error-log-umum)

---

## ✨ Fitur

| Fitur | Keterangan |
|---|---|
| 📢 Report Channel | Laporkan channel/grup publik Telegram |
| 👤 Report Profile Photo | Laporkan foto profil akun Telegram |
| 👥 Mass Report | Semua akun yang login ikut report sekaligus |
| 🔐 Login Multi-Akun | Bisa login banyak akun, semua dipakai saat report |
| 🔒 2FA Support | Mendukung akun dengan Two-Factor Authentication |
| 💎 Sistem Premium | Akses dikontrol owner, hanya premium yang bisa pakai |
| 👑 Owner Panel | Manajemen premium user (add/remove/list) |
| ☁️ Supabase Database | Data tersimpan di cloud, sync real-time |
| 📄 JSON Fallback | Otomatis pakai JSON lokal kalau Supabase offline |
| 🔄 Session Restore | Session Telegram tersimpan, tidak perlu login ulang |
| ✏️ Edit Message UI | Setiap interaksi tombol mengedit pesan yang sama (clean UI) |

---

## 📁 Struktur Proyek

```
script-report-telegram/
├── telegram_bot.js          # File utama bot
├── config.js                # Konfigurasi (token, API keys, dll)
├── package.json             # Dependencies
├── README.md                # Dokumentasi ini
├── database/
│   ├── db.js                # Layer abstraksi database (Supabase + JSON)
│   ├── premium_users.json   # Cache lokal daftar premium user
│   └── user_sessions.json   # Cache lokal session Telegram
└── sessions/                # Folder session (dibuat otomatis)
```

---

## 🔧 Persyaratan

| Kebutuhan | Versi / Keterangan |
|---|---|
| Node.js | >= 18.0.0 |
| Telegram Bot Token | Dari [@BotFather](https://t.me/BotFather) |
| Telegram API ID & Hash | Dari [my.telegram.org](https://my.telegram.org) |
| Supabase Account | [supabase.com](https://supabase.com) (opsional, ada fallback JSON) |

---

## 📦 Instalasi

```bash
# 1. Clone / download proyek
git clone <repo-url>
cd script-report-telegram

# 2. Install dependencies
npm install
```

**Dependencies yang diinstall:**

| Package | Versi | Fungsi |
|---|---|---|
| `node-telegram-bot-api` | 0.66.0 | Bot Telegram (polling) |
| `telegram` | 2.26.22 | Telegram MTProto client (gramjs) |
| `@supabase/supabase-js` | ^2.45.4 | Supabase database client |

---

## ⚙️ Konfigurasi

Edit file `config.js`:

```js
module.exports = {
  // ── Bot Token (dari @BotFather) ──────────────────────
  BOT_TOKEN: 'YOUR_BOT_TOKEN',

  // ── Owner (bisa satu atau array) ──────────────────────
  OWNER_ID:       [123456789, 987654321],   // Telegram User ID
  OWNER_USERNAME: ['username1', 'username2'],

  // ── Supabase (opsional) ───────────────────────────────
  SUPABASE_URL: 'https://xxxx.supabase.co',
  SUPABASE_KEY: 'eyJhbGci...',

  // ── Fallback JSON ─────────────────────────────────────
  PREMIUM_USERS_FILE: 'database/premium_users.json',
  SESSIONS_FILE:      'database/user_sessions.json',

  // ── Tampilan ──────────────────────────────────────────
  THUMBNAIL_URL: 'https://link-gambar-thumbnail.jpg',

  // ── Telegram API (dari my.telegram.org) ───────────────
  DEFAULT_API_ID:   '12345678',
  DEFAULT_API_HASH: 'abcdef1234567890abcdef1234567890',

  // ── Pengaturan Report ─────────────────────────────────
  MAX_REPORTS_PER_SESSION: 100,
  REPORT_DELAY:   500,   // jeda antar report (ms)
  SESSION_TIMEOUT: 3600, // timeout session (detik)
};
```

### Cara dapat Telegram User ID

Forward pesan apapun ke bot [@userinfobot](https://t.me/userinfobot), bot tersebut akan membalas dengan User ID Anda.

### Cara dapat API ID & Hash

1. Buka [my.telegram.org](https://my.telegram.org)
2. Login dengan nomor HP Telegram
3. Klik **API development tools**
4. Isi form, lalu catat `api_id` dan `api_hash`

---

## ☁️ Setup Supabase

> Lewati bagian ini jika ingin pakai JSON lokal saja.

### 1. Buat Project

1. Buka [supabase.com](https://supabase.com) → **New Project**
2. Catat **Project URL** dan **anon public key** dari **Settings → API**

### 2. Buat Tabel

Jalankan SQL berikut di **Supabase → SQL Editor**:

```sql
-- Tabel daftar premium user
CREATE TABLE IF NOT EXISTS premium_users (
  user_id    BIGINT PRIMARY KEY,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Tabel session Telegram yang tersimpan
CREATE TABLE IF NOT EXISTS user_sessions (
  user_id        BIGINT PRIMARY KEY,
  phone          TEXT,
  api_id         TEXT,
  api_hash       TEXT,
  string_session TEXT,
  updated_at     TIMESTAMPTZ DEFAULT NOW()
);
```

### 3. Isi Config

```js
SUPABASE_URL: 'https://xxxx.supabase.co',   // Project URL
SUPABASE_KEY: 'eyJhbGci...',                // anon public key
```

### Perilaku Fallback

```
Supabase tersambung  →  Baca/tulis ke Supabase + sync ke JSON lokal
Supabase error/offline →  Otomatis pakai JSON lokal, tidak crash
```

---

## 🚀 Menjalankan Bot

```bash
# Jalankan bot
npm start

# Atau langsung
node telegram_bot.js
```

**Output normal saat startup:**

```
🤖 Vinss Botz Report v2.0.0 started!
[DB] Supabase client initialized: https://xxxx.supabase.co
📂 Loading existing sessions...
[DB] Premium users loaded from Supabase: 3
[DB] Sessions loaded from Supabase: 2
✅ Restored: 1234567890 (+6281234567890)
✅ Vinss Botz Report v2.0.0 running! 2 active session(s).
```

---

## 🔑 Sistem Akses

```
┌─────────────────────────────────────────────────────┐
│  OWNER   →  Akses penuh dari mana saja               │
│              (private chat, group manapun)            │
│                                                       │
│  PREMIUM →  Akses penuh dari mana saja               │
│              (ditambahkan owner via Owner Panel)      │
│                                                       │
│  USER BIASA → DITOLAK                                │
│              Harus beli akses ke owner               │
└─────────────────────────────────────────────────────┘
```

> **Owner** secara otomatis dianggap premium. Tidak perlu ditambahkan ke daftar premium.

---

## 📖 Cara Pakai

### Untuk User / Premium

```
1. Buka private chat bot → /start
2. Klik [🔐 Login Sekarang]
3. Kirim nomor HP (contoh: +6281234567890)
4. Masukkan kode OTP dari Telegram
5. (Jika 2FA) Masukkan password Two-Factor Authentication
6. Setelah login → ketik /start → pilih menu report
```

### Untuk Owner — Tambah Premium User

```
1. Ketik /start di chat bot
2. Klik [👑 Owner Panel]
3. Klik [➕ Add Premium]
4. Kirim User ID target (contoh: 1234567890)
```

### Untuk Owner — Hapus Premium User

```
1. Ketik /start → [👑 Owner Panel]
2. Klik [➖ Remove Premium]
3. Kirim User ID yang ingin dihapus
```

---

## 🚩 Metode Report

| No | Label | Keterangan |
|---|---|---|
| 1 | Spam | Konten spam |
| 2 | Kekerasan | Konten kekerasan |
| 3 | Pornografi | Konten pornografi |
| 4 | Kekerasan Anak | Konten kekerasan anak |
| 5 | Narkotika | Promosi narkotika |
| 6 | Data Pribadi | Kebocoran data pribadi |
| 7 | Akun Palsu | Akun palsu / scam |
| 8 | Hak Cipta | Pelanggaran hak cipta |
| 9 | Konten Tdk Relevan | Konten tidak relevan secara geografis |
| 10 | Lainnya (Custom) | Pesan alasan bebas / custom |

---

## 🗄️ Arsitektur Database

```
                    ┌─────────────────┐
                    │   telegram_bot  │
                    │      .js        │
                    └────────┬────────┘
                             │ import
                    ┌────────▼────────┐
                    │   database/     │
                    │     db.js       │  ← Layer abstraksi
                    └──────┬──┬───────┘
                           │  │
              ┌────────────▼  ▼─────────────┐
              │                             │
   ┌──────────▼──────────┐   ┌─────────────▼──────────┐
   │     Supabase        │   │    JSON Lokal           │
   │   (cloud, utama)    │   │  (fallback / cache)     │
   │                     │   │                         │
   │  • premium_users    │   │  • premium_users.json   │
   │  • user_sessions    │   │  • user_sessions.json   │
   └─────────────────────┘   └─────────────────────────┘
```

**Strategi tulis:**
- Supabase → tulis dulu ke Supabase, lalu sync JSON
- Error Supabase → tetap tulis ke JSON lokal

**Strategi baca:**
- Supabase tersambung → baca dari Supabase (data terbaru)
- Supabase error → baca dari JSON lokal (cache terakhir)

---

## 📚 API Database (db.js)

### `loadPremiumUsers()` → `Promise<Set<number>>`
Load semua ID premium user. Prioritas: Supabase → JSON.
```js
const premiumUsers = await db.loadPremiumUsers();
// Returns: Set { 1234567890, 9876543210 }
```

### `addPremiumUser(userId)` → `Promise<void>`
Tambah user ke daftar premium.
```js
await db.addPremiumUser(1234567890);
```

### `removePremiumUser(userId)` → `Promise<void>`
Hapus user dari daftar premium.
```js
await db.removePremiumUser(1234567890);
```

### `loadSessions()` → `Promise<Object>`
Load semua session tersimpan.
```js
const sessions = await db.loadSessions();
// Returns: { '1234567890': { phone, api_id, api_hash, stringSession } }
```

### `saveSession(userId, sessionData)` → `Promise<void>`
Simpan satu session setelah login berhasil.
```js
await db.saveSession(userId, {
  phone: '+6281234567890',
  api_id: '12345678',
  api_hash: 'abcdef...',
  stringSession: '1AQAAABc...',
});
```

### `deleteSession(userId)` → `Promise<void>`
Hapus session saat logout.
```js
await db.deleteSession(userId);
```

### `saveAllSessions(userSessions)` → `Promise<void>`
Bulk upsert semua session aktif (dipakai saat startup).
```js
await db.saveAllSessions(userSessions);
```

### `supabaseReady()` → `boolean`
Cek apakah Supabase sudah dikonfigurasi dan aktif.
```js
if (db.supabaseReady()) {
  console.log('Supabase aktif');
}
```

---

## 🔄 Alur Bot

### Alur Login

```
User kirim /start
      │
      ▼
Cek hasAccess(userId)?
   Tidak → Tolak, info ke owner
   Ya    ▼
Sudah login? → Ya → Tampilkan menu
   Tidak ▼
Tampilkan halaman login
      │
User klik [🔐 Login Sekarang]
      │
      ▼
Input nomor HP → sendCode() → dapat phoneCodeHash
      │
      ▼
Input kode OTP → api.auth.SignIn()
      │
      ├── Sukses → Simpan session → Tampilkan menu
      │
      └── Error SESSION_PASSWORD_NEEDED
                │
                ▼
          Input password 2FA → account.GetPassword()
                              → computeCheck()
                              → api.auth.CheckPassword()
                              → Simpan session → Tampilkan menu
```

### Alur Report

```
Menu → Pilih [📢 Report Channel / 👤 Report Profile Photo]
                │
                ▼ (edit pesan)
         Pilih metode (1-10)
                │
                ▼ (edit pesan)
    [Metode 10] → Input custom text
                │
                ▼
         Input username target
                │
                ▼
         Input jumlah report per akun
                │
                ▼ (edit pesan)
    runMassReport() — semua akun login report sekaligus
                │
                ▼ (edit pesan)
         Hasil report + tombol [🔄 Report Lagi] / [🏠 Menu]
```

---

## 🛠️ Troubleshooting

### ❌ `TypeError: fetch failed` (Supabase)

**Penyebab:** Supabase URL/Key belum benar atau tidak ada koneksi internet.

**Solusi:**
1. Cek `SUPABASE_URL` dan `SUPABASE_KEY` di `config.js`
2. Pastikan koneksi internet aktif
3. Bot tetap berjalan normal menggunakan JSON lokal sebagai fallback

---

### ❌ `signIn is not a function`

**Penyebab:** gramjs v2 tidak punya `client.signIn()`.

**Solusi:** Sudah diperbaiki — bot menggunakan `api.auth.SignIn` dan `api.auth.CheckPassword` secara langsung.

---

### ❌ `Session expired` saat startup

**Penyebab:** String session sudah kedaluwarsa (akun logout dari perangkat lain / password berubah).

**Solusi:** User perlu login ulang via bot. Session lama otomatis dihapus.

---

### ❌ Bot tidak merespons

Cek urutan berikut:
1. `BOT_TOKEN` benar di `config.js`
2. Bot tidak sedang di-block oleh Telegram
3. Tidak ada instance bot lain yang berjalan (konflik polling)
4. Jalankan ulang: `npm start`

---

### ❌ `Akses Ditolak` padahal sudah login

**Penyebab:** User belum ditambahkan ke daftar premium.

**Solusi:** Owner tambahkan User ID via `[👑 Owner Panel] → [➕ Add Premium]`.

---

## 📝 Error Log Umum

| Log | Artinya | Tindakan |
|---|---|---|
| `[DB] Supabase belum dikonfigurasi` | SUPABASE_URL/KEY belum diisi | Isi di config.js atau biarkan (pakai JSON) |
| `[DB] Supabase saveAllSessions error: TypeError: fetch failed` | Gagal konek ke Supabase | Cek URL/KEY, bot tetap jalan via JSON |
| `⚠️ Expired: <userId>` | Session kedaluwarsa | User login ulang |
| `✅ Restored: <userId>` | Session berhasil dipulihkan | Normal |
| `Polling error: ...` | Error koneksi polling bot | Bot akan coba lagi otomatis |

---

## 📄 Lisensi

Proyek ini untuk penggunaan pribadi. Dilarang disebar atau dijual tanpa izin pembuat.

---

*Dokumentasi ini dibuat untuk versi **v2.0.0***

