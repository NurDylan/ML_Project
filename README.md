# Indoor Localization Using WLAN Fingerprinting: Comparative Study of Machine Learning Models

A comparative machine learning project evaluated on the UJIIndoorLoc dataset. This repository implements a unified data preprocessing pipeline alongside multiple machine learning models—ranging from baseline statistical methods to advanced deep learning architectures—to tackle both indoor location classification and coordinate regression.  

## Project Overview
Global Positioning System (GPS) signals are often weak or unavailable inside complex architectural structures due to signal attenuation and physical barriers. This project utilizes WLAN/WiFi Fingerprinting (measuring Received Signal Strength Indicators (RSSI) from surrounding Access Points (APs)) to determine user positioning accurately without specialized hardware. 

The project addresses two distinct tasks:
* **Classification (Building & Floor):** Predicts discrete locations (13 unique Building-Floor combinations) using signal fingerprints.
* **Regression (Longitude & Latitude):** Predicts exact continuous 2D spatial coordinates.

## Dataset
The project uses the UJIIndoorLoc benchmark dataset from the UCI Machine Learning Repository:  
**Training Set:** 19,937 samples (reduced to 19,300 after duplicate removal)  
**Validation Set:** 1,111 samples  
**Features:** 520 Wireless Access Points (WAPs)  

## Shared Data Preprocessing Pipeline
To ensure unbiased and reproducible evaluations across all models, a common preprocessing pipeline was applied:  
**Duplicate Removal:** Removed 637 exact duplicate records from the training data.  
**Handling Missing/Undetected Signals:** Replaced dummy non-detection values (100) with -110 dBm to realistically represent weak/absent signals.  
**Feature Reduction:** Dropped 55 non-informative WAP features never detected in the training set, reducing feature dimensionality from 520 to 465.  
**Normalization & Scaling:** Standardized the RSSI values using StandardScaler (fitted exclusively on training data to prevent leakage).  

### 1. Classification (Building & Floor)

| Model | Type | Accuracy | Macro F1-Score |
| :--- | :--- | :---: | :---: |
| **Logistic Regression** | Baseline | 88.48% | 0.8746 |
| **Linear SVM** | Baseline | 85.15% | 0.8222 |
| **1D CNN** | Advanced | 99.50% | — |

---

### 2. Regression (Longitude & Latitude Coordinates)

| Model | Type | MAE (meters) | RMSE (meters) |
| :--- | :--- | :---: | :---: |
| **K-Nearest Neighbors (KNN)** | Baseline | ~8.00 m | ~15.00 m |
| **Gradient Boosting Regressor** | Advanced | 20.14 m | 29.60 m |
| **Deep Neural Network (DNN)** | Advanced | 7.08 m | 11.31 m |

## Contributors & Responsibilities
* Nur Afiqah — Advanced Classification (1D CNN) & Basic Regression (KNN)
* Raneem Alhamaydah — Data Preprocessing Pipeline, Basic Classification (Linear SVM) & Advanced Regression (DNN)
* Jawaher Al-Aji — Basic Classification (Logistic Regression) & Advanced Regression (Gradient Boosting) 
