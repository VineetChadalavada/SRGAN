# Super-Resolution Generative Adversarial Network (SRGAN)

This project implements a Super-Resolution Generative Adversarial Network (SRGAN) to upscale low-resolution images to high-resolution images, specifically designed for binary classification tasks (e.g., classifying cats vs. dogs). This README documents the steps followed for the project setup, training process, and evaluation.

## Table of Contents
1. [Introduction](#1-Introduction)
2. [Project Structure](#2-Project-Structure)
3. [Getting Started](#3_Getting-Started)
4. [Training Process](#4-Training-Process)
5. [Results and Evaluation](#5-Results-and-evaluation)
6. [References](#6-References)

### 1. Introduction

I implemented an SRGAN to generate high-resolution images from low-resolution inputs, which were then used in a binary classification task. SRGAN combines GANs and convolutional neural networks (CNNs) to produce realistic high-resolution images from low-resolution images. This approach is useful in applications like medical imaging, satellite imagery, and object detection.

### 2. Project Structure

The project is organized as follows:

- `models/` - Contains saved model files:
  - `mobilenetv2_model_a.h5`: Model A trained on the original dataset.
  - `discriminator_epoch_150.keras`: Discriminator model from SRGAN after 150 epochs.
  - `generator_epoch_150.keras`: Generator model from SRGAN after 150 epochs.
  - `mobilenetv2_model_b.h5`: Model B trained on SRGAN-generated images along with the original dataset.
- `notebooks/` - Jupyter Notebooks used during the training process:
  - `Model_A_vchadala.ipynb`: Notebook for training Model A.
  - `SRGAN_vchadala.ipynb`: Notebook for training the SRGAN.
  - `Model_B_vchadala.ipynb`: Notebook for training Model B.
- `images/` - Sample images generated by SRGAN, demonstrating the quality of the output.
- `docs/` - Includes a report comparing Model A and Model B.

### 3. Getting Started

#### Prerequisites
- **Python 3.x**
- Required libraries:
  ```bash
  pip install tensorflow keras matplotlib numpy

  ### Setup

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/VineetChadalavada/SRGAN.git
   cd SRGAN
2. **Install Git LFS (for handling large model files)**:
   ```bash
   git lfs install
   git lfs pull
### 4. Training Process

The following steps outline the training process that I followed:

#### Step 1: Train Model A (Binary Classifier)
- **Objective**: Train a binary classifier (Model A) on the original dataset images using `Model_A_vchadala.ipynb`.
- **Preprocessing**: Images were resized to 128x128, with data augmentation methods applied, including rescaling, rotation, width shift, height shift, shear, zoom, horizontal flip, and fill mode.
- **Training**: I used a pre-trained MobileNetV2 model and fine-tuned it for binary classification (cats vs. dogs).
- **Output**: The trained model was saved as `mobilenetv2_model_a.h5` in the `models/` folder.

#### Step 2: Train the SRGAN
- **Objective**: Train SRGAN to generate 128x128 images from downscaled 32x32 images using `SRGAN_vchadala.ipynb`.
- **Preprocessing**: Images were downscaled to 32x32 for the generator input, with a target output of 128x128.
- **Training**: Both the generator and discriminator were trained iteratively for at least 150 epochs.
- **Output**: The generator and discriminator models were saved as `generator_epoch_150.keras` and `discriminator_epoch_150.keras` in the `models/` folder, with sample generated images in the `images/` folder.

#### Step 3: Train Model B (Binary Classifier on SRGAN Images)
- **Objective**: Train a new binary classifier (Model B) using the high-resolution images generated by SRGAN along with the original dataset, using `Model_B_vchadala.ipynb`.
- **Dataset**: The SRGAN-generated 128x128 images were combined with the original dataset to train Model B.
- **Training**: Similar to Model A, transfer learning with MobileNetV2 was used, fine-tuning the model on the SRGAN-enhanced dataset.
- **Output**: The trained model was saved as `mobilenetv2_model_b.h5` in the `models/` folder.

#### Step 4: Compare the Performance
- **Objective**: Evaluate and compare the performance of Model A and Model B to assess the impact of SRGAN-generated images on classification.
- **Metrics**: I used the following metrics:
  - **Accuracy**: The percentage of correct predictions.
  - **F1-score**: The harmonic mean of precision and recall.
  - **AUC (Area Under the Curve)**: To measure the ability of the model to distinguish between classes.
- **Visualization**: Plots of these metrics for both models were created to visualize performance differences.

### 5. Results and Evaluation

**Summary of Results**:
- **Accuracy Comparison**: Model B’s accuracy was compared to Model A’s to determine if the SRGAN-generated images led to improvements.
- **F1-score and AUC**: F1-score and AUC values for both models were analyzed to note significant differences.
- **Sample Images**: Sample images comparing low-resolution (32x32) and SRGAN-generated high-resolution (128x128) images are saved in the `images/` folder, showcasing the visual quality improvement.

### 6. References

- **SRGAN Paper**: Ledig, C., et al. "Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network." [Link](https://doi.org/10.48550/arXiv.1609.04802)
