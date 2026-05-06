# 🤖 Implementasi Transformer — Text, Vision & Object Detection

**Nama:** Nada Nadhira Najwa Mazaya  
**NIM:** 256150100111005  
**Institusi:** Program Magister Ilmu Komputer, Fakultas Ilmu Komputer (FILKOM), Universitas Brawijaya

Repositori ini berisi implementasi dan eksperimen **Transformer** dari scratch menggunakan PyTorch, mencakup tiga domain utama: **Text Classification**, **Vision Classification**, dan **Object Detection**. Setiap eksperimen menyertakan model pembanding (baseline) untuk analisis trade-off yang komprehensif.

---

## 📋 Daftar Isi

- [Gambaran Umum](#gambaran-umum)
- [Eksperimen](#eksperimen)
  - [1. Text Classification — AG News](#1-text-classification--ag-news)
  - [2. Vision Classification — CIFAR-10](#2-vision-classification--cifar-10)
  - [3. ViT Patch Size Ablation](#3-vit-patch-size-ablation)
  - [4. Object Detection — YOLOv8](#4-object-detection--yolov8)
- [Hasil & Kesimpulan](#hasil--kesimpulan)
- [Struktur Repo](#struktur-repo)
- [Requirements](#requirements)

---

## Gambaran Umum

| Domain | Dataset | Model Utama | Model Pembanding |
|--------|---------|-------------|------------------|
| Text Classification | AG News (4 kelas) | Transformer Encoder | BiLSTM + Attention, BiLSTM |
| Vision Classification | CIFAR-10 (10 kelas) | Vision Transformer (ViT) | CNN Residual, DenseNet |
| ViT Ablation | CIFAR-10 | ViT (patch 2×2, 4×4, 8×8) | — |
| Object Detection | Custom image | YOLOv8n / s / m | Confidence Threshold Ablation |

---

## Eksperimen

### 1. Text Classification — AG News

Dataset **AG News** berisi 120.000 artikel berita dari 4 kategori: *World, Sports, Business, Sci/Tech*.

**Pipeline:**
- Tokenisasi sederhana (lowercase, hapus punctuation)
- Vocabulary 5.000 token teratas
- Padding / truncation ke panjang maksimum 256 token
- Batch size: 32

**Model:**

| Model | Arsitektur |
|-------|-----------|
| **Transformer** | Embedding → Positional Encoding → Transformer Encoder (2 layer, 8 head) → Mean Pooling → Linear |
| **BiLSTM + Attention** | Embedding → BiLSTM (2 layer, hidden=64) → Custom Attention → FC |
| **BiLSTM** | Embedding → BiLSTM (2 layer) → Last Hidden → FC |

---

### 2. Vision Classification — CIFAR-10

Dataset **CIFAR-10** berisi 60.000 gambar 32×32 piksel dari 10 kelas.

**Model:**

| Model | Arsitektur |
|-------|-----------|
| **ViT** | Patch Embedding (4×4) → Positional Encoding → Transformer Encoder → CLS Token → Linear |
| **CNN Residual** | Conv → BatchNorm → ReLU → Residual Blocks → Adaptive Pooling → FC |
| **DenseNet** | DenseBlock + Transition Layers → Global AvgPool → FC |

---

### 3. ViT Patch Size Ablation

Eksplorasi pengaruh ukuran patch terhadap akurasi ViT pada CIFAR-10:

| Patch Size | Jumlah Patches |
|------------|---------------|
| 2×2 | 256 patches |
| 4×4 | 64 patches |
| 8×8 | 16 patches |

---

### 4. Object Detection — YOLOv8

Dua sub-eksperimen menggunakan **Ultralytics YOLOv8**:

**Eksperimen A — Model Size Comparison** (`conf=0.25, iou=0.45`):

| Model | Parameter |
|-------|-----------|
| YOLOv8n (Nano) | 3.15M |
| YOLOv8s (Small) | 11.16M |
| YOLOv8m (Medium) | 25.89M |

**Eksperimen B — Confidence Threshold Ablation** (YOLOv8s, `iou=0.45`):  
Nilai conf yang diuji: `0.10 · 0.25 · 0.50 · 0.70 · 0.85`

---

## Hasil & Kesimpulan

### 📊 Text Classification

| Model | Accuracy | Waktu Training |
|-------|----------|---------------|
| Transformer Encoder | 90.66% | 189.36s |
| **BiLSTM + Attention** ⭐ | **91.18%** | 101.42s |
| BiLSTM Bidirectional | 91.14% | 92.85s |

> **Kesimpulan:** BiLSTM + Attention unggul untuk klasifikasi teks pendek (≤256 token). Transformer membutuhkan data yang jauh lebih besar untuk mencapai potensi penuhnya.

---

### 📊 Vision Classification

| Model | Accuracy | Waktu Training |
|-------|----------|---------------|
| ViT (patch 4×4) | 56.58% | 104.25s |
| **CNN Residual** ⭐ | **81.14%** | 156.35s |
| DenseNet | 76.24% | 140.82s |

> **Kesimpulan:** CNN Residual jauh lebih unggul untuk gambar kecil (32×32). ViT dirancang untuk resolusi tinggi (≥224×224) dan data yang sangat besar.

---

### 📊 ViT Patch Size Ablation

| Patch Size | Accuracy |
|------------|----------|
| 2×2 (256 patches) | 59.90% |
| 4×4 (64 patches) | 56.58% |
| 8×8 (16 patches) | 52.47% |

> **Kesimpulan:** Patch lebih kecil menghasilkan akurasi lebih tinggi, namun ViT tetap tidak mampu menyaingi CNN pada dataset resolusi rendah.

---

### 📊 Object Detection — YOLOv8

**Model Size Trade-off:**
- **YOLOv8n** → Tercepat, cocok untuk edge devices
- **YOLOv8s** → Seimbang antara kecepatan dan akurasi
- **YOLOv8m** → Akurasi terbaik, rekomendasi untuk production ⭐

**Confidence Threshold Recommendations:**

| Use Case | Model | Conf |
|----------|-------|------|
| Production (akurasi) | YOLOv8m | ≥ 0.50 |
| Edge / realtime | YOLOv8n | 0.25 |
| Safety-critical | YOLOv8m | ≥ 0.70 |
| Research / max recall | YOLOv8s | 0.10 |

---

### 🔑 Key Findings

1. Transformer **tidak optimal** untuk teks pendek tanpa pretraining skala besar
2. CNN masih **jauh lebih baik** dari ViT untuk gambar resolusi 32×32
3. BiLSTM + Attention terbukti **terbaik** untuk klasifikasi teks di dataset ini
4. ViT membutuhkan gambar **≥224×224** untuk performa optimal
5. **Confidence threshold** sangat kritis dalam deployment YOLO
6. **Trade-off model size** harus disesuaikan dengan kebutuhan deployment

---

## Struktur Repo

```
📦 Tugas-Implementasi-Transformer/
├── 📓 Tugas-Implementasi-Transformer.ipynb   # Notebook utama
├── 📄 README.md
│
├── 📂 outputs/                               # Hasil eksperimen (dihasilkan saat run)
│   ├── text_results.csv
│   ├── vision_results.csv
│   ├── patch_size_results.csv
│   ├── yolo_model_comparison.csv
│   ├── yolo_conf_ablation.csv
│   ├── text_models_comparison.png
│   ├── text_confusion_matrices.png
│   ├── vision_models_comparison.png
│   ├── vision_confusion_matrices.png
│   ├── cifar10_samples.png
│   ├── patch_size_*.png
│   ├── yolo_model_comparison_grid.png
│   ├── yolo_conf_ablation_grid.png
│   └── yolo_metrics_barchart.png
```

---

## Requirements

```
torch >= 2.0
torchvision >= 0.15
datasets
scikit-learn
matplotlib
seaborn
pandas
numpy
ultralytics
```

---

<div align="center">
  <sub>Dibuat untuk keperluan akademis · Deep Learning · 2025</sub>
</div>
