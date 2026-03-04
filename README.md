# Classical Gallbladder Segmentation — Gallbladder Cancer (Kaggle)

Classic image processing pipeline for gallbladder segmentation in ultrasound images. Built exclusively with low-level operations using NumPy, OpenCV, and scikit-image — no AI models or high-level abstractions.

---

## Pipeline (7 stages)

| 01 | Ingestion & Traceability | Image loading with `manifest.csv` inventory |
| 02 | Histogram Homogenization | Manual equalization using NumPy primitives (`np.histogram`, `np.cumsum`, `np.interp`) |
| 03 | Basic Transforms | Log transform, power/gamma transform, and Gaussian smoothing |
| 04 | Binarization + Morphology | Vectorized boolean indexing + morphological opening/closing |
| 05 | ROI Selection | Connected components via `skimage.measure.label` and `regionprops` |
| 06 | Gradient (Prewitt) | Custom `conv2d()` implemented from scratch with Prewitt kernels |
| 07 | Laplacian | Custom `conv2d()` with Laplacian kernel + Gaussian pre-smoothing |

---

## Dataset

- **Source:** [Gallbladder Cancer — Kaggle](https://www.kaggle.com/datasets/aneerbansaha/gallbladder-cancer)
- **Folder used:** `validation/nml/`

Kaggle requires manual download or API access. See `manifest.csv` for the full image inventory with paths, classes, formats, and sizes.

---

## Repository Structure

```
├── pipeline.ipynb        # Fully reproducible main notebook
├── manifest.csv          # Processed image inventory (id, path, class, format, size)
├── resultados/           # Output images per evaluated image
│   ├── step_01_input.png
│   ├── step_02_homogenized.png
│   ├── step_03_transform1.png
│   ├── step_03_transform2.png
│   ├── step_04_binary_raw.png
│   ├── step_04_binary_clean.png
│   ├── step_04_overlay.png
│   ├── step_05_roi_selected.png
│   ├── step_05_roi_overlay.png
│   ├── step_06_grad_mag.png
│   └── step_07_laplacian.png
```

---

## Requirements

```bash
pip install numpy opencv-python scikit-image pandas pillow matplotlib
```

---

## Usage

1. Download the dataset from Kaggle and place it locally.
2. Update the dataset path in `pipeline.ipynb`.
3. Run all cells — the pipeline processes all images uniformly (no per-image parameter tuning).
4. Results are saved automatically to `resultados/`.

---

## Constraints

- All binarization is fully vectorized — no `if/elif/else` or pixel-by-pixel loops.
- Histogram equalization uses only NumPy — no `cv2.equalizeHist` or CLAHE.
- Gradient and Laplacian use a custom `conv2d()` — no `cv2.Sobel`, `cv2.Laplacian`, or scipy.
- ROI selection uses connected components only — no pretrained models.
- Same parameters applied to all images — no per-image tuning.
