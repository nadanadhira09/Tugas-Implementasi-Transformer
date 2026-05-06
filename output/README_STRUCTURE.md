# Project Structure

## Root Directory (`/Tugas/pmesin/`)
- `Tugas-Implementasi-Transformer.ipynb` - Main notebook with all experiments
- `data/` - CIFAR-10 dataset (used for training)

## Output Directory (`/Tugas/pmesin/output/`)

### `/results/` - Experiment Results (CSV Files)
- `text_results.csv` - Text classification model comparison
- `vision_results.csv` - Vision classification model comparison  
- `patch_size_results.csv` - ViT patch size ablation study
- `yolo_model_comparison.csv` - YOLO model size comparison
- `yolo_conf_ablation.csv` - YOLO confidence threshold ablation

### `/visualizations/` - Output Images (PNG Files)
**Text Classification:**
- `text_models_comparison.png` - Loss & Accuracy comparison plot
- `text_confusion_matrices.png` - Confusion matrices for text models

**Vision Classification:**
- `vision_models_comparison.png` - Loss & Accuracy comparison plot
- `vision_confusion_matrices.png` - Confusion matrices for vision models
- `cifar10_samples.png` - CIFAR-10 dataset sample images

**ViT Patch Size Analysis:**
- `patch_size_loss_comparison.png` - Loss for different patch sizes
- `patch_size_accuracy_comparison.png` - Accuracy for different patch sizes
- `patch_size_metrics_comparison.png` - Normalized metrics comparison

**YOLO Object Detection:**
- `yolo_model_comparison_grid.png` - Model comparison visualization
- `yolo_conf_ablation_grid.png` - Confidence threshold ablation
- `yolo_metrics_barchart.png` - Metrics summary dashboard
- `yolo_comparison_metrics_barchart.png` - 4-panel comparison chart

### `/models/` - Pretrained YOLO Weights
- `yolov8n.pt` - YOLOv8 Nano (lightweight)
- `yolov8s.pt` - YOLOv8 Small (balanced)
- `yolov8m.pt` - YOLOv8 Medium (high accuracy)

### Documentation Files
- `README.md` - Project overview
- `README_ENGLISH.md` - English version
- `LAPORAN_TUGAS_TRANSFORMER.txt` - Detailed report

