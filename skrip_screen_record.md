# Skrip Screen Record, Generative Image Suite
# Durasi Target: 3-5 Menit

---

## PERSIAPAN SEBELUM RECORD

- Pastikan Streamlit sudah berjalan dan URL Ngrok sudah terbuka di browser
- Buka browser fullscreen (Chrome/Firefox), tab pada URL ngrok
- Resolusi minimal 1280x720
- Mulai rekam layar (OBS / Loom / built-in screen recorder)

---

## [00:00 - 00:20] OPENING, Tampilan Awal Aplikasi

**Yang dilakukan:**
Tunjukkan tampilan awal aplikasi di browser.

**Yang diucapkan / diketik di teks (jika perlu):**
> Ini adalah StudioAI, aplikasi web berbasis Streamlit untuk Text-to-Image generation,
> Inpainting, dan Outpainting menggunakan Stable Diffusion v1.5.

**Aksi:**
- Tunjukkan judul aplikasi "StudioAI: Craeating Amazing Paint with Stable Diffusion"
- Tunjukkan sidebar di kiri berisi parameter
- Tunjukkan dua tab: "GENERATE" dan "EDIT"

---

## [00:20 - 01:30] TAB GENERATE, TEXT-TO-IMAGE

**Yang dilakukan:**
Demonstrasikan fitur generate gambar di tab GENERATE.

### Langkah 1, Atur Parameter di Sidebar
- Tunjukkan slider **Quality Steps** (geser ke 30)
- Tunjukkan slider **Creativity (CFG)** (biarkan 7.5)
- Tunjukkan **Seed Control** (biarkan 42)
- Tunjukkan dropdown **Scheduler** (pilih "DPM++")
- Tunjukkan slider **Batch Size (Jumlah Gambar)** (biarkan 1)

### Langkah 2, Generate 1 Gambar
- Klik tab **"GENERATE"**
- Tunjukkan text area **Prompt** (isi atau gunakan default)
- Tunjukkan text input **Negative Prompt**
- Klik tombol **"Initialize Generation"**
- Tunggu spinner "Processing Image" selesai
- Tunjukkan gambar hasil yang muncul di panel "Visual Output"

### Langkah 3, Batch Generation (Grid 2x2)
- Di sidebar, geser **Batch Size (Jumlah Gambar)** menjadi **4**
- Klik **"Initialize Generation"** lagi
- Tunggu hingga selesai
- Tunjukkan **grid 2x2** dengan 4 gambar yang muncul
- Tunjukkan tombol "Select Img 1", "Select Img 2", dst untuk memilih gambar

### Langkah 4, Flush RAM
- Klik tombol **"Flush RAM"** di sidebar
- Tunjukkan toast "Memory Cleared!" yang muncul

---

## [01:30 - 02:30] TAB EDIT, INPAINTING

**Yang dilakukan:**
Demonstrasikan fitur Inpainting dengan canvas mask.

### Langkah 1, Pilih Gambar untuk Diedit
- Klik tab **"EDIT"**
- Gambar dari generate sebelumnya otomatis tersedia
- Pastikan radio button **"Inpainting (Edit Objek)"** terpilih

### Langkah 2, Gambar Mask di Canvas
- Tunjukkan section **"Draw Mask"** dengan gambar sebagai background canvas
- Gunakan mouse untuk **menggambar area putih** di bagian gambar yang ingin diubah
- Gambar beberapa goresan membentuk area yang akan di-replace

### Langkah 3, Isi Prompt & Generate
- Di panel kanan tunjukkan text input **"Prompt Baru (Ganti jadi apa?)"**
- Isi dengan deskripsi objek baru yang diinginkan
- Tunjukkan slider **Strength**
- Klik tombol **"Execute Inpainting"**
- Tunggu spinner "Processing Inpainting..." selesai
- Tunjukkan hasil inpainting yang muncul

---

## [02:30 - 03:30] TAB EDIT, OUTPAINTING

**Yang dilakukan:**
Demonstrasikan fitur Outpainting Zoom Out.

### Langkah 1, Pilih Mode Outpainting
- Masih di tab **"EDIT"**
- Klik radio button **"Outpainting (Zoom Out)"**
- Tunjukkan gambar saat ini di panel "Original"

### Langkah 2, Zoom Out
- Tunjukkan info "Gambar akan diperluas 128px ke segala arah"
- Isi atau gunakan default **Prompt Deskriptif**
- Klik tombol **"Zoom Out (Expand)"**
- Tunggu spinner "Expanding Canvas..." selesai
- Tunjukkan hasil gambar yang diperluas ke semua arah

---

## [03:30 - 04:00] CLOSING

**Yang dilakukan:**
Kembali ke tab GENERATE untuk menunjukkan fitur scheduler.

- Klik tab **"GENERATE"**
- Di sidebar ubah **Scheduler** ke **"DDIM"**
- Pastikan **Batch Size** kembali ke 1
- Klik **"Initialize Generation"**
- Tunjukkan hasilnya
- Zoom out browser sedikit agar seluruh layout terlihat
- Berhenti rekam

---

## TIPS RECORDING

- Gerakkan kursor secara perlahan saat menunjuk elemen UI
- Saat menunggu spinner, tetap tunjukkan layar (jangan minimize)
- Jika ada error, refresh halaman dan coba lagi sebelum recording
- Simpan video dalam format `.mp4` (H.264 codec)
- Nama file: `video_demo_aplikasi_BFGAI.mp4`

---

## CHECKLIST SEBELUM SUBMIT

- [ ] Notebook Pipeline sudah dijalankan penuh di Colab (ada output di semua cell)
- [ ] Notebook Streamlit sudah dijalankan dan URL Ngrok aktif
- [ ] Token ngrok dikembalikan ke "YOUR_AUTHENTICATION_KEY" sebelum submit
- [ ] Video screen record tersimpan sebagai `video_demo_aplikasi_BFGAI.mp4`
- [ ] Semua file ada dalam 1 folder:
  - `Pipeline_submission_BFGAI_Ninditya-Salma-Nur-Aini.ipynb`
  - `Streamlit_submission_BFGAI_Ninditya-Salma-Nur-Aini.ipynb`
  - `video_demo_aplikasi_BFGAI.mp4`
  - `requirements.txt`
- [ ] Folder di-zip dan siap diupload ke Dicoding
