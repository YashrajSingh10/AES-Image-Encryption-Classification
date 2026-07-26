# AES Encryption Mode Classification using CNN

## Overview

This project investigates whether a Convolutional Neural Network (CNN) can distinguish between images encrypted using different AES encryption modes.

Using the Intel Image Classification Dataset, multiple experiments were conducted to analyze the ability of CNNs to classify encrypted images under different AES modes and initialization strategies. The project includes comparisons between ECB, CBC, CTR, CFB, and OFB encryption modes, along with an analysis of the effect of random and fixed Initialization Vectors (IVs) and nonces on classification performance.

---

## Dataset

**Intel Image Classification Dataset**

- Original Images: 14,034
- Image Size: 150 × 150

Classes:

- Buildings
- Forest
- Glacier
- Mountain
- Sea
- Street

Dataset Source:

https://www.kaggle.com/datasets/puneet6060/intel-image-classification

---

## Experiments

### Experiment 1: Original vs ECB vs CBC

The original images were encrypted using ECB and CBC modes.

Classes:

- Original
- AES-ECB
- AES-CBC

Total Samples: **42,102**

Validation Accuracy: **96.71%**

---

### Experiment 2: CBC vs CTR (Fixed Counter Initialization)

The original images were encrypted using CBC and CTR modes. CTR encryption was performed using a fixed counter initialization to study whether the CNN could distinguish between the two encryption modes.

Classes:

- AES-CBC
- AES-CTR

Total Samples: **28,068**

---

### Experiment 3: CBC vs CTR (Variable Counter Initialization)

The experiment was repeated using a variable (random) counter initialization for CTR mode while keeping the CNN architecture unchanged. This allowed evaluation of the effect of counter initialization on classification performance.

Classes:

- AES-CBC
- AES-CTR

Total Samples: **28,068**

---

### Experiment 4: CBC vs CTR vs CFB vs OFB

ECB was replaced with the more secure CFB and OFB modes to evaluate CNN performance on four AES encryption modes.

Two experiments were conducted.

#### Experiment 4A: Random IV / Nonce

- Random IV for CBC, CFB, and OFB
- Random nonce for CTR

Result:

- Validation Accuracy: **25.00%**

Since a new IV/nonce was generated for every image, the encrypted outputs changed every time, leaving almost no consistent patterns for the CNN to learn.

#### Experiment 4B: Fixed IV / Nonce

- Fixed IV for CBC, CFB, and OFB
- Fixed nonce for CTR

Result:

- Validation Accuracy: **98.40%**

Using fixed initialization produced consistent encrypted outputs for each mode, allowing the CNN to learn mode-specific characteristics and classify the encryption modes successfully.

---

## Methodology

### Image Processing

- Resize images to 150 × 150
- Random Horizontal Flip
- Random Rotation (±10°)
- Normalize pixel values to [0,1]

### AES Encryption

AES-128 encryption was implemented using the following modes:

- ECB (Electronic Codebook)
- CBC (Cipher Block Chaining)
- CTR (Counter Mode)
- CFB (Cipher Feedback)
- OFB (Output Feedback)

Different experiments were performed using both random and fixed Initialization Vectors (IVs) and nonces to study their impact on CNN-based encryption mode classification.

### CNN Architecture

A Convolutional Neural Network (CNN) was implemented using PyTorch.

Architecture:

- Convolution Layer (32 Filters)
- ReLU
- Max Pooling

- Convolution Layer (64 Filters)
- ReLU
- Max Pooling

- Convolution Layer (128 Filters)
- ReLU
- Max Pooling

- Convolution Layer (256 Filters)
- ReLU
- Max Pooling

- Fully Connected Layer (512 Neurons)

- Output Layer

The same CNN architecture was used across all experiments.

---

## Train-Test Split

Training Images: **11,227**

Validation Images: **2,807**

The generated encrypted images were split using an 80:20 train-validation ratio.

---

## Experimental Results

| Experiment | Classes | Validation Accuracy |
|------------|-----------------------------|----------------:|
| Original vs ECB vs CBC | 3 | 96.71% |
| CBC vs CTR (Fixed Counter) | 2 | *(Update)* |
| CBC vs CTR (Variable Counter) | 2 | *(Update)* |
| CBC vs CTR vs CFB vs OFB (Random IV/Nonce) | 4 | 25.00% |
| CBC vs CTR vs CFB vs OFB (Fixed IV/Nonce) | 4 | 98.40% |

---

## Key Findings

- CNNs can successfully distinguish different AES encryption modes when consistent encryption characteristics are present.
- ECB preserves visible image patterns, making it easier to distinguish than the other AES modes.
- Random IVs and nonces generate different ciphertexts for every encryption, resulting in almost no consistent learnable patterns and reducing the CNN accuracy to approximately **25%**.
- Using fixed IVs and nonces produces consistent encrypted outputs, allowing the CNN to learn mode-specific characteristics and increasing the validation accuracy to **98.40%**.
- Larger image resolutions preserve sufficient statistical information for CNN-based encryption mode classification.

---

## Technologies Used

- Python
- PyTorch
- NumPy
- Matplotlib
- Scikit-Learn
- Pillow
- PyCryptodome

---



## Future Work

- Investigate AES-GCM and authenticated encryption modes.
- Evaluate deeper CNN architectures such as ResNet and EfficientNet.
- Perform explainability analysis using Grad-CAM.
- Extend the study to larger image datasets.
- Compare AES-128, AES-192, and AES-256.

---

## Author

**Yashraj Singh**
