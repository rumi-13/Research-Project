# A Robust Pixel-Level Interpretability in OCT-based Retinal Disease Classification

Undergraduate dissertation project focused on improving explainability for OCT-based retinal disease classification.

## Authors
- Asgar Rashid — https://github.com/rumi-13
- Faisal Ahmad Malik — https://github.com/faisalmalik01

## Supervisor
- Dr. Tawseef Ahmed Teli

## Research Summary
### Introduction
Deep learning models can classify retinal OCT scans with high accuracy, but standard Grad-CAM explanations are often coarse and unstable. This project improves interpretability by introducing a **Multi-Layer Fused Grad-CAM** framework for OCT-based retinal disease classification.

### Problem Statement
The dissertation addresses three core limitations in prior explainability methods:
- low spatial precision from final-layer-only attribution,
- weak robustness under perturbation,
- limited quantitative validation of explanation quality.

### Proposed Methodology
1. Train/evaluate a ResNet50-based classifier on OCT2017 (CNV, DME, DRUSEN, NORMAL).
2. Generate Grad-CAM maps from three CNN depths (Layer 2, Layer 3, Layer 4).
3. Compute confidence-retention scores by masking each map and re-running inference.
4. Normalize retention scores into per-image fusion weights.
5. Fuse maps into a single heatmap.
6. Evaluate robustness by adding Gaussian noise (σ = 0.007, 0.008, 0.009) and measuring SSIM.

### Results
- Fused Grad-CAM maps are more anatomically focused than standard final-layer Grad-CAM.
- Fused explanations remain more stable under noise across all four classes.
- SSIM gains (Fused vs Standard) increase with noise level, indicating stronger robustness:
  - σ = 0.007: +0.0157 to +0.0196
  - σ = 0.008: +0.0185 to +0.0264
  - σ = 0.009: +0.0233 to +0.0321

### References
- Rashid, A., Malik, F. A. (2024). *A Robust Pixel-Level Interpretability in OCT-based Retinal Disease Classification* (Undergraduate Dissertation).  
  Available in this repository: `/Docs/Research-Dissertation.pdf`
- Selvaraju, R. R., Cogswell, M., Das, A., Vedantam, R., Parikh, D., & Batra, D. (2017). *Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization*. ICCV.

## Repository Structure
- `/Docs/Research-Dissertation.pdf` — full dissertation
- `/retinaloct.model.training.ipynb` — model training workflow
- `/fused.gradcam.ipynb` — fused Grad-CAM and robustness workflow
- `/class_names.json` — class labels (`CNV`, `DME`, `DRUSEN`, `NORMAL`)
- `/requirements.txt` — Python dependencies
- `/Output/` — generated visualizations and SSIM plot

## Example Outputs
### Standard Grad-CAM
![Standard Grad-CAM](Output/standard-gradCam.png)

### Fused Grad-CAM
![Fused Grad-CAM](Output/fused-Cam.png)

### Clean vs Noisy Fused Heatmaps
![Clean vs Noisy Fused](Output/clean_vs_noisy-Fused-Cam.png)

### Noisy Fused Heatmap Example
![Noisy Fused](Output/noisy-fused-cam.png)

### SSIM Robustness Plot
![SSIM Scores](Output/SSIM-Score.png)

## Setup
```bash
python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# .venv\Scripts\activate   # Windows
pip install -r requirements.txt
```

## Reproducibility Notes
- The notebooks are the primary implementation artifacts in this repository.
- Paths/dataset locations may need to be adjusted inside notebook cells before execution.
- Dissertation experiments use OCT2017 class categories: CNV, DME, DRUSEN, NORMAL.

## Limitations and Future Work (as documented in dissertation)
- No expert-annotated pixel-level lesion masks were available for direct clinical overlap scoring.
- Robustness was evaluated with synthetic Gaussian perturbation; broader real-world scanner/domain validation is needed.
- Future work includes multi-center datasets and extending the method to additional architectures.

## Disclaimer
This repository is for academic and research purposes. It is not a clinical diagnostic tool.
