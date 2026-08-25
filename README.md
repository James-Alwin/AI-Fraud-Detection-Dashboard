# 🛡️ AI-Powered Credit Card Fraud Detection Dashboard

## 📌 Project Overview

This project is a machine learning-powered credit card fraud detection system with an interactive web dashboard built using **FastAPI, HTML, Bootstrap, JavaScript, and Chart.js**.

The system trains **Random Forest** and **Logistic Regression** classification models, accepts transaction data through CSV upload, generates fraud predictions, and presents model analytics through a web dashboard.

## 🚀 Features

- Batch-wise fraud prediction
- Supports the Credit Card Fraud Detection dataset with **284,807 transactions**
- Random Forest fraud classification
- Logistic Regression model comparison
- Fraud vs. Legitimate transaction comparison
- Fraud trend visualization
- Random Forest feature-importance visualization
- Accuracy, Precision, Recall and F1-score
- Confusion Matrix
- ROC Curve comparison
- Random Forest vs. Logistic Regression AUC comparison
- Downloadable prediction results as CSV
- FastAPI-based backend and web dashboard

## 🧠 Machine Learning Models

### Random Forest Classifier

Random Forest is used as the primary prediction model in the dashboard.

```python
RandomForestClassifier(
    n_estimators=100,
    random_state=42,
    class_weight="balanced"
)
```

The `class_weight="balanced"` setting gives greater importance to the minority class in the highly imbalanced fraud dataset.

### Logistic Regression

Logistic Regression is trained as a comparison model.

```python
LogisticRegression(
    max_iter=1000,
    class_weight="balanced"
)
```

## 📊 Dataset

**Credit Card Fraud Detection Dataset — Kaggle**

Dataset statistics from the current training run:

- **Total transactions:** 284,807
- **Fraud cases:** 492
- **Target variable:** `Class`

The dataset is highly imbalanced, so the project evaluates the models using more than accuracy alone.

## 📈 Model Training Results

The current training script uses an **80/20 train-test split** with stratification.

### Random Forest

| Metric | Result |
|---|---:|
| Accuracy | **99.95%** |
| ROC-AUC | **0.9573** |

### Logistic Regression

| Metric | Result |
|---|---:|
| Accuracy | **97.12%** |
| ROC-AUC | **0.9735** |

> In the current training run, Random Forest achieved higher accuracy, while Logistic Regression achieved higher ROC-AUC.

## 🏗️ Project Architecture

```text
                    creditcard.csv
                          │
                          ▼
                   train_model.py
                          │
                ┌─────────┴─────────┐
                ▼                   ▼
          Random Forest       Logistic Regression
                │                   │
                └─────────┬─────────┘
                          ▼
                    Saved Models
                ┌─────────┴─────────┐
                ▼                   ▼
           rf_model.pkl        lr_model.pkl
                │                   │
                └─────────┬─────────┘
                          ▼
                        app.py
                       FastAPI
                          │
                          ▼
                   Web Dashboard
                          │
                     Upload CSV
                          │
                          ▼
                 Transaction Prediction
                          │
                          ▼
                  Analytics Dashboard
```

## 📁 Project Structure

```text
Fraud_Detection_DashBoard/
│
├── app.py
├── train_model.py
├── rf_model.pkl
├── lr_model.pkl
│
├── dataset/
│   └── creditcard.csv
│
├── templates/
│   ├── index.html
│   └── result.html
│
├── static/
│   ├── style.css
│   └── predictions.csv
│
└── README.md
```

## 🛠️ Tech Stack

- **Python**
- **Scikit-learn**
- **Pandas**
- **NumPy**
- **Joblib**
- **FastAPI**
- **Uvicorn**
- **Jinja2**
- **HTML / CSS / JavaScript**
- **Bootstrap**
- **Chart.js**

## ⚙️ Installation & Setup

### 1. Open the project directory

```powershell
cd J:\Fraud_Detection_DashBoard
```

### 2. Create a virtual environment

```powershell
python -m venv venv
```

### 3. Activate the virtual environment

```powershell
.\venv\Scripts\activate
```

### 4. Install dependencies

```powershell
pip install pandas numpy scikit-learn joblib fastapi uvicorn jinja2 python-multipart
```

## 📂 Dataset Setup

Create:

```text
dataset/
```

Place the dataset inside it:

```text
dataset/creditcard.csv
```

## 🧠 Train the Models

```powershell
python train_model.py
```

Training flow:

```text
Load Dataset
     ↓
Separate Features and Target
     ↓
80/20 Stratified Train-Test Split
     ↓
Train Random Forest
     ↓
Evaluate Random Forest
     ↓
Train Logistic Regression
     ↓
Evaluate Logistic Regression
     ↓
Save Models
```

After successful training:

```text
rf_model.pkl
lr_model.pkl
```

## 🚀 Run the FastAPI Application

```powershell
python app.py
```

Open:

```text
http://127.0.0.1:8000
```

## 📤 Using the Dashboard

1. Open `http://127.0.0.1:8000`.
2. Upload a compatible transaction CSV file.
3. FastAPI receives and reads the uploaded file.
4. Transaction data is processed in batches.
5. Random Forest generates predictions.
6. The dashboard displays the analysis.

The dashboard includes:

- Total transactions
- Fraudulent transactions
- Legitimate transactions
- Fraud trend
- Feature importance
- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- ROC Curve
- Model AUC comparison

## 📊 Model Evaluation

### Accuracy

```text
Accuracy = (TP + TN) / (TP + TN + FP + FN)
```

### Precision

```text
Precision = TP / (TP + FP)
```

### Recall

```text
Recall = TP / (TP + FN)
```

### F1-Score

```text
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

### ROC-AUC

ROC-AUC measures the model's ability to distinguish between fraudulent and legitimate transactions across classification thresholds.

## 🔲 Confusion Matrix

```text
                 Actual
              Fraud   Legit
Pred Fraud      TP      FP
Pred Legit      FN      TN
```

- **TP** — True Positive
- **TN** — True Negative
- **FP** — False Positive
- **FN** — False Negative

## ⚠️ Why Accuracy Alone Is Not Enough

The dataset contains:

```text
284,807 total transactions
492 fraudulent transactions
```

Because fraudulent transactions are a very small minority, accuracy alone may not fully describe fraud-detection performance.

The project therefore also evaluates:

- Precision
- Recall
- F1-score
- Confusion Matrix
- ROC-AUC

## 🔌 FastAPI API

The application also provides an API endpoint for individual transaction prediction.

The API returns a predicted class and fraud probability.

Example:

```json
{
    "prediction": 0,
    "fraud_probability": 0.0123
}
```

## 📥 Prediction Output

Prediction results can be downloaded as:

```text
predictions.csv
```

## 🔮 Future Improvements

- Hyperparameter tuning
- Cross-validation
- Additional classification models
- Feature engineering
- Advanced class-imbalance techniques
- Model explainability
- Authentication
- Database integration
- Cloud deployment
- Real-time transaction monitoring
- Automated model retraining

## 👨‍💻 Author

**James Alwin**

Machine Learning / Data Science Project
