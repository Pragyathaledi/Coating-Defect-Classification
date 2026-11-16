# Transfer learning for multi-label coating defect classification

Code and results for the paper *"Transfer learning for multi-label coating defect classification: evaluation protocol, noise robustness and deployment cost"* ([Authors], 2026).

## What this repository does
Four models are compared on the public **CoatingVision** dataset (2,227 electrode-coating images, four labels: surface crack, delamination, pinhole, unclassified):
a small CNN trained from scratch, and ImageNet-pretrained **ResNet50**, **EfficientNet-B0** and **ConvNeXt-Tiny**.

1. Random split (70/10/20) and a **sample-wise split** (frames from one recording never appear in more than one partition)
2. Robustness to Gaussian noise, Gaussian blur and brightness change
3. Model size and single-image inference time
4. Grad-CAM heatmaps

## How to run
1. Open `coating_defect_classification.ipynb` in [Google Colab](https://colab.research.google.com) (File > Upload notebook).
2. Runtime > Change runtime type > GPU.
3. Run all cells **in order, in one session**. The dataset is downloaded automatically from Figshare.

Dependencies are listed in `requirements.txt` (Colab already provides most of them).

## Data
The dataset is **not** included here. It is downloaded from https://doi.org/10.6084/m9.figshare.29260121.v1 (CC BY 4.0). Please cite the dataset paper: V. Sampath et al., "A defect dataset for electrode coating manufacturing", *Scientific Data* 13, 1333 (2026).

## Results
Files in `results/` (seed 42, one run per model and protocol):
- `results_classification.csv`, `random_vs_honest.csv`, `results_speed_size.csv`: original CSV files written by the notebook.
- `results_honest_split.csv` (sample-wise split, per label) and `results_robustness.csv` (noise/blur/brightness): **transcribed from the printed Colab output**, so values are rounded to 3-4 decimals. Re-running the notebook writes exact versions.

Figures are in `figures/` (`fig1_split_comparison.png`, `fig2_robustness.png`, `fig3_gradcam.png` are the ones used in the paper; the Grad-CAM panels come from the original Colab output).

## Notes and limitations
- One training run per configuration. GPU training is not bit-exact, so re-running can change scores by a few thousandths to hundredths; differences between the pretrained models are within that range.
- The dataset has only eight recordings, and the "unclassified" label has 14 positive test images in the sample-wise split.
- The data are electrode coatings; no claim is made about aerospace or nano-scale coatings.
- The notebook was assembled from cells that were run one after another in Colab; if a cell errors, please open an issue with the message.

## Licence
Code: MIT (see `LICENSE`). Dataset: CC BY 4.0 (see the Figshare record).
