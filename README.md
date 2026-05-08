# BanglaOCR

BanglaOCR is a Bangla character recognition project built with PyTorch and EfficientNet-B0.

## Workflow

The workflow in this repository follows these steps:

1. **Load the dataset**
   - Images are read from `Train/` and `Test/` folders.
   - Each class is stored in a numeric folder name.
   - `.bmp` images are loaded as grayscale.

2. **Preprocess and augment images**
   - Images are resized to `64x64`.
   - Training data uses small random rotations and affine translations.
   - Images are normalized before being passed to the model.

3. **Create train/validation/test loaders**
   - The training set is split into train and validation subsets.
   - Data is loaded with PyTorch `DataLoader` objects.

4. **Train EfficientNet-B0**
   - EfficientNet-B0 is adapted for grayscale input.
   - The classifier head is replaced for 243 classes.
   - Training uses Adam optimizer and cross-entropy loss.
   - Early stopping keeps the best validation model.

5. **Save training artifacts**
   - The best model is saved as `efficientnet_b0.pth`.
   - Training plots are saved as `training_plot.png`.

6. **Evaluate on the test set**
   - The saved model is loaded for testing.
   - Accuracy and classification report are generated.
   - A confusion matrix is saved as `confusion_matrix.png`.

7. **Export predictions**
   - Predictions are written to `predictions.csv` with image path, actual label, and predicted label.

## Repository Outputs

The notebook creates its outputs in the model directory, such as:

- `efficientnet_b0.pth`
- `training_plot.png`
- `confusion_matrix.png`
- `predictions.csv`

## Notes

- The notebook is designed for Bangla OCR character classification.
- Update dataset paths before running if your local folder structure is different.
