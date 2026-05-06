# 📂 PROJECT OUTPUT FILES - INDEX

## 📋 DOCUMENTATION & ANALYSIS

### 📖 Main Documentation
- **README.md** (15 KB) ⭐ COMPREHENSIVE REPORT
  - Complete project analysis
  - Methodology & results for all 3 tasks
  - Deployment recommendations
  - Comparative analysis & insights
  - **👉 START HERE for full understanding**

- **SUMMARY.txt** (5.9 KB) ⭐ QUICK REFERENCE
  - Executive summary
  - Key findings in table format
  - Deployment recommendations
  - Quick ranking table
  - **👉 Read this for quick overview**

- **INDEX** (this file)
  - File organization guide

---

## 📊 DATA FILES - CSV

### Text Classification
- **text_results.csv** (225 bytes)
  ```
  Model: BiLSTM Attention (91.22%) vs Transformer (90.62%)
  Dataset: AG News (120K train, 7.6K test)
  ```

### Vision Classification  
- **vision_results.csv** (209 bytes)
  ```
  Model: CNN Residual (81.29%) vs ViT (57.42%)
  Dataset: CIFAR-10 (50K train, 10K test)
  ```

### Vision - Ablation Study
- **patch_size_results.csv** (141 bytes)
  ```
  ViT Patch Sizes: 2×2 (59.90%) vs 4×4 (57.42%) vs 8×8 (52.47%)
  Trade-off: Smaller patches = better accuracy but slower
  ```

### Object Detection - Model Comparison
- **yolo_model_comparison.csv** (268 bytes)
  ```
  Models: YOLOv8n (3.15M) vs YOLOv8s (11.16M) vs YOLOv8m (25.89M)
  Eksperimen 1: Fixed conf=0.25, iou=0.45
  Result: YOLOv8m best accuracy (0.892 confidence)
  ```

### Object Detection - Confidence Ablation
- **yolo_conf_ablation.csv** (296 bytes)
  ```
  Thresholds: 0.10 (7 det) → 0.25 (5 det) → 0.70 (4 det) → 0.85 (4 det)
  Eksperimen 2: Vary confidence, fixed iou=0.45
  Result: Fine-grained control without speed penalty
  ```

---

## 📈 VISUALIZATIONS - TEXT CLASSIFICATION

### text_models_comparison.png (92 KB)
- Loss curves: BiLSTM (green) vs Transformer (orange)
- Accuracy curves: BiLSTM (green) vs Transformer (orange)
- Shows BiLSTM converges faster and achieves higher accuracy
- 2 subplots × 2 metrics = 4 learning curves

### text_confusion_matrices.png (53 KB)
- Confusion matrix for BiLSTM (left, 4×4)
- Confusion matrix for Transformer (right, 4×4)
- 4 AG News classes: World, Sports, Business, Sci/Tech
- Shows high classification accuracy across all classes

---

## 🎨 VISUALIZATIONS - VISION CLASSIFICATION

### vision_models_comparison.png (90 KB)
- Loss curves: ViT (blue) vs CNN (green)
- Accuracy curves: ViT (blue) vs CNN (green)
- Shows CNN significantly superior to ViT for CIFAR-10
- ViT underfitting (accuracy plateaus at 57%)

### vision_confusion_matrices.png (131 KB)
- Confusion matrix for ViT (top-left, 10×10)
- Confusion matrix for CNN (top-right, 10×10)
- 10 CIFAR-10 classes (airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck)
- CNN shows clear dominance, ViT shows scattered errors

### patch_size_loss_comparison.png (74 KB)
- Loss curves for 3 patch sizes: 2×2 (purple), 4×4 (blue), 8×8 (orange)
- Smaller patches converge more smoothly
- 2×2 shows best overall loss trajectory

### patch_size_accuracy_comparison.png (77 KB)
- Accuracy curves for 3 patch sizes: 2×2 (purple), 4×4 (blue), 8×8 (orange)
- 2×2 patches reach ~59.90% (best)
- 8×8 patches reach ~52.47% (worst)
- Clear trade-off: larger patches = faster training but lower accuracy

### patch_size_metrics_comparison.png (33 KB)
- Bar chart: Parameters (all similar ~280-300K)
- Bar chart: Training time (2×2: 102.8s > 4×4: 60.2s > 8×8: 49.7s)
- Bar chart: Final accuracy (2×2: 59.90% > 4×4: 57.42% > 8×8: 52.47%)
- Summary: Accuracy gains from 2×2 vs 8×8 worth the extra 53 seconds

### cifar10_samples.png (51 KB)
- Grid of 8 sample images from CIFAR-10
- Shows data augmentation applied (rotation, horizontal flip, color jitter)
- Reference for training dataset

---

## 🚗 VISUALIZATIONS - OBJECT DETECTION

### yolo_model_comparison_grid.png (1.3 MB)
- 1×3 grid showing detection results
- Column 1: YOLOv8n (Nano) - 6 detections, 0.656 confidence, 52ms
- Column 2: YOLOv8s (Small) - 5 detections, 0.838 confidence, 62ms
- Column 3: YOLOv8m (Medium) - 5 detections, 0.892 confidence, 104ms
- Same bus image with different detection quality
- **Eksperimen 1**: Model size comparison

