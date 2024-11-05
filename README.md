# SRGAN

# SRGAN for Super-Resolution

A Super-Resolution Generative Adversarial Network (SRGAN) to upscale low-resolution images to high-resolution images, specifically designed for binary classification tasks (e.g., classifying cats vs. dogs). This README will guide you through the project setup, training process, and usage.

## Table of Contents
1. [Introduction](#introduction)
2. [Project Structure](#project-structure)
3. [Getting Started](#getting-started)
4. [Training Process](#training-process)
5. [Results and Evaluation](#results-and-evaluation)
6. [Usage](#usage)
7. [References](#references)

### 1. Introduction

This project implements an SRGAN to generate high-resolution images from low-resolution inputs, which are then used in a binary classification problem. SRGAN combines GANs and convolutional neural networks (CNNs) to generate realistic high-resolution images from low-resolution images. This can be useful in applications like medical imaging, satellite imagery, and object detection.

### 2. Project Structure

The project is organized as follows:

- `models/` - Contains saved model files (`Model_A.h5`, `SRGAN.h5`, `Model_B.h5`).
- `notebooks/` - Jupyter Notebooks used for training SRGAN and the classification models.
- `images/` - Sample images generated by SRGAN for demonstration purposes.
- `docs/` - Documentation files, including this README.

### 3. Getting Started

#### Prerequisites
- Python 3.x
- Install required libraries:
  ```bash
  pip install tensorflow keras matplotlib numpy

  ### 4. Training Process

This project involves the following main steps:

#### Step 1: Train Model A (Binary Classifier)
- **Objective:** Train a binary classifier (Model A) on the original dataset images using transfer learning.
- **Preprocessing:** Resize all images to 128x128 resolution, and apply normalization and any necessary data augmentations.
- **Training:** Use a pre-trained model (e.g., MobileNetV2) and fine-tune it for binary classification (e.g., cats vs. dogs).
- **Output:** Save the trained model as `Model_A.h5` in the `models/` folder.

#### Step 2: Train the SRGAN
- **Objective:** Train the SRGAN to generate 128x128 images from downscaled 32x32 images.
- **Preprocessing:** Downscale training images to 32x32 as input for the generator network, with 128x128 as the target output resolution.
- **Training:** Train both the generator and discriminator iteratively for at least 150 epochs. Save intermediate outputs for evaluation.
- **Output:** Save the trained SRGAN model as `SRGAN.h5` in the `models/` folder and some sample generated images in the `images/` folder.

#### Step 3: Train Model B (Binary Classifier on SRGAN Images)
- **Objective:** Train a new binary classifier (Model B) using the high-resolution images generated by the SRGAN.
- **Dataset:** Use the SRGAN to generate 128x128 images from the 32x32 downscaled images and use these images to train Model B.
- **Training:** Similar to Model A, use transfer learning (e.g., MobileNetV2) to fine-tune the binary classifier on the SRGAN-generated dataset.
- **Output:** Save the trained model as `Model_B.h5` in the `models/` folder.

#### Step 4: Compare the Performance
- **Objective:** Evaluate and compare the performance of Model A and Model B to determine if the SRGAN-generated images improved the classifier performance.
- **Metrics:** Use the following metrics for evaluation:
  - **Accuracy:** The percentage of correct predictions.
  - **F1-score:** The harmonic mean of precision and recall, which balances both false positives and false negatives.
  - **AUC (Area Under the Curve):** Measures the ability of the model to distinguish between classes.
- **Visualization:** Plot these metrics for both models to visualize the differences in performance.

### 5. Results and Evaluation

Provide a summary of the results, including comparisons between Model A and Model B:

- **Accuracy Comparison:** Mention the accuracy of both models and whether Model B (trained on SRGAN-generated images) shows improvement over Model A.
- **F1-score and AUC:** Include F1-score and AUC values for both models and note any significant differences.
- **Sample Images:** Display a few examples of low-resolution (32x32) vs. SRGAN-generated high-resolution (128x128) images in the `images/` folder to showcase the visual quality.

### 6. Usage

#### Running the Code
1. Open the Jupyter Notebooks in `notebooks/`.
2. Follow the steps in each notebook:
   - **`SRGAN_Training.ipynb`:** For training the SRGAN model.
   - **`Model_A_Training.ipynb`:** For training Model A on the original high-resolution dataset.
   - **`Model_B_Training.ipynb`:** For training Model B on SRGAN-generated images.

3. **Evaluation Notebook:** Create a notebook (e.g., `Evaluation.ipynb`) to run the evaluation metrics on both models and compare the results.

#### Example Command
If running on a terminal or command line, save the Jupyter notebooks as Python scripts and execute them, or use the notebooks directly.

### 7. References

- **SRGAN Paper:** Ledig, C., et al. "Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network."
- **Keras Documentation:** [Keras - Deep Learning for Humans](https://keras.io/)

