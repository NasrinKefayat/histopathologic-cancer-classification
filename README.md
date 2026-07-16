# Histopathologic Cancer Classification

Deep learning project for binary classification of histopathology image patches using transfer learning with ResNet18 and DenseNet121.

The objective of this project is to classify image patches as either:

- `0`: No tumor tissue
- `1`: Tumor tissue present

Two convolutional neural network architectures were trained and compared under different hyperparameter settings.

## Project Overview

Histopathologic image classification is an important task in medical image analysis. The goal is to automatically detect whether a tissue image patch contains tumor cells.

In this project, I used two ImageNet-pretrained deep learning models:

- ResNet18
- DenseNet121

Both models were fine-tuned on a subset of the Kaggle Histopathologic Cancer Detection dataset.

The workflow includes:

- Dataset preparation
- Random subset selection
- Exploratory data analysis
- Train, validation, and test splitting
- Data augmentation
- Transfer learning
- Hyperparameter experiments
- Model evaluation
- ResNet18 and DenseNet121 comparison

## Dataset

The project uses the Histopathologic Cancer Detection dataset from Kaggle.

The original dataset is large and contains many histopathology image patches. Due to computational and storage limitations in Google Colab, a randomly selected subset of the dataset was used for this project.

The subset contains:

- 5,000 image patches
- 3,095 negative samples
- 1,905 positive samples
- Image size: 96 × 96 pixels
- RGB images
- Binary labels

Class distribution:

- Negative: 61.9%
- Positive: 38.1%

The dataset is not included in this repository.

## Data Splitting

The selected subset was divided into:

- Training set: 80%
- Validation set: 10%
- Test set: 10%

Stratified splitting was used to preserve the class distribution across all subsets.

## Data Preprocessing and Augmentation

Training images were augmented to improve model generalization.

The preprocessing pipeline includes:

- Resize
- Random horizontal flip
- Random vertical flip
- Random rotation
- Color jitter
- Tensor conversion
- ImageNet normalization

Validation and test images were resized, converted to tensors, and normalized without random augmentation.

## Models

### ResNet18

ResNet18 uses residual connections that help gradients flow through the network and make deep models easier to train.

The original classification layer was replaced with a new fully connected layer for binary classification.

### DenseNet121

DenseNet121 connects each layer to all previous layers within a dense block. This improves feature reuse and supports stronger gradient flow.

The original classifier was replaced with a new output layer for binary classification.

## Transfer Learning

Both models were initialized with ImageNet-pretrained weights.

The final classification layer was adapted for two output classes, and the complete network was fine-tuned on the histopathology dataset subset.

## Training Configuration

The models were trained using:

- Loss function: CrossEntropyLoss
- Optimizer: Adam
- Learning-rate scheduler: ReduceLROnPlateau
- Epochs: 10
- Validation-based model checkpointing

The model with the highest validation accuracy was saved and later used for test evaluation.

## Hyperparameter Experiments

Several combinations of learning rate and batch size were tested.

Learning rates:

- `0.0001`
- `0.00005`
- `0.00001`

Batch sizes:

- `16`
- `32`

These experiments were performed for both ResNet18 and DenseNet121.

## Evaluation Metrics

The models were evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion matrix
- Classification report

Because the dataset is imbalanced, F1-score and recall are especially important alongside accuracy.

## Results

### Best ResNet18 Result

Best configuration:

- Learning rate: `0.00005`
- Batch size: `32`

Performance:

| Metric | Score |
|---|---:|
| Accuracy | 0.9196 |
| Precision | 0.9345 |
| Recall | 0.8509 |
| F1-score | 0.8908 |

### Best DenseNet121 Result

Best configuration:

- Learning rate: `0.00001`
- Batch size: `32`

Performance:

| Metric | Score |
|---|---:|
| Accuracy | 0.9066 |
| Precision | 0.8602 |
| Recall | 0.9172 |
| F1-score | 0.8878 |

## Model Comparison

| Model | Learning Rate | Batch Size | Accuracy | Precision | Recall | F1-score |
|---|---:|---:|---:|---:|---:|---:|
| ResNet18 | 0.00005 | 32 | 0.9196 | 0.9345 | 0.8509 | 0.8908 |
| DenseNet121 | 0.00001 | 32 | 0.9066 | 0.8602 | 0.9172 | 0.8878 |

ResNet18 achieved the highest overall accuracy, precision, and F1-score.

DenseNet121 achieved the highest recall, meaning it identified a larger proportion of positive tumor samples.

This comparison shows that model selection depends on the main objective:

- ResNet18 provides stronger overall classification performance.
- DenseNet121 may be preferable when reducing false negatives is more important.

## Project Structure

```text
histopathologic-cancer-classification/
│
├── notebooks/
│   ├── resnet18_histopathologic_cancer_detection.ipynb
│   └── densenet121_histopathologic_cancer_detection.ipynb
│
├── presentation/
│   └── histopathologic_cancer_detection_presentation.pdf
│
├── README.md
├── requirements.txt
└── .gitignore

Running the Project

The notebooks were developed and tested in Google Colab.

To run the project:

Download the Histopathologic Cancer Detection dataset from Kaggle.
Create or select a subset of the dataset.
Update the dataset path in the notebooks.
Install the required libraries.
Run the notebooks in Google Colab or Jupyter Notebook.

The original private Google Drive paths were removed from the notebooks.

Technologies
Python
PyTorch
Torchvision
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Pillow
Google Colab
Limitations
Only a randomly selected subset of the full Kaggle dataset was used.
The dataset contains class imbalance.
Training was limited to 10 epochs.
Results may vary depending on the selected random subset.
The project was developed under Google Colab resource limitations.
Future Work

Possible improvements include:

Training on the complete dataset
Testing additional architectures
Applying weighted loss or sampling strategies
More extensive hyperparameter optimization
Increasing the number of epochs
Adding cross-validation
Evaluating ROC-AUC and precision-recall curves
Using explainability methods such as Grad-CAM
Presentation

A complete project presentation is available in:

presentation/histopathologic_cancer_detection_presentation.pdf