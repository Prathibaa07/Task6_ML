# Phishing URL Detection Using Decision Tree

## 📌 Project Overview

This project implements a **Machine Learning model for detecting phishing URLs** using a Decision Tree Classifier.

The project uses the **PhiUSIIL Phishing URL Dataset**, which contains URL and webpage-related features that can be used to distinguish between legitimate and phishing websites.

The notebook performs data loading, preprocessing, feature selection, train-test splitting, model training, prediction, and model evaluation.

## 📂 Dataset

**Dataset:** `PhiUSIIL_Phishing_URL_Dataset.csv`

The dataset contains:

- **13,394 records**
- **56 columns**
- URL-related and webpage-related features
- Target column: `label`

The original labels are:

- `0` → Phishing
- `1` → Legitimate

For model training, the labels are converted so that:

- `1` → Phishing
- `0` → Legitimate

The dataset initially contains 48 missing values, and the target distribution is 8,075 legitimate URLs and 5,318 phishing URLs.

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Google Colab / Jupyter Notebook

## 📦 Libraries

The following Python libraries are used:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.tree import DecisionTreeClassifier, plot_tree
from sklearn.metrics import (
    accuracy_score,
    precision_score,
    recall_score,
    f1_score,
    confusion_matrix,
    ConfusionMatrixDisplay
)
```

## 🔄 Project Workflow

### 1. Load the Dataset

The dataset is loaded using Pandas:

```python
df = pd.read_csv("PhiUSIIL_Phishing_URL_Dataset.csv")
```

The notebook examines the dataset shape, first few records, column names, missing values, and target distribution.

### 2. Data Preprocessing

Rows with missing target labels are removed.

The target variable is converted into the required format:

```python
y = (df["label"] == 0).astype(int)
```

Only numerical features are selected for model training. Infinite values are replaced with missing values, and missing feature values are filled using the corresponding column median.

After preprocessing, the feature matrix contains:

- **13,393 records**
- **50 numerical features**

The target contains 8,075 legitimate URLs and 5,318 phishing URLs.

### 3. Train-Test Split

The dataset is divided into training and testing sets using an 80:20 split.

```python
X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.20,
    random_state=42,
    stratify=y
)
```

The resulting datasets contain:

- **Training records:** 10,714
- **Testing records:** 2,679

### 4. Model Training

A **Decision Tree Classifier** is used.

```python
model = DecisionTreeClassifier(
    max_depth=5,
    class_weight="balanced",
    random_state=42
)
```

The model is trained using the training dataset.

The notebook also visualizes the trained Decision Tree with legitimate and phishing classes.

## 📊 Screenshot:
Confusion Matrix:

<img width="576" height="452" alt="Screenshot 2026-10-16 095427" src="https://github.com/user-attachments/assets/931ee09b-115a-48b3-b6fe-3b66dda2f23e" />


Phishing URL Detection:
<img width="1392" height="720" alt="Screenshot 2026-10-16 095403" src="https://github.com/user-attachments/assets/f20fa652-d1f1-45e8-91c8-9bec06f0e4e7" />


## 📊 Model Evaluation

The trained model is used to predict the test dataset.

```python
y_pred = model.predict(X_test)
```

The notebook evaluates the model using:

- Accuracy
- Precision
- Recall
- F1-score
- Specificity
- Confusion Matrix

The confusion matrix obtained is:

```text
[[1615    0]
 [   0 1064]]
```

This represents 1,615 correctly classified legitimate URLs and 1,064 correctly classified phishing URLs, with no false positives or false negatives in the reported test results.

### Final Results

| Metric | Score |
|---|---:|
| Accuracy | 1.0000 |
| Precision | 1.0000 |
| Recall | 1.0000 |
| F1-score | 1.0000 |
| Specificity | 1.0000 |

The notebook reports a score of **1.0000 (100%) for all five evaluation metrics**.

## 📁 Project Structure

```text
Project/
│__ NewFolder(2)
├── Task6_ML.ipynb
├── PhiUSIIL_Phishing_URL_Dataset.csv
└── README.md
```

## ▶️ How to Run

1. Download or clone the project.
2. Place `PhiUSIIL_Phishing_URL_Dataset.csv` in the same directory as the notebook.
3. Open `Task6_ML.ipynb` using:
   - Google Colab, or
   - Jupyter Notebook / JupyterLab.
4. Run the notebook cells sequentially.
5. The notebook will preprocess the data, train the Decision Tree model, generate predictions, and display evaluation results.

## 🎯 Objective

The main objective of this project is to build a machine learning-based system capable of classifying URLs as **phishing or legitimate** using URL and webpage characteristics.

## 📌 Conclusion

A Decision Tree Classifier was trained on numerical features from the PhiUSIIL phishing URL dataset. The notebook's reported test results show **100% accuracy, precision, recall, F1-score, and specificity**, with a confusion matrix containing no classification errors on the test set. 

> **Note:** These results are the outputs reported by the supplied notebook. They should be interpreted as evaluation results for this particular train/test split and model configuration.
