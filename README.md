# Mikrotik Assistant (RouterOS v6)

Asisten AI untuk MikroTik RouterOS. Anda mengetik prompt, sistem menyarankan command, lalu Anda bisa menyetujui eksekusi. Termasuk Web UI dan bot Telegram.

## Kebutuhan
- RouterOS v6.x (API port 8728/8729)
- Docker (disarankan) atau Python 3.12+
- OpenAI API key

## Mulai Cepat (Docker)

Pull:
```
docker pull raufendro/mikrotik-ai-raufendro:1.0.2
```

Jalankan (webapp + bot Telegram):
```
docker run -d --name mikrotik-ai \
  -p 8000:8000 \
  -e MIKROTIK_ROUTER_HOST=10.1.1.1 \
  -e MIKROTIK_ROUTER_PORT=8728 \
  -e MIKROTIK_ROUTER_USER=admin \
  -e MIKROTIK_ROUTER_PASS=your_password \
  -e OPENAI_API_KEY=sk-... \
  -e TELEGRAM_BOT_TOKEN=123:abc \
  -e TELEGRAM_ALLOWED_CHAT_IDS=1769420825 \
  -e TELEGRAM_AUTO_START=1 \
  raufendro/mikrotik-ai-raufendro:1.0.2
```

Buka Web UI:
```
http://<server-ip>:8000
```

Catatan:
- Ubah port host dengan mengedit `-p HOSTPORT:8000`.
- Router harus bisa dijangkau dari server (jaringan yang sama/VPN).

## Cara Pakai Bot Telegram
1) Kirim prompt ke bot.
2) Bot mengembalikan daftar command yang disarankan.
3) Tekan **Apply** untuk mengeksekusi.

Contoh video chat:
- [![Demo Telegram Bot](https://img.youtube.com/vi/qfm-geXyqE4/0.jpg)](https://youtube.com/shorts/qfm-geXyqE4?si=Ao9VoqLTH81MF0gH)

## Environment Variables

Wajib:
- `MIKROTIK_ROUTER_HOST`
- `MIKROTIK_ROUTER_PORT`
- `MIKROTIK_ROUTER_USER`
- `MIKROTIK_ROUTER_PASS`
- `OPENAI_API_KEY`
- `TELEGRAM_BOT_TOKEN`
- `TELEGRAM_ALLOWED_CHAT_IDS`
- `TELEGRAM_AUTO_START=1`

Penjelasan:

**Router**
- `MIKROTIK_ROUTER_HOST` — IP/host RouterOS.
- `MIKROTIK_ROUTER_PORT` — port API RouterOS (default 8728).
- `MIKROTIK_ROUTER_USER` — username API RouterOS.
- `MIKROTIK_ROUTER_PASS` — password API RouterOS.
- `MIKROTIK_TIMEOUT` — timeout koneksi API (detik).

**OpenAI**
- `OPENAI_API_KEY` — API key OpenAI.
- `OPENAI_MODEL` — model yang dipakai (default `gpt-5.2`).
- `OPENAI_ORG` — ID organisasi (opsional).
- `OPENAI_PROJECT` — ID project (opsional).

**Telegram**
- `TELEGRAM_BOT_TOKEN` — token bot Telegram.
- `TELEGRAM_ALLOWED_CHAT_IDS` — daftar chat ID yang diizinkan (dipisah koma).
- `TELEGRAM_AUTO_START` — `1/true` untuk auto-start bot saat webapp jalan.

## Catatan Keamanan
- Gunakan user MikroTik khusus dengan izin terbatas.
- Jangan membagikan OpenAI API key atau Telegram bot token.
