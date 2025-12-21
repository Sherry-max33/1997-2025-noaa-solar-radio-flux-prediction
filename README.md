# ☀️ NOAA Solar Radio Flux Prediction (1997–2025)
*End-to-end analysis and prediction of NOAA solar activity data, combining **preprocessing**, **EDA**, **regression**, and **artificial neural networks (ANNs)** implemented in **Keras** and **PyTorch**.*

## 🧭 Project Overview

This project builds a **complete data science pipeline** to analyze and predict **daily solar radio flux (10.7 cm)** using historical solar activity indicators from *NOAA (1997–2025)*.

## 📊 Data Source

- **Provider:** the U.S. Dept. of Commerce, NOAA, Space Environment Center
- **Frequency:** Daily
- **Time Range:** 1997–2025
- **Format:** ASCII text files (yearly & quarterly)

**Target variable**
- `Radio_Flux_10.7_cm`
**Key predictors**
- Sunspot activity: `SESC_Sunspot_Number`, `Sunspot_Area`
- Solar flares: `XRay_C`, `XRay_M`, `XRay_X`
- Optical indicators

## 🧹 Preprocessing & Data Cleaning

### Raw file ingestion
- Extracted and inspected NOAA ASCII data using Linux command-line tools
### Data integration
- Merged yearly and quarterly files into a unified daily dataset
- Removed duplicated records caused by overlapping coverage
### Missing values
Converted sentinel and placeholder values (`-1`, `-999`, `*`) to proper missing values
### Outliers
Treated extreme `Sunspot_Area` values as missing to prevent distortion
### Imputation
- Dropped variables with excessive missingness
- Applied median imputation to sparse flare-related features

✅ Result: ~10,500 clean daily observations suitable for ML modeling

## 🔍 Exploratory Data Analysis (EDA)

EDA revealed several important patterns:
- Solar activity variables span very different numeric scales
- Flare variables are sparse count data
- Substantial temporal variability is evident over the observation period.

## 📈 Modeling Strategy

- **Classical Regression**
Provides a linear reference model

- **Artificial Neural Networks (ANN)**
Fully connected **MLP-style neural networks** were implemented in two frameworks to ensure robustness and framework-independent understanding.
**🔹 Keras**
- Dense layers: 32 → 16 → 1
- ReLU activations
- Adam optimizer
- Loss: MSE | Metric: MAE

**🔹 PyTorch**
- Custom `nn.Module` implementation
- Explicit training & validation loops
- Same architecture as Keras

## 🧪 Evaluation & Prediction
-Train/test split with feature standardization
-Metrics: **MSE** and **MAE**

Both **ANN models** produced consistent and stable predictions, with **performance exceeding linear baselines**.

## 💡 Key Insights

- Linear regression provides a strong baseline for solar radio flux prediction
- ANN models deliver modest error reductions over the linear baseline, suggesting additional structure beyond a purely linear relationship.
- Keras and PyTorch implementations produce comparable results when using aligned features and similar MLP architectures.

## 🛠️ Tech Stack

- **Linear Modeling:** lm, caret (based on R)  
- **Deep Learning:** Keras, PyTorch  
- **Data Processing & Visualization:** pandas, numpy, scikit-learn, ggplot2  
