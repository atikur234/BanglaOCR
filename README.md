# BanglaOCR

BanglaOCR is a Bangla character recognition project built with PyTorch. The repository contains two training notebooks that use different CNN backbones for the same OCR dataset:

- `efficientnet_b0_ocr_dataset.ipynb`
- `resnet18_full_ocr_dataset.ipynb`

Both notebooks follow a similar workflow for training, evaluation, and result export.

## Dataset Structure

The notebooks expect the dataset to be arranged like this:

```text
Final_Bangla_OCR_Dataset/
├── Train/
│   ├── 001/
│   ├── 002/
│   └── ...
└── Test/
    ├── 001/
    ├── 002/
    └── ...
```

- Images are `.bmp` files.
- Each numeric folder represents a character class.
- Images are loaded as grayscale.

## Workflow

### 1. Load and prepare the dataset
- Read training images from `Train/` and test images from `Test/`.
- Convert images to grayscale.
- Assign labels by folder name, using `001 -> 0` through `243 -> 242`.

### 2. Apply preprocessing and augmentation
- Resize images to `64x64`.
- Apply light augmentation during training:
  - random rotation
  - random affine translation
- Normalize the tensor values before feeding them to the model.

### 3. Create training, validation, and test loaders
- Split the training set into training and validation subsets.
- Use PyTorch `DataLoader` for batching.
- Use batch size `64` for training, validation, and testing.

### 4. Train a CNN model
The repository provides two training options:

- **EfficientNet-B0 notebook**
  - Replaces the first convolution layer to accept grayscale input.
  - Replaces the classifier head for `243` classes.
  - Trains for up to `20` epochs with Adam and cross-entropy loss.

- **ResNet-18 notebook**
  - Replaces the first convolution layer to accept grayscale input.
  - Replaces the fully connected layer for `243` classes.
  - Trains for up to `20` epochs with Adam and cross-entropy loss.

Both notebooks use **early stopping** to keep the best validation model.

### 5. Save model and training plots
- Save the best model weights to the model output directory.
- Save training curves showing loss and accuracy progression.

### 6. Evaluate on the test set
- Load the best saved checkpoint.
- Run inference on the test set.
- Generate:
  - test accuracy
  - classification report
  - confusion matrix

### 7. Export predictions
- Save a CSV file containing:
  - image path
  - actual label
  - predicted label

## Output Folders

Each notebook stores its outputs in a separate directory:

- `EfficientNetB0-20epochs/`
- `ResNet18-20epoch/`

Typical output files include:

- `efficientnet_b0.pth`
- `resnet18.pth`
- `training_plot.png` or `train_val_plot.png`
- `confusion_matrix.png`
- `predictions.csv`

## Results

From the notebook outputs:

- **EfficientNet-B0** achieved about **90.39%** test accuracy.
- **ResNet-18** achieved about **86.46%** test accuracy.

## Notes

- Update the `BASE_DIR` path in the notebooks before running them on your machine.
- The project is focused on Bangla OCR character classification.
- The notebooks are designed for experimentation and model comparison.
