# AES Encryption Mode Classification using CNN

## Overview

This project investigates whether a Convolutional Neural Network (CNN) can distinguish between images encrypted using different AES encryption modes.

Using the Intel Image Classification Dataset, AES-ECB and AES-CBC encrypted versions of each image were generated and a CNN was trained to classify images into three categories:

* Original
* AES-ECB
* AES-CBC

---

## Dataset

**Intel Image Classification Dataset**

* Original Images: 14,034
* Image Size: 150 × 150
* Classes:

  * Buildings
  * Forest
  * Glacier
  * Mountain
  * Sea
  * Street

Dataset Source:
https://www.kaggle.com/datasets/puneet6060/intel-image-classification

---

## Data Generation

For every original image:

1. Original image retained
2. AES-ECB encrypted image generated
3. AES-CBC encrypted image generated

This expanded the dataset from:

* 14,034 original images

to

* 42,102 total samples

| Class    | Samples |
| -------- | ------- |
| Original | 14,034  |
| AES-ECB  | 14,034  |
| AES-CBC  | 14,034  |

---

## Methodology

### Image Processing

* Resize images to 150 × 150
* Random horizontal flip
* Random rotation (±10°)
* Normalization to [0,1]

### Encryption

AES-128 encryption was implemented using:

* ECB (Electronic Codebook) Mode
* CBC (Cipher Block Chaining) Mode

### Model

A Convolutional Neural Network (CNN) was trained using PyTorch to classify images into:

* Original
* ECB
* CBC

---

## Train-Test Split

* Training Images: 11,227
* Validation Images: 2,807

After expansion:

* Training Samples: 33,681
* Validation Samples: 8,421

---

## Results

### Best Validation Accuracy

98.57%

### Confusion Matrix

| Actual \ Predicted | Original | ECB  | CBC  |
| ------------------ | -------- | ---- | ---- |
| Original           | 2807     | 0    | 0    |
| ECB                | 0        | 2661 | 146  |
| CBC                | 0        | 4    | 2803 |

### Classification Performance

* Original Accuracy: 100%
* ECB Accuracy: 94.8%
* CBC Accuracy: 99.86%

---

## Key Findings

* CNNs can reliably distinguish AES-ECB and AES-CBC encrypted images when sufficient image resolution is available.
* Small datasets such as CIFAR-10 (32×32 images) produced significantly lower performance (~66.7% accuracy).
* Larger images (150×150) preserve enough statistical information for a CNN to learn differences between encryption modes.

---

## Technologies Used

* Python
* PyTorch
* NumPy
* Matplotlib
* Scikit-Learn
* Pillow
* PyCryptodome

---

## Repository Structure

```text
AES-CNN-Encryption-Classifier
│
├── AES_Image_Classification.ipynb
├── README.md
├── requirements.txt
├── confusion_matrix.png
├── loss_curve.png
└── intel_aes_classifier.pth
```

## Future Work

* Classification of CBC vs CTR encryption modes
* Comparison with additional AES modes (CFB, OFB, GCM)
* Deeper CNN architectures
* Explainability and feature visualization
* Analysis on larger image datasets

---

## Author

Yashraj Singh
