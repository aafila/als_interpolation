# A Novel Framework for Efficient Reconstruction of Occluded Terrains Using Geometric Analysis and Iterative Plane Fitting

Authors:
- Amiraslan Fila (Corresponding Author; email: afila@student.unimelb.edu.au), Department of Infrastructure Engineering, The University of Melbourne, Melbourne, Victoria 3053, Australia.
- A/Prof Jagannath Aryal, Department of Infrastructure Engineering, The University of Melbourne, Melbourne, Victoria 3053, Australia.
- Prof Abbas Rajabifard, Department of Infrastructure Engineering, The University of Melbourne, Melbourne, Victoria 3053, Australia.

This project presents a reproducible framework for reconstructing occluded ground surfaces in aerial LiDAR data using:
- **2D iterative line fitting**, as proof of concept and  
- **3D iterative plane fitting**.

Each approach iteratively fits geometries from both sides of a void (missing region), extrapolates into the interior, samples jittered points on the extended front, and evaluates the estimated surface against known ground truth using ANOVA on RMSE, Tukey's HSD pari-wise comparison, and compute time.

---

## 📁 Project Structure

```
project/
├── data/
│   ├── S7_1.laz                          # Test LAZ file from OpenGF (ground-only filtered)
│   ├── 20250528_30x_voids.csv           # 30 rectangular voids (coordinates)
│   ├── 20250530_RMSE_Runs_all_methods_both_axes.csv    # RMSE values across methods and axes (use for reproducibility)
│   ├── 20250528_selected_methods_compute_time.csv # Timing for 4 selected methods (use for reproducibility
├── notebooks/
│   ├── 2D_void_reconstruction.ipynb   # 2D jittered line fitting
│   ├── 3D_void_reconstruction.ipynb  # 3D plane fitting and surface interpolatino
├── outputs/
│   ├── visualisations/                             # method plots
│   ├── 20250530_anova_for_accuracy.csv             # Final analysis outputs
│   ├── 20250530_anova_for_accuracy.csv             # Final analysis outputs
│   ├── 20250530_tukey_hsd_for_compute_time.csv             # Final analysis outputs
│   ├── 20250530_tukey_hsd_for_compute_time.csv             # Final analysis outputs
├── src/
│   ├── 2D_void_reconstructin.ipynb                    # Read and filter point cloud
│   ├── plane_fit_utils.py               # Plane fitting and jittered sampling
│   ├── interpolation_methods.py         # Spline, PDE, IDW, Kriging
│   ├── evaluation_metrics.py            # RMSE, timing, ANOVA, Tukey HSD
├── README.md
```

---

## 🎯 Objectives

- Reconstruct void regions in terrain using nearby ground points.
- Evaluate methods across multiple geometries and orientations.
- Quantify accuracy and computational efficiency.
- Visualise iteration-wise progression for transparency and insight.

---

## 📈 Methods Summary

### ✅ 2D Iterative Line Fitting
- Fitted along X or Y axis.
- Uses a sliding window (3m wide, with 2m overlap) to extend 1m per iteration.
- Samples equidistant points with **quadratic jittering**.
- Supports **midpoint** or **full** A-to-B traversal.

### ✅ 3D Iterative Plane Fitting
- Each plane spans 2m (across void) × 3m (along direction).
- Extends 1.5m initially, then 1m per step.
- Jittered samples on extended fronts form basis for next plane.
- Midpoint or full traversal strategies applied.

---

## 📊 Evaluation Metrics

- **Root Mean Square Error (RMSE)** against real ground points removed from void interiors.
- **Compute Time** for each reconstruction run.
- **Statistical analysis**:
  - One-way ANOVA
  - Tukey HSD post-hoc test
  - Rankings by accuracy and speed

---

## 📦 Datasets

| File                                               | Description                                 |
|----------------------------------------------------|---------------------------------------------|
| `S7_1.laz`                                          | Ground-filtered aerial point cloud          |
| `20250528_30x_voids.csv`                            | 30 rectangular occlusions (test zones)      |
| `20250528_methods_rmse_all.csv`                     | RMSE for all combinations (method × axis)   |
| `20250528_selected_methods_compute_time.csv`        | Compute time for 4 selected methods         |

-
S7_1 laz file was taken from OpenGF Publicly available source took from [here](https://drive.google.com/drive/folders/1ud3fuiaNGHBiTVmIg36mrDarz-zzCzID). It is part of [this repository](https://github.com/Nathan-UW/OpenGF?tab=readme-ov-file) . [Paper link](https://openaccess.thecvf.com/content/CVPR2021W/EarthVision/html/Qin_OpenGF_An_Ultra-Large-Scale_Ground_Filtering_Dataset_Built_Upon_Open_ALS_CVPRW_2021_paper.html)
---

## 📚 Notebooks

| Notebook                                 | Description                             |
|------------------------------------------|-----------------------------------------|
| `2D_void_Reconstruction.ipynb`           | Runs 2D line fitting on all voids       |
| `3D_void_Reconstruction.ipynb`           | Runs 3D plane fitting with visualisation|

---

## 📊 Example Results (summary)

| Method           | Mean RMSE (m) | Mean Time (s) |
|------------------|---------------|---------------|
| MID | X | Spline |     2.84      |     0.92      |
| MID | X | PDE    |     2.83      |     2.84      |
| FULL | X | Spline|     2.69      |     4.25      |
| FULL | X | PDE   |     2.67      |     4.98      |

*See full results in CSVs for statistical breakdowns.*

---

## Requirements

Install dependencies with:

```bash
pip install -r requirements.txt
```

Required packages include:
- `numpy`, `pandas`, `matplotlib`
- `laspy`, `sklearn`, `scipy`
- `shapely`, `sklearn`, `statsmodels`

---

## 🧪 Future Work

- Extend to adaptive patch sizes
- Extend based on point density

---

## 📬 Contact

This repository is part of a research project on **terrain reconstruction using geometric analysis and anisotropy-aware interpolation**. For questions or collaboration, please contact the repository owner.
=======
