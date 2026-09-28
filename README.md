# 🌱 Soil Organic Carbon Prediction Using Multispectral & LiDAR Data

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Flask](https://img.shields.io/badge/Flask-Web%20App-green)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Ensemble-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 📌 Project Overview

This project presents a **machine learning-based web application for predicting Soil Organic Carbon (SOC)** in *Spartina alterniflora* wetlands using multispectral remote-sensing and LiDAR-derived terrain features.

The system uses **Particle Swarm Optimization (PSO)** for feature selection and a **weighted ensemble Voting Regressor** combining XGBoost, Gradient Boosting, LightGBM, and CatBoost models.

The trained model is integrated with a **Flask web application**, where users can enter the required environmental features and obtain an SOC prediction along with its SOC level classification.

---

## 🎯 Objectives

* Predict Soil Organic Carbon (SOC) using remote-sensing and terrain features.
* Select relevant features using Particle Swarm Optimization (PSO).
* Train and combine multiple machine learning regression models.
* Evaluate model performance using standard regression metrics.
* Deploy the trained model through a Flask web application.
* Provide an interactive interface for SOC prediction and visualization.

---

## 🔄 Project Workflow

```text
Raw SOC Dataset
       ↓
Data Preprocessing & Analysis
       ↓
Feature Selection using PSO
       ↓
14 Selected Features
       ↓
Train-Test Split (80:20)
       ↓
Multiple ML Regression Models
       ↓
Weighted Voting Regressor
       ↓
Model Evaluation
       ↓
Save Trained Model
       ↓
Flask Web Application
       ↓
User Inputs Feature Values
       ↓
SOC Prediction
       ↓
SOC Level Classification
```

---

## 🧠 Machine Learning Approach

### 1. Feature Selection — Particle Swarm Optimization

Particle Swarm Optimization (PSO) is an optimization technique inspired by the collective behavior of groups of particles.

In this project, PSO is used to identify relevant features for SOC prediction by optimizing the model's prediction error.

The PSO configuration used in the project includes:

* **Particles:** 10
* **Iterations:** 5
* **Optimization objective:** Minimize RMSE

---

### 2. Selected Features

The final model uses **14 features**.

#### Multispectral / Vegetation Features

| Feature | Description                                  |
| ------- | -------------------------------------------- |
| Green   | Green spectral band                          |
| RedEdge | Red-edge spectral band                       |
| NDVI    | Normalized Difference Vegetation Index       |
| GNDVI   | Green Normalized Difference Vegetation Index |
| NDRE    | Normalized Difference Red Edge               |
| EVI     | Enhanced Vegetation Index                    |
| SAVI    | Soil Adjusted Vegetation Index               |
| DVI     | Difference Vegetation Index                  |
| MSAVI   | Modified Soil Adjusted Vegetation Index      |
| SOS     | Start of Season                              |

#### LiDAR / Terrain Features

| Feature  | Description               |
| -------- | ------------------------- |
| Altitude | Elevation information     |
| Slope    | Terrain slope             |
| Aspect   | Direction of the slope    |
| Relief   | Local elevation variation |

### Target Variable

```text
SOC — Soil Organic Carbon
```

---

## 🤖 Machine Learning Models

The project uses multiple regression algorithms:

* XGBoost Regressor
* Gradient Boosting Regressor
* LightGBM Regressor
* CatBoost Regressor

These models are combined using a **Weighted Voting Regressor**.

### Ensemble Weights

| Model             | Weight |
| ----------------- | -----: |
| XGBoost           |      3 |
| Gradient Boosting |      1 |
| LightGBM          |      3 |
| CatBoost          |      2 |

The ensemble combines predictions from the individual models to generate the final SOC prediction.

---

## ⚙️ Model Configuration

The models use boosting-based configurations with parameters such as:

```text
n_estimators = 1200
learning_rate = 0.03
```

Additional model-specific parameters are defined in `retrain.py`.

---

## 📊 Model Evaluation

The project evaluates regression models using:

| Metric   | Purpose                                                         |
| -------- | --------------------------------------------------------------- |
| MAE      | Measures average absolute prediction error                      |
| RMSE     | Measures prediction error with greater penalty for large errors |
| MAPE     | Measures average percentage error                               |
| R² Score | Measures how well the model explains variation in SOC           |

The data is divided into:

```text
80% → Training
20% → Testing
```

using a fixed random state for reproducibility.

---

## 🌐 Web Application

The trained model is deployed using **Flask**.

The web application allows users to:

* Enter values for the 14 selected features.
* Generate an SOC prediction.
* View the predicted SOC value.
* Classify the prediction as Low, Medium, or High SOC.
* View previous predictions.
* Visualize prediction values using a heatmap.

### SOC Classification

| SOC Value | Classification |
| --------- | -------------- |
| `< 2`     | Low SOC        |
| `2 – <5`  | Medium SOC     |
| `≥ 5`     | High SOC       |

---

## 🗺️ Heatmap Visualization

The web application includes an interactive heatmap visualization for demonstration purposes.

The current prototype generates simulated latitude and longitude points around a predefined region and associates them with SOC prediction values.

> **Note:** The current heatmap is intended for visualization/demo purposes. It does not represent actual georeferenced SOC measurements. A production version could integrate actual UAV/LiDAR coordinates and spatial prediction data.

---

## 📁 Project Structure

```text
SOC-Prediction-in-Spartina-alterniflora/
│
├── app.py
├── model.sav
├── Notebook.ipynb
├── retrain.py
├── SOC_dataset.csv
├── processed.csv
├── report.log
│
└── templates/
    └── index.html
```

### File Description

| File                   | Description                                                     |
| ---------------------- | --------------------------------------------------------------- |
| `app.py`               | Flask web application and prediction logic                      |
| `model.sav`            | Saved trained Voting Regressor                                  |
| `Notebook.ipynb`       | Data analysis, feature selection, model training and evaluation |
| `retrain.py`           | Script for retraining and saving the model                      |
| `SOC_dataset.csv`      | Original SOC dataset                                            |
| `processed.csv`        | Processed dataset with selected features                        |
| `report.log`           | Training/output logs                                            |
| `templates/index.html` | Frontend interface                                              |

---

## 🛠️ Technologies Used

### Programming Language

* Python

### Machine Learning

* Scikit-learn
* XGBoost
* LightGBM
* CatBoost

### Optimization

* PySwarms / Particle Swarm Optimization

### Data Processing

* Pandas
* NumPy

### Web Development

* Flask
* HTML
* CSS
* JavaScript
* Bootstrap

### Visualization

* Matplotlib
* Seaborn
* Plotly
* Leaflet

### Model Persistence

* Joblib

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone <YOUR-GITHUB-REPOSITORY-URL>
```

Navigate to the project directory:

```bash
cd SOC-Prediction-in-Spartina-alterniflora
```

### 2. Install Required Libraries

```bash
pip install flask numpy pandas joblib scikit-learn xgboost lightgbm catboost pyswarms
```

### 3. Run the Flask Application

```bash
python app.py
```

### 4. Open the Application

Open the following address in your browser:

```text
http://127.0.0.1:5000
```

---

## 🔁 Retraining the Model

If you want to retrain the machine learning model using the processed dataset:

```bash
python retrain.py
```

The script:

1. Loads `processed.csv`
2. Selects the 14 input features
3. Separates features and target
4. Splits the dataset into training and testing sets
5. Creates the four regression models
6. Builds the weighted Voting Regressor
7. Trains the ensemble
8. Saves the trained model as `model.sav`

---

## 💡 How the Application Works

```text
User
 ↓
Enters 14 feature values
 ↓
Flask receives the input
 ↓
Input is converted into numerical format
 ↓
Saved ML model receives the input
 ↓
Voting Regressor predicts SOC
 ↓
SOC value is classified
 ↓
Result displayed on webpage
```

---

## 🔬 Example

A user provides values for:

```text
Green
RedEdge
NDVI
GNDVI
NDRE
EVI
SAVI
DVI
MSAVI
Altitude
Slope
Aspect
Relief
SOS
```

The application passes these values to the trained ensemble model.

Example result:

```text
Predicted SOC: 4.27
SOC Level: Medium SOC
```

---

## 🔮 Future Improvements

* Integrate real UAV multispectral and LiDAR datasets with geographic coordinates.
* Replace simulated heatmap points with actual spatial prediction data.
* Add automatic data preprocessing and validation.
* Implement model uncertainty estimation instead of a fixed confidence value.
* Add user authentication and prediction history storage using a database.
* Deploy the Flask application to a cloud platform.
* Add interactive GIS-based SOC prediction maps.
* Improve model tuning using automated hyperparameter optimization.

---

## 📚 Key Concepts

This project demonstrates practical knowledge of:

* Machine Learning
* Regression
* Ensemble Learning
* Feature Selection
* Particle Swarm Optimization
* Remote Sensing
* Multispectral Data
* LiDAR Data
* Data Preprocessing
* Model Evaluation
* Flask Deployment
* Web-based Machine Learning Applications

---

## 👩‍💻 Author

**Soundarya Patil**

Computer Science & Engineering Student

---

## 📄 License

This project is licensed under the **MIT License**.
