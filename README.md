# Classical-Segmentation-Gallbladder-Cancer-Kaggle-
Classic image processing pipeline for gallbladder segmentation in ultrasound images. Built exclusively with low-level operations using NumPy, OpenCV, and scikit-image — no AI models or high-level abstractions.
# Pipeline (7 stages)

Ingestion & traceability — Image loading with manifest.csv inventory
Histogram homogenization — Manual equalization using NumPy primitives
Basic transforms — Log, power/gamma, and Gaussian smoothing
Binarization + morphology — Vectorized boolean indexing + morphological opening/closing
ROI selection — Connected components via skimage.measure.label and regionprops
Gradient (Prewitt/Sobel) — Custom convolution implemented from scratch
Laplacian — Custom convolution with Laplacian kernel + Gaussian pre-smoothing
