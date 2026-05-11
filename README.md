# Flatness Prediction from CNC Data  
Machine Learning • CNC Machining • Quality Control

This project predicts the final flatness of a camhousing surface after CNC operation OP20 using measurement and process data collected during OP10.  
The dataset contains **95 real production samples**, collected directly from a CNC machining line.

---

## 🎯 Project Objective

The goal is to build a regression model that predicts **surface flatness after OP20** based on:

- geometric measurements from 8 control points after OP10,
- machining parameters (feed rate, spindle speed, tool plunge difference),
- clamping pressures,
- clamping sequence (One‑Hot encoded),
- production shift.

This enables early detection of potential nonconformities, reduces rework, and improves process stability.

---

## 🧩 Dataset Overview

The dataset includes **17 input features** and **1 target variable**:

### Geometry (mm)
- `pkt_1` … `pkt_8` — height measurements at 8 reference points

### Machining parameters
- `Feedrate` [mm/min]  
- `SpindleSpeed` [rpm]  
- `ToolPlungeDiff` [mm]

### Clamping parameters
- `ClampPressure_1` [MPa]  
- `ClampPressure_2` [MPa]  
- `BasePressure` [MPa]

### Categorical (encoded)
- `Sequence_1111`  
- `Sequence_1234`  
- `Sequence_4321`

### Target
- `Flatness` [mm]

All features were converted to `float64` for consistent numerical processing.

---

## 🔍 Exploratory Data Analysis

### Key findings
- Strongest correlations with flatness: **pkt_1, pkt_2, pkt_8**  
- Machining parameters show moderate influence  
- Clamping pressures affect deformation during fixturing  
- Clamping sequence impacts final geometry  
- Flatness distribution peaks around **0.030 mm**, with clusters near **0.020 mm** and **0.040 mm**

---

## 🏗️ Machine Learning Pipeline

1. Convert all features to numeric  
2. One‑Hot encode clamping sequences  
3. Train/test split (80/20)  
4. Train regression models:
   - KNN Regressor  
   - Linear Regression  
   - Random Forest  
   - Gradient Boosting  
   - SVR  
5. Evaluate using:
   - MSE, RMSE  
   - R²  
   - MAE  
   - MAPE  
   - Cross‑Validation Mean  

---

## 📊 Model Performance

| Model              | R²   | RMSE | MAE | MAPE |
|-------------------|------|------|-----|------|
| **KNN Regressor** | **0.53** | 0.01 | 0.00 | 0.18 |
| Linear Regression | 0.52 | 0.01 | 0.01 | 0.19 |
| Gradient Boosting | 0.48 | 0.01 | 0.00 | 0.18 |
| Random Forest     | 0.47 | 0.01 | 0.00 | 0.18 |
| SVR               | 0.00 | 0.01 | 0.01 | 0.24 |

**Best model: KNN Regressor (R² = 0.53)**  
Performs best on this small, nonlinear dataset.

---

## 🧠 Industrial Conclusions

- Flatness after OP20 is strongly driven by OP10 geometry  
- Clamping pressures and sequence significantly influence deformation  
- Machining parameters also contribute  
- ML enables predictive quality control before OP20  
- The project can be extended into a real‑time monitoring tool

---

## 📁 Repository Structure

