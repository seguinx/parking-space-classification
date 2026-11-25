# Parking Space Classification with Deep Learning

A three-class image classification project comparing a custom CNN, data augmentation, and transfer learning with ResNet18.

## Classes

| Label | Class |
|---:|---|
| 0 | Occupied |
| 1 | Available |
| 2 | Available but restricted |

## Models and experiments

- Custom CNN trained from scratch
- CNN with rotation and color augmentation
- CNN with affine augmentation (rotation, translation, and scaling)
- ResNet18 transfer learning using feature extraction
- ResNet18 fine-tuning (unfreezing `layer4` and training the final classifier)

## Best result

In the recorded experiment, **ResNet18 with fine-tuning achieved 86.86% test accuracy**.

| Model | Test accuracy | Training time (s) |
|---|---:|---:|
| Baseline CNN | 74.29% | 20.31 |
| CNN + Augmentation 1 | 71.43% | 47.15 |
| CNN + Augmentation 2 | 77.14% | 30.44 |
| ResNet18 Feature Extraction | 77.71% | 71.48 |
| ResNet18 Fine-Tuning | **86.86%** | 70.83 |

Training times depend on the hardware and runtime environment. The results above are from the recorded run and may vary when the notebook is re-executed.

## Repository structure

```text
.
├── parking_space_classification.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── data/
    └── images_128/
        ├── 0/
        ├── 1/
        └── 2/
```

## Dataset setup

The image dataset is not included in this repository. Add your images locally using the folder structure above:

```text
data/images_128/0/   # Occupied images
data/images_128/1/   # Available images
data/images_128/2/   # Available but restricted images
```

The notebook expects the folder names `0`, `1`, and `2`. Do not commit private, licensed, or otherwise restricted images unless you have permission to redistribute them.

## Installation

Python 3.10 or 3.11 is recommended.

```bash
git clone https://github.com/seguinx/parking-space-classification.git
cd parking-space-classification

python -m venv .venv
```

Activate the environment:

**Windows PowerShell**
```powershell
.venv\Scripts\Activate.ps1
```

**macOS / Linux**
```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

For GPU acceleration, install the PyTorch build that matches your CUDA environment. See the [official PyTorch installation selector](https://pytorch.org/get-started/locally/).

## Run the notebook

```bash
jupyter notebook parking_space_classification.ipynb
```

You can also open the notebook in [Google Colab](https://colab.research.google.com/) after uploading it or opening it from GitHub. Select a GPU runtime if available.

## Methodology

- Dataset split: 70% training, 15% validation, and 15% test.
- Stratified split with a fixed random seed.
- The same split is reused across experiments.
- Data augmentation is applied to training images only.
- Validation data are used for model selection.
- The test set is reserved for final evaluation.
- Evaluation includes accuracy, classification reports, confusion matrices, and misclassified examples.

## Notes

- The notebook saves model checkpoints (`.pth`) during training. These files are generated locally and are excluded from Git by `.gitignore`.
- The notebook has been prepared with cleared cell outputs for a lighter, cleaner GitHub upload. Re-run the cells to regenerate outputs and figures.
