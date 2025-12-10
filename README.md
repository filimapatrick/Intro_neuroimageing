# MRI Image Processing with Nibabel

A comprehensive introduction to working with MRI neuroimaging data using Python. This notebook series covers loading, visualizing, processing, and analyzing brain MRI images using Nibabel, NumPy, SciPy, and Matplotlib.

## Overview

This project demonstrates essential techniques for working with NIfTI (Neuroimaging Informatics Technology Initiative) MRI files, including:

- Loading and inspecting MRI data structures
- Visualizing 3D brain scans in multiple planes (sagittal, coronal, axial)
- Basic image statistics and histogram analysis
- Image filtering and morphological operations
- Batch processing multiple subjects and extracting statistics

## Project Structure

```
.
├── 01_nibabel_intro.ipynb       # Main Jupyter notebook with all lessons
├── datasets/                     # Directory for MRI files
├── summary_stats.csv            # Output CSV with extracted statistics
├── README.md                    # This file
└── .gitignore                   # Git ignore file
```

## Installation & Setup

### Prerequisites

- Python 3.7+
- Virtual environment (recommended)

### Create and Activate Virtual Environment

```bash
python -m venv .venv
source .venv/bin/activate  # On macOS/Linux
# or
.venv\Scripts\activate  # On Windows
```

### Install Dependencies

```bash
pip install nibabel numpy matplotlib scipy pandas jupyter
```

Alternatively, run the first cell in the notebook:
```python
pip install nibabel numpy matplotlib scipy pandas
```

## Notebook Contents

### 01 — Introduction to Nibabel: Loading and Inspecting MRI
- Load NIfTI MRI files using Nibabel
- Extract data arrays, affine matrices, and headers
- Print MRI shape, data type, and voxel dimensions
- Visualize 3D slices in anatomical planes

### 02 — NumPy for MRI: Slicing, Masking, Stats, Histogram
- Index and slice 3D MRI data using NumPy
- Compute basic statistics (mean, median, min, max)
- Create brain masks using intensity thresholding
- Generate intensity histograms

### 03 — MRI Image Processing: Filtering and Morphology
- Apply Gaussian smoothing/filtering to MRI data
- Create binary masks from thresholded data
- Apply morphological operations:
  - **Erosion**: Remove small structures
  - **Dilation**: Fill small holes
- Visualize original, eroded, and dilated masks

### 04 — Mini Project: Loop Through Subjects & Extract Stats
- Batch process multiple MRI files
- Extract statistics for each subject:
  - Mean, median, min, max intensity
  - Voxel count
  - Histogram peak intensity
- Save results to CSV file for further analysis

## Key Libraries

| Library | Purpose |
|---------|---------|
| **Nibabel** | Read/write NIfTI MRI files |
| **NumPy** | Array operations and computations |
| **Matplotlib** | Data visualization and image display |
| **SciPy** | Advanced image processing (filtering, morphology) |
| **Pandas** | Data manipulation and CSV export |

## Usage

1. **Prepare your data**: Place MRI files (`.nii` or `.nii.gz`) in the `datasets/` folder
2. **Update file paths**: Modify `nii_path` variables in cells to match your filenames
3. **Run cells sequentially**: Execute notebook cells from top to bottom
4. **View results**: Inspect generated plots and CSV statistics

### Example: Processing your own MRI

```python
import nibabel as nib
import numpy as np

# Load MRI
img = nib.load("your_file.nii.gz")
data = img.get_fdata()

# Get dimensions
print("Shape:", data.shape)
print("Data type:", data.dtype)

# Apply mask and statistics
mask = data > 10
brain_voxels = data[mask]
print("Brain mean intensity:", np.mean(brain_voxels))
```

## Output Files

- **summary_stats.csv**: Contains statistics for all processed MRI files
  - Columns: subject, mean_intensity, median_intensity, max_intensity, min_intensity, voxel_count, hist_peak

## Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| `ModuleNotFoundError` | Run the first cell to install dependencies via pip |
| `FileNotFoundError` for MRI files | Ensure `.nii` files are in `datasets/` folder and path is correct |
| `IndexError` on slicing | Use dynamic indexing: `data.shape[2]//2` instead of hardcoded indices |
| Empty CSV output | Check that MRI files exist in `datasets/` and match expected format |

## MRI Coordinate Systems

The notebook uses standard anatomical planes:

- **Sagittal**: Left-right cross-section (X-axis)
- **Coronal**: Front-back cross-section (Y-axis)
- **Axial**: Top-bottom cross-section (Z-axis)

Each slice is transposed and displayed with `origin='lower'` for anatomical orientation.

## Tips & Best Practices

1. **Check your data first**: Always inspect `data.shape`, `data.dtype`, and `data.min()/max()`
2. **Use dynamic indexing**: Avoid hardcoding slice indices; use `data.shape[axis]//2`
3. **Mask before statistics**: Apply brain masks to exclude background voxels
4. **Batch processing**: Use loops to process multiple subjects programmatically
5. **Save results**: Export statistics to CSV for downstream analysis

## Resources

- [Nibabel Documentation](https://nipy.org/nibabel/)
- [NIfTI Format Specification](https://nifti.nimh.nih.gov/)
- [NumPy Array Indexing](https://numpy.org/doc/stable/reference/arrays.indexing.html)
- [SciPy Image Processing](https://docs.scipy.org/doc/scipy/reference/ndimage.html)

## License

This educational material is provided as-is for learning purposes.

## Author

Created for neuroimaging data processing tutorials.
# Intro_neuroimageing