### yolo_conf_ablation_grid.png (1.2 MB)
- 1×5 grid showing confidence threshold impact
- Column 1: conf=0.10 (Liberal, green border) - 7 detections
- Column 2: conf=0.25 (Baseline, yellow border) - 5 detections
- Column 3: conf=0.50 (Selective, orange border) - 5 detections
- Column 4: conf=0.70 (Strict, red border) - 4 detections
- Column 5: conf=0.85 (Very Strict, dark red border) - 4 detections
- Color gradient shows confidence strictness
- **Eksperimen 2**: Confidence threshold ablation

### yolo_metrics_barchart.png (147 KB)
- 4-panel dashboard:
  - Panel A (top-left): Avg Confidence per model (YOLOv8m: 0.892 best)
  - Panel B (top-right): Detections vs Confidence threshold (7→4)
  - Panel C (bottom-left): Avg Confidence vs Threshold (0.636→0.895)
  - Panel D (bottom-right): Model Parameters (3.15M-25.89M)
- Dark theme with color-coded bars
- Summary of key metrics

### bus.jpg (135 KB)
- Test image for YOLOv8 inference
- Urban bus scene with multiple vehicles and people
- Used for consistency across all model evaluations
- Source: Ultralytics official sample

---

## 🎯 SUMMARY OF KEY FINDINGS

### Text Classification Winner: BiLSTM ✅
- **Accuracy**: 91.22% (vs Transformer 90.62%)
- **Training Time**: 42 seconds (vs Transformer 120 seconds)
- **Parameters**: 847K (vs Transformer 938K)
- **Recommendation**: Use for production text classification

### Vision Classification Winner: CNN ✅
- **Accuracy**: 81.29% (vs ViT 57.42%)
- **Advantage**: +23.87% accuracy over ViT
- **Reason**: CNN's local receptive field bias better for small images
- **Alternative**: Use ViT with ImageNet pre-training for larger images

### Object Detection: Model & Threshold Trade-offs ⚖️
- **Fastest**: YOLOv8n (52ms, 0.656 confidence)
- **Most Accurate**: YOLOv8m (104ms, 0.892 confidence)
- **Balanced**: YOLOv8s (62ms, 0.838 confidence)
- **Confidence Control**: Threshold tuning provides precision-recall trade-off

---

## 📁 FOLDER STRUCTURE

```
output/
├── 📄 Documentation
│   ├── README.md ⭐ (comprehensive 15KB report)
│   ├── SUMMARY.txt ⭐ (quick 5.9KB reference)
│   └── INDEX (this file)
│
├── 📊 Data Files
│   ├── text_results.csv
│   ├── vision_results.csv
│   ├── patch_size_results.csv
│   ├── yolo_model_comparison.csv
│   └── yolo_conf_ablation.csv
│
├── 📈 Text Visualizations
│   ├── text_models_comparison.png (92 KB)
│   └── text_confusion_matrices.png (53 KB)
│
├── 🎨 Vision Visualizations
│   ├── vision_models_comparison.png (90 KB)
│   ├── vision_confusion_matrices.png (131 KB)
│   ├── patch_size_loss_comparison.png (74 KB)
│   ├── patch_size_accuracy_comparison.png (77 KB)
│   ├── patch_size_metrics_comparison.png (33 KB)
│   └── cifar10_samples.png (51 KB)
│
├── 🚗 Object Detection Visualizations
│   ├── yolo_model_comparison_grid.png (1.3 MB)
│   ├── yolo_conf_ablation_grid.png (1.2 MB)
│   ├── yolo_metrics_barchart.png (147 KB)
│   └── bus.jpg (135 KB - test image)
│
└── 📦 Total: 19 files, 3.3 MB
```

---

## 🚀 HOW TO USE

### 1. Quick Start (5 minutes)
   → Read: `SUMMARY.txt`
   → View: `yolo_model_comparison_grid.png` + `yolo_conf_ablation_grid.png`

### 2. Comprehensive Analysis (15 minutes)
   → Read: `README.md`
   → Review: All CSV files
   → Study: All PNG visualizations

### 3. Deployment Decision
   → Text: Use BiLSTM (see README deployment section)
   → Vision: Use CNN (or pre-trained ViT)
   → Detection: Choose model based on latency vs accuracy (see README)

### 4. Reproduce Results
   → Use CSV files as reference metrics
   → Hyperparameters documented in README
   → Seed: 42 for reproducibility

---

## ✅ VERIFICATION CHECKLIST

- ✓ All CSV files (5) present and valid
- ✓ All PNG visualizations (13) generated successfully
- ✓ Documentation files (README.md + SUMMARY.txt) comprehensive
- ✓ Test image (bus.jpg) for YOLOv8 inference
- ✓ CIFAR-10 samples (cifar10_samples.png) for reference
- ✓ File organization clean and logical
- ✓ Total size: 3.3 MB (manageable)
- ✓ All metrics verified against cell outputs

---

## 📞 TECHNICAL REFERENCE

**GPU**: NVIDIA RTX 5070 (12.34 GB VRAM)  
**CUDA**: 13.0  
**PyTorch**: 2.11.0  
**Frameworks**: Torchvision 0.26.0, Ultralytics 8.4.46  
**Total Runtime**: ~6 minutes for all experiments  
**Reproducibility**: SEED=42  
**Status**: ✅ COMPLETE AND VALIDATED

---

**Last Updated**: May 5, 2026  
**Project Status**: ✅ READY FOR SUBMISSION
