# PRMS Auto Attendance 🚀

Otomatisasi Presensi (Check-in & Check-out) PRMS dengan Dukungan Jadwal Cron, Notifikasi Telegram Bot, dan Docker.

---

## 📋 Fitur Utama

- ⏰ **Otomatisasi Jadwal Presensi**:
  - **Pre-Login**: 07:00 WIB (Simpan token otentikasi)
  - **Check-in**: 07:50 WIB (Jadwal Senin–Jumat, dengan random delay 0–20 menit)
  - **Check-out**: 17:30 WIB (Jadwal Senin–Jumat, dengan random delay 0–30 menit)
- 🤖 **Integrasi Telegram Bot**:
  - Notifikasi real-time saat check-in, check-out, atau ada error.
  - Perintah manual via chat Telegram (`/checkin`, `/checkout`, `/status`, dll).
- 🐳 **Docker Support**: Dilengkapi `Dockerfile` untuk deployment cepat & terisolasi di VPS.
- ⚡ **Health Check Server**: Built-in HTTP server ringan untuk cloud platform health checking.

---

## 🛠️ Persyaratan Sistem

- Node.js `>=18.0.0`
- Docker (opsional, direkomendasikan untuk deployment di VPS)

---

## ⚙️ Konfigurasi Environment (`.env`)

Buat file `.env` di root direktori aplikasi (salin dari `.env.example`):

```bash
cp .env.example .env
```

Isi variabel environment berikut:

```env
# URL API PRMS
API_BASE=https://prms-api.fid-app.my.id/api

# Kredensial Akun PRMS
EMAIL=email_anda@example.com
PASSWORD=password_prms_anda

# Lokasi Koordinat Presensi
BASE_LATITUDE=-6.159868350846804
BASE_LONGITUDE=106.87936991839877

# Catatan/Keterangan Presensi
NOTE=Standby POC AURORA

# Timezone (Wajib untuk jadwal cron)
TZ=Asia/Jakarta

# Konfigurasi Telegram Bot (Opsional)
TELEGRAM_BOT_TOKEN=token_bot_telegram_anda
TELEGRAM_CHAT_ID=chat_id_telegram_anda
```

---

## 🚀 Cara Menjalankan (Lokal)

1. **Install Dependencies**:
   ```bash
   npm install
   ```

2. **Jalankan Aplikasi**:
   ```bash
   npm start
   ```

---

## 🐳 Deployment di VPS (Dengan Docker)

Rekomendasi terbaik untuk menjalankan aplikasi 24/7 di VPS (seperti Tencent Cloud, DigitalOcean, IDCloudHost, dll):

1. **Clone Repository**:
   ```bash
   git clone https://github.com/rakazidan/attendance-automation.git
   cd attendance-automation
   ```

2. **Buat File `.env`**:
   ```bash
   nano .env
   # Isi dengan variabel yang sesuai
   ```

3. **Build & Run Docker Container**:
   ```bash
   sudo docker build -t prms-bot .
   sudo docker run -d \
     --name prms-bot \
     --restart always \
     --env-file .env \
     -p 3000:3000 \
     prms-bot
   ```

4. **Cek Monitoring & Log**:
   ```bash
   # Cek status container
   sudo docker ps

   # Cek log bot real-time
   sudo docker logs -f prms-bot
   ```

---

## 📜 Lisensi

[MIT License](LICENSE)
