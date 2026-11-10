# Phishing URL Detection Using Machine Learning

## Overview

This project focuses on developing an interpretable machine learning model to detect phishing URLs using the PhiUSIIL Phishing URL Dataset.

I use Logistic Regression with different regularization strategies to classify URLs as legitimate or phishing. I also investigate feature importance, model explainability using SHAP, and operational decision thresholds from a Security Operations Center (SOC) perspective.

The main objective is not only to achieve good classification performance but also to understand the model's decisions and evaluate its practical usefulness for phishing detection.

## Objectives

- Explore and analyze the phishing URL dataset.
- Perform data cleaning and feature preparation.
- Investigate correlations and relationships between features.
- Train and compare five Logistic Regression configurations.
- Evaluate models using classification metrics and confusion matrices.
- Investigate duplicate records and potential data leakage.
- Compare random and domain-based train-test splitting.
- Interpret model predictions using SHAP.
- Analyze classification thresholds for different SOC operational scenarios.

## Dataset

**Dataset:** PhiUSIIL Phishing URL Dataset

The dataset contains URL-related numerical and binary features describing domain characteristics, URL structure, and webpage properties.

- Total records: 235,795
- Unique domains: 220,086
- Features used: 49
- Target variable: `IsPhishing`
  - `0`: Legitimate URL
  - `1`: Phishing URL

**Dataset source:** [PhiUSIIL Phishing URL Dataset – Kaggle](https://www.kaggle.com/datasets/)

Download the dataset and place the CSV file in the appropriate location before executing the notebook.

## Technologies and Libraries

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- Scikit-learn
- SHAP
- Jupyter Notebook

## Project Methodology

### 1. Exploratory Data Analysis (EDA)

- Dataset structure and quality assessment.
- Missing values and duplicate records.
- Investigation of extreme values.
- Target variable definition and class distribution.
- Numerical and binary feature analysis.

### 2. Data Preprocessing

- Feature selection and removal of unnecessary textual columns.
- Target and feature separation.
- Correlation and multicollinearity analysis.
- Stratified train-test splitting.
- Feature standardization using StandardScaler.

### 3. Machine Learning and Evaluation

I compare five Logistic Regression configurations:

| Model | Configuration |
|---|---|
| M1 | Unregularized Logistic Regression |
| M2 | Strong L2 Regularization |
| M3 | Standard L2 Regularization |
| M4 | Sparse L1 Regularization |
| M5 | L2 Regularization with Balanced Class Weights |

Evaluation metrics:

- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC
- PR-AUC
- Confusion Matrix

I also investigate duplicate records, label consistency, and domain-based data splitting to assess potential data leakage and model generalization.

### 4. Model Explainability and SOC Threshold Analysis

I use SHAP to understand how individual features influence model predictions.

The analysis includes:

- Global feature importance using SHAP bar plots.
- Feature impact analysis using SHAP beeswarm plots.
- Local prediction explanations using waterfall plots.
- Investigation of True Positive, True Negative, and False Positive predictions.
- Decision threshold comparison:
  - 0.20: Threat Hunting Mode.
  - 0.50: Default Classification Mode.
  - 0.85: Automated Firewall Blocking Mode.

## Initial Model Results

The following results were obtained using the initial stratified random train-test split:

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| M1 – Unregularized | 0.9994 | 0.9996 | 0.9990 | 0.9993 | 0.9999948 |
| M2 – Strong L2 | 0.9976 | 0.9985 | 0.9958 | 0.9971 | 0.9999633 |
| M3 – Standard L2 | 0.9994 | 0.9996 | 0.9989 | 0.9992 | 0.9999920 |
| M4 – Sparse L1 | 0.9985 | 0.9993 | 0.9971 | 0.9982 | 0.9999795 |
| M5 – SOC Balanced | 0.9994 | 0.9995 | 0.9990 | 0.9992 | 0.9999925 |

**Important evaluation note:** These are initial random-split results. I identified 371 test records whose feature values also appeared in the training set. Although no conflicting labels were found, these overlapping records may inflate performance estimates. Domain-based evaluation is therefore included to investigate generalization to previously unseen domains.

## Repository Structure

```text
phishing-url-detection/
│
├── notebooks/
│   └── phishing_url_detection.ipynb
│
├── results/
│   ├── model_comparison.csv
│   ├── confusion_matrices/
│   └── shap_plots/
│
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## Installation and Usage

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/phishing-url-detection.git

cd phishing-url-detection
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Activate it:

**Linux/macOS:**

```bash
source venv/bin/activate
```

**Windows:**

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Download the dataset

Download the PhiUSIIL dataset from Kaggle and place the CSV file in the dataset location expected by the notebook.

### 5. Run the notebook

```bash
jupyter notebook
```

Open:

```text
notebooks/phishing_url_detection.ipynb
```

Execute the notebook cells sequentially.

## Future Improvements

- Evaluate models using domain-based validation.
- Investigate additional classification algorithms.
- Perform hyperparameter optimization.
- Improve generalization to previously unseen domains.
- Explore additional feature selection techniques.
- Integrate the detection model into a practical phishing analysis tool.
- Investigate deployment and integration with SOC monitoring workflows.

## Author

**Youssef Sarrad**

Cybersecurity | Machine Learning | Network Security

GitHub: [YOUR_GITHUB_PROFILE](https://github.com/YOUR_USERNAME)

---

*This project is developed for educational and research purposes. It demonstrates the application of machine learning and model explainability techniques to phishing URL detection.*