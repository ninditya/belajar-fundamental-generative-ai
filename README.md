# 🎨 Generative Image Suite, Submission BFGAI

> **Belajar Fundamental Generative AI | Dicoding Indonesia**
> Submission Project: Image Generation with Stable Diffusion

---

## 📋 Daftar Isi

- [What, Apa Itu Proyek Ini?](#what--apa-itu-proyek-ini)
- [Who, Untuk Siapa?](#who--untuk-siapa)
- [Why, Mengapa Proyek Ini Dibuat?](#why--mengapa-proyek-ini-dibuat)
- [Where, Di Mana Proyek Ini Berjalan?](#where--di-mana-proyek-ini-berjalan)
- [When, Kapan Proyek Ini Dibuat?](#when--kapan-proyek-ini-dibuat)
- [How, Bagaimana Cara Kerjanya?](#how--bagaimana-cara-kerjanya)
- [Struktur File](#struktur-file)
- [Hasil Eksperimen](#hasil-eksperimen)
- [Cara Menjalankan](#cara-menjalankan)
- [Kriteria Penilaian](#kriteria-penilaian)

---

## What, Apa Itu Proyek Ini?

**Generative Image Suite** adalah aplikasi *end-to-end* berbasis **Stable Diffusion v1.5** yang mampu:

| Fitur | Deskripsi |
|-------|-----------|
| 🖼️ **Text-to-Image** | Menghasilkan gambar dari teks (prompt) menggunakan pipeline Stable Diffusion |
| 🎛️ **Hyperparameter Tuning** | Eksperimen guidance scale, inference steps, scheduler |
| 🔲 **Batch Inference** | Generate 1–4 gambar sekaligus dalam grid 2×2 |
| ✏️ **Inpainting** | Modifikasi area spesifik gambar menggunakan mask manual maupun otomatis (CLIPSeg) |
| 🔭 **Outpainting** | Memperluas kanvas gambar ke satu arah atau zoom-out bertahap ke semua arah |
| 🖥️ **Streamlit Interface** | Antarmuka web interaktif yang dapat diakses via browser menggunakan Ngrok |

Proyek ini terbagi menjadi **dua notebook**:
1. **Pipeline Notebook**, eksperimen teknis mendalam dengan Stable Diffusion
2. **Streamlit Notebook**, membangun antarmuka web interaktif dengan `logic.py` + `app.py`

---

## Who, Untuk Siapa?

| Pihak | Peran |
|-------|-------|
| **Pemilik Proyek** | Ninditya (Siswa Belajar Fundamental Generative AI, Dicoding) |
| **Reviewer** | Tim Reviewer Dicoding Indonesia |
| **Target Pengguna** | Siapa pun yang ingin menggunakan aplikasi Generative AI berbasis browser tanpa coding |

Proyek ini ditujukan untuk **siswa** yang sedang belajar konsep Generative AI secara praktis dengan pendekatan *engineering-oriented*, tidak hanya menjadi pengguna, tetapi memahami cara kerja model di balik layar.

---

## Why, Mengapa Proyek Ini Dibuat?

### Tujuan Pembelajaran
- Memahami cara kerja **Diffusion Model** secara teknis (bukan sekadar pengguna)
- Mempraktikkan konfigurasi pipeline Stable Diffusion: seed, scheduler, guidance scale, inference steps
- Menguasai teknik manipulasi gambar: **inpainting** (edit area) dan **outpainting** (perluasan kanvas)
- Membangun solusi Generative AI **end-to-end** dalam bentuk aplikasi nyata

### Nilai Teknis
- Menggunakan model terbuka (`runwayml/stable-diffusion-v1-5`) yang dapat dikontrol penuh
- Menerapkan **Two-Stage Refiner Pattern** untuk kualitas gambar lebih tinggi
- Mengintegrasikan **CLIPSeg** untuk automasking berbasis teks
- Memanfaatkan **Ngrok** sebagai tunnel publik agar aplikasi bisa diakses dari internet

---

## Where, Di Mana Proyek Ini Berjalan?

### Environment
| Komponen | Spesifikasi |
|----------|-------------|
| **Platform** | Google Colab (disarankan) / Kaggle |
| **GPU** | T4 GPU (free tier) |
| **Runtime** | Python 3.10+ |
| **Framework** | PyTorch + Hugging Face Diffusers |

### Akses Aplikasi
- Aplikasi Streamlit berjalan secara lokal di **port 8501**
- Diekspos ke internet menggunakan **Ngrok tunnel** → URL publik dapat dibagikan

### Model yang Digunakan
| Model | Fungsi |
|-------|--------|
| `runwayml/stable-diffusion-v1-5` | Text-to-Image generation |
| `runwayml/stable-diffusion-inpainting` | Inpainting & Outpainting |
| `CIDAS/clipseg-rd64-refined` | Automasking berbasis teks (CLIPSeg) |

---

## When, Kapan Proyek Ini Dibuat?

| Milestone | Waktu |
|-----------|-------|
| Pembuatan proyek | Mei 2025 |
| Penyelesaian Pipeline Notebook | Mei 2025 |
| Penyelesaian Streamlit Notebook | Mei 2025 |
| Submission ke Dicoding | Mei 2025 |

---

## How, Bagaimana Cara Kerjanya?

### Arsitektur Sistem

```
┌─────────────────────────────────────────────────┐
│              Google Colab (GPU T4)               │
│                                                  │
│  ┌──────────────────────────────────────────┐   │
│  │           logic.py                       │   │
│  │  ┌─────────────────────────────────────┐ │   │
│  │  │  load_models_cached()               │ │   │
│  │  │  generate_image()  → SD v1.5        │ │   │
│  │  │  flush_memory()    → gc + CUDA      │ │   │
│  │  │  set_scheduler()   → Euler/DPM/DDIM │ │   │
│  │  │  run_inpainting()  → SD Inpainting  │ │   │
│  │  │  prepare_outpainting() → Canvas     │ │   │
│  │  └─────────────────────────────────────┘ │   │
│  └──────────────────────────────────────────┘   │
│                      ↕ import                    │
│  ┌──────────────────────────────────────────┐   │
│  │           app.py (Streamlit UI)          │   │
│  │  ┌──────────────┐  ┌──────────────────┐ │   │
│  │  │ ✨ GENERATE  │  │    🛠️ EDIT      │ │   │
│  │  │  - Prompt    │  │  - Inpainting    │ │   │
│  │  │  - Neg Prompt│  │  - Outpainting   │ │   │
│  │  │  - Scheduler │  │  - Zoom Out      │ │   │
│  │  │  - CFG Scale │  │  - Canvas Draw   │ │   │
│  │  │  - Steps     │  │                  │ │   │
│  │  │  - Batch     │  │                  │ │   │
│  │  └──────────────┘  └──────────────────┘ │   │
│  └──────────────────────────────────────────┘   │
│                      ↕ port 8501                 │
│  ┌──────────────────────────────────────────┐   │
│  │         Ngrok Tunnel (Public URL)        │   │
│  └──────────────────────────────────────────┘   │
└─────────────────────────────────────────────────┘
```

### Alur Kerja Pipeline Notebook

```
1. Load SD v1.5 Pipeline
         ↓
2. generate_simple_image()     ← Basic: prompt + neg_prompt + seed
         ↓
3. generate_advanced_image()   ← + guidance_scale + num_inference_steps
         ↓
4. Guidance Scale Experiment   ← [2.0, 7.5, 15.0]
         ↓
5. Inference Steps Experiment  ← [5, 15, 50]
         ↓
6. Batch Inference (2×2 grid)  ← num_images_per_prompt=4
         ↓
7. Scheduler Comparison        ← Euler A | DPM++ | DDIM
         ↓
8. Two-Stage Refiner           ← denoising_end=0.8 → denoising_start=0.8
         ↓
9. Load SD Inpainting Pipeline
         ↓
10. Manual Masking (hardcode)  ← trial & error, seed=9
         ↓
11. CLIPSeg Automasking        ← text-prompted segmentation
         ↓
12. Outpainting (1 direction)  ← prepare_outpainting(direction)
         ↓
13. Zoom Out (multi-step)      ← expand ke semua arah bertahap
```

### Detail Fungsi Kunci

#### `generate_simple_image()`, Basic
```python
def generate_simple_image(prompt, negative_prompt, seed):
    generator = torch.Generator(device=device).manual_seed(seed)
    image = pipe(
        prompt=prompt,
        negative_prompt=negative_prompt,
        generator=generator,
    ).images[0]
    return image
```

#### `generate_advanced_image()`, Skilled
```python
def generate_advanced_image(prompt, negative_prompt, seed,
                            guidance_scale=7.5, num_inference_steps=50):
    generator = torch.Generator(device=device).manual_seed(seed)
    image = pipe(
        prompt=prompt,
        negative_prompt=negative_prompt,
        generator=generator,
        guidance_scale=guidance_scale,
        num_inference_steps=num_inference_steps,
    ).images[0]
    return image
```

#### `load_scheduler()`, Advanced
```python
def load_scheduler(pipe, scheduler_name):
    if scheduler_name == 'Euler A':
        pipe.scheduler = EulerAncestralDiscreteScheduler.from_config(...)
    elif scheduler_name == 'DPM++':
        pipe.scheduler = DPMSolverMultistepScheduler.from_config(...)
    elif scheduler_name == 'DDIM':
        pipe.scheduler = DDIMScheduler.from_config(...)
    return pipe
```

#### `inpaint_engine()`, Kriteria 2
```python
def inpaint_engine(image, mask, prompt, negative_prompt, seed):
    result = inpaint_pipe(
        prompt=prompt,
        negative_prompt=negative_prompt,
        image=image,
        mask_image=mask,
        generator=torch.Generator(device=device).manual_seed(seed),
    ).images[0]
    return result
```

---

## Struktur File

```
submission-generative-AI/
│
├── 📓 Pipeline_submission_BFGAI_Nama-siswa.ipynb   # Notebook eksperimen
├── 📓 Streamlit_submission_BFGAI_Nama-siswa.ipynb  # Notebook Streamlit app
├── 📄 requirements.txt                             # Dependensi Python
├── 📝 README.md                                    # Dokumentasi proyek (file ini)
│
├── 🖼️ basic_comparison.png            # Hasil simple vs advanced image
├── 🖼️ guidance_scale_comparison.png   # Perbandingan guidance scale [2.0, 7.5, 15.0]
├── 🖼️ inference_steps_comparison.png  # Perbandingan steps [5, 15, 50]
├── 🖼️ batch_inference_2x2.png         # Grid 2×2 hasil batch inference
├── 🖼️ scheduler_comparison.png        # Euler A vs DPM++ vs DDIM
├── 🖼️ two_stage_generation.png        # Hasil Base + Refiner pattern
├── 🖼️ inpainting_manual.png           # Hasil inpainting mask manual
├── 🖼️ clipseg_automasking.png         # Hasil CLIPSeg automasking
├── 🖼️ inpainting_auto_vs_manual.png   # Perbandingan manual vs auto mask
├── 🖼️ outpainting_result.png          # Hasil outpainting 1 arah
└── 🖼️ zoom_out_result.png             # Hasil zoom-out multi-step
```

### Arsitektur Streamlit Notebook

```
Streamlit_submission_BFGAI_Nama-siswa.ipynb
│
├── Cell 1  [markdown] # Penting, instruksi pengerjaan
├── Cell 2  [markdown] # Prepare Dependencies
├── Cell 3  [code]     !pip install dependencies
├── Cell 4  [code]     import pyngrok, subprocess
├── Cell 5  [markdown] # Streamlit
├── Cell 6  [markdown] ## logic.py (Basic)
├── Cell 7  [code]     %%writefile logic.py       ← model loader + stubs
├── Cell 8  [code]     %%writefile -a logic.py    ← generate_image() Basic
├── Cell 9  [markdown] ## logic.py (Skilled)
├── Cell 10 [code]     %%writefile -a logic.py    ← flush_memory() + set_scheduler() + generate_image() batch
├── Cell 11 [markdown] ## logic.py (Advanced)
├── Cell 12 [code]     %%writefile -a logic.py    ← run_inpainting() + prepare_outpainting()
├── Cell 13 [markdown] ## app.py, TIDAK perlu diubah
├── Cell 14 [code]     %%writefile app.py         ← UI Streamlit lengkap (StudioAI)
├── Cell 15 [markdown] # Menggunakan Ngrok
├── Cell 16 [markdown] ## Konfigurasi Ngrok
├── Cell 17 [code]     auth_token + subprocess.Popen(streamlit run app.py)
├── Cell 18 [markdown] ## Membuat Public URL
├── Cell 19 [code]     public_url = ngrok.connect(8501).public_url
├── Cell 20 [markdown] Catatan limit Ngrok
├── Cell 21 [markdown] ## Menutup Semua Tunnel
└── Cell 22 [code]     ngrok.kill()
```

---

## Hasil Eksperimen

### Kriteria 1: Text-to-Image

**Prompt yang digunakan:**
```
an astronaut in white space suit standing on the surface of mars,
earth visible in background sky, red rocky martian terrain,
starry dark space, science fiction, digital illustration, concept art
```

**Negative Prompt:**
```
photorealistic, realistic, photograph, 3d render, messy, blurry,
low quality, bad art, ugly, sketch, grainy, unfinished, chromatic aberration
```

#### Guidance Scale Comparison (seed=222)
| Scale | Karakteristik |
|-------|--------------|
| **2.0** (Rendah) | Gambar kurang terfokus, model lebih bebas mengeksplorasi ruang latent. Detail kabur, variasi visual tinggi. Elemen tidak selalu mengikuti deskripsi prompt. |
| **7.5** (Sedang) | Keseimbangan optimal antara kreativitas dan kesesuaian prompt. Detail astronaut dan Mars jelas dan konsisten. |
| **15.0** (Tinggi) | Gambar sangat patuh pada prompt, warna lebih saturasi. Berisiko over-sharpening dan artefak pada tepian objek. |

#### Inference Steps Comparison (seed=222)
| Steps | Karakteristik |
|-------|--------------|
| **5** (Rendah) | Sangat kasar, penuh noise, sulit dikenali. Denoising terlalu singkat untuk membentuk struktur koheren. |
| **15** (Sedang) | Struktur mulai terbentuk, detail masih kasar. Cocok untuk preview cepat. |
| **50** (Tinggi) | Gambar bersih, detail halus, stabilitas visual tinggi. Ideal untuk output final. |

#### Scheduler Comparison (seed=222, steps=30)
| Scheduler | Karakteristik |
|-----------|--------------|
| **Euler A** | Stochastic ancestral sampling, lebih kreatif dan organik. Tekstur kaya, variasi tinggi antar run. |
| **DPM++** | Deterministik dengan solver ODE efisien. Kualitas tinggi dengan step lebih sedikit, detail tajam dan konsisten. |
| **DDIM** | Klasik dan deterministik. Hasil konsisten, cocok untuk interpolasi latent. Kualitas sedikit di bawah DPM++ pada step rendah. |

### Kriteria 2: Inpainting & Outpainting

| Teknik | Detail |
|--------|--------|
| **Manual Masking** | Area mask ditentukan hardcode (trial & error), sisi kanan gambar untuk broken satellite, seed=9 |
| **CLIPSeg Automasking** | Mask otomatis berbasis teks menggunakan model `CIDAS/clipseg-rd64-refined` |
| **Outpainting** | Perluasan kanvas ke satu arah (right/left/up/down), 256px |
| **Zoom Out** | Ekspansi bertahap ke semua arah, 3 steps × 80px per step |
| **Two-Stage Refiner** | Stage 1: `denoising_end=0.8` → Stage 2: `StableDiffusionImg2ImgPipeline` `denoising_start=0.8` |

---

## Cara Menjalankan

### Prerequisites
```bash
pip install -r requirements.txt
```

### Menjalankan di Google Colab (Disarankan)

1. **Upload** kedua file `.ipynb` ke Google Colab
2. **Aktifkan GPU**: Runtime → Change runtime type → **T4 GPU**
3. **Jalankan Pipeline Notebook** terlebih dahulu untuk eksperimen
4. **Jalankan Streamlit Notebook**:
   - Jalankan semua cell `%%writefile logic.py` (Basic → Skilled → Advanced)
   - Jalankan cell `%%writefile app.py` (tidak perlu diubah)
   - **Ganti** `YOUR_AUTHENTICATION_KEY` dengan Ngrok Auth Token Anda
   - Jalankan cell Ngrok → copy public URL → buka di browser

### Mendapatkan Ngrok Auth Token

1. Kunjungi [ngrok.com](https://ngrok.com) dan daftar/login
2. Buka menu **Your Authtoken**
3. Copy token dan paste di cell:
   ```python
   auth_token = "PASTE_TOKEN_ANDA_DI_SINI"
   ```

### Requirements

```
diffusers==0.27.2
transformers==4.40.0
accelerate==0.30.0
safetensors>=0.4.3
torch>=2.0.0
torchvision>=0.15.0
Pillow>=9.5.0
numpy>=1.23.0
matplotlib>=3.7.0
streamlit>=1.33.0
streamlit-drawable-canvas>=0.9.3
pyngrok>=7.0.0
```

---

## 🛡️ Model & Library yang Digunakan

| Library | Versi | Fungsi |
|---------|-------|--------|
| `diffusers` | 0.27.2 | Pipeline Stable Diffusion |
| `transformers` | 4.40.0 | CLIPSeg segmentation model |
| `torch` | ≥2.0.0 | Deep learning framework |
| `streamlit` | ≥1.33.0 | Web interface framework |
| `streamlit-drawable-canvas` | 0.8.0 | Canvas interaktif untuk mask |
| `pyngrok` | ≥7.0.0 | Ngrok tunnel untuk public URL |
| `Pillow` | ≥9.5.0 | Manipulasi gambar |

---

*Dibuat untuk submission Belajar Fundamental Generative AI, Dicoding Indonesia, 2025*
