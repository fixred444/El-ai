# El Ai

Website chat AI berbahasa Indonesia dengan tampilan ala Claude/Gemini: sidebar riwayat obrolan, jawaban streaming, mode gelap/terang, dan render Markdown + blok kode.

Tanpa build step: HTML/CSS/JS statis + satu serverless function (`api/chat.js`) yang menyimpan API key dengan aman di server.

## Struktur

```
index.html, style.css, app.js, markdown.js, favicon.svg   -> tampilan
api/chat.js                                                -> backend (Vercel Function)
vercel.json, package.json                                  -> konfigurasi
```

## Deploy: GitHub -> Vercel

1. Buat repository baru di GitHub, lalu upload semua file proyek ini (atau `git push`).
2. Buka https://vercel.com/new, pilih **Import** repository tadi.
3. Framework Preset: **Other** (biarkan Build Command dan Output Directory kosong).
4. Buka **Environment Variables**, tambahkan:
   - `AI_API_KEY` = API key kamu (wajib)
   - `AI_BASE_URL` = `https://api.z.ai/api/paas/v4` (opsional)
   - `AI_MODEL` = `glm-4.5-flash` (opsional)
5. Klik **Deploy**. Setiap `git push` ke GitHub akan otomatis deploy ulang.

Jika key kamu dari platform bigmodel.cn, isi `AI_BASE_URL` dengan `https://open.bigmodel.cn/api/paas/v4`. Penyedia lain yang kompatibel dengan format OpenAI (`/chat/completions`) juga bisa dipakai dengan mengganti `AI_BASE_URL` dan `AI_MODEL`.

## Jalankan lokal

```bash
npm i -g vercel
cp .env.example .env     # isi AI_API_KEY
vercel dev
```

## Mengubah identitas / jawaban "Apa itu El Ai?"

Edit konstanta `SYSTEM_PROMPT` di `api/chat.js`.

## Keamanan

- Jangan menaruh API key di kode atau commit file `.env`. Key hanya disimpan di Environment Variables Vercel.
- Endpoint `/api/chat` bisa dipanggil siapa saja yang tahu URL-nya, jadi pakai key dengan batas kuota/biaya.
