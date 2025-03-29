# Fatty-Liver-Analysis

# Fatty Liver Classification using PyTorch

## Overview
Non-alcoholic fatty liver disease (NAFLD) is an increasingly important cause of fibrosis and hepatocellular carcinoma. Liver biopsy remains the gold standard to evaluate fibrosis in patients with NAFLD. Accurate and noninvasive diagnosis of advanced fibrosis in NAFLD patients is necessary for disease monitoring, treatment selection, and risk stratification.

This project focuses on classifying fatty liver disease using a neural network implemented in PyTorch. The dataset consists of various features, including BMI and sex, with a target label indicating whether the liver is fatty or not.

We constructed and validated a simple model, LiveFbr, using 9 routine clinical blood test parameters to detect advanced fibrosis in liver-biopsy proven NAFLD patients. Its diagnostic ability was evaluated across one discovery set and two independent validation sets, consistently outperforming existing indexes such as FIB-4 and NAFLD Fibrosis Score (NFS).

## Dataset
The dataset consists of two CSV files:
- `train.csv`: Training dataset
- `test.csv`: Testing dataset

Columns removed from the dataset:
- `Unnamed: 0`
- `FBID`
- `SampleID`
- `Fibrosis`
- `group`

The data contains 20 clinical indexes of ~800 patients with liver fibrosis.

## Preprocessing Steps
- Convert all values to numeric format.
- Handle missing values by dropping rows with NaN values.
- Encode categorical variable `Sex` using Label Encoding.
- Create a label column if missing, based on BMI threshold (> 25 indicates fatty liver).
- Normalize the dataset using `StandardScaler`.

## Model Architecture
A fully connected neural network with the following layers:
- Input layer: Dynamically set based on dataset features.
- Hidden Layers:
  - Fully connected (128 neurons) + BatchNorm + ReLU + Dropout (0.5)
  - Fully connected (64 neurons) + BatchNorm + ReLU + Dropout (0.5)
- Output layer: 1 neuron (no activation, as BCEWithLogitsLoss is used)

Additionally, models such as Linear Regression, Random Forest, and Gradient Boosting have been constructed and evaluated in R.

## Training Details
- Optimizer: AdamW (learning rate: 0.001, weight decay: 5e-4)
- Loss Function: Binary Cross Entropy with Logits
- Learning Rate Scheduler: ReduceLROnPlateau (factor 0.1, patience 3)
- Early Stopping: Stops training if validation loss does not improve for 5 consecutive epochs.

## Results
Training achieved a high accuracy:
Best Testing Accuracy: **95.92%**


