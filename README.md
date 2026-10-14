# Student Performance Prediction

A machine learning project that explores student data and predicts final mathematics grades and Pass/Fail outcomes using regression and classification.

## Project Objectives

- Explore student demographic, family, and study-related attributes.
- Predict final mathematics grades using regression.
- Classify students as Pass or Fail using Logistic Regression.
- Evaluate model performance using appropriate metrics.

## Dataset

The project uses the Student Performance dataset from the UCI Machine Learning Repository.

- Dataset: Student Performance
- Records: 395
- Features: 33 columns in the original mathematics dataset
- Target: G3 (final mathematics grade, from 0 to 20)
- Pass threshold: G3 >= 10

Source: https://archive.ics.uci.edu/dataset/320/student%2Bperformance

Reference:
Cortez, P. and Silva, A. (2008). Using Data Mining to Predict Secondary School Student Performance.

## Models and Results

### Linear Regression

The regression model uses selected student-related features and excludes G1 and G2 to avoid using earlier grades as predictors.

| Metric | Result |
|---|---:|
| MAE | 3.49 |
| RMSE | 4.25 |
| R² | 0.118 |

The model has limited predictive power, so its predictions should be interpreted cautiously.

### Logistic Regression: Pass/Fail

The classification target is defined as Pass when G3 >= 10 and Fail otherwise.

Original model:

| Metric | Result |
|---|---:|
| Accuracy | 65.8% |
| Pass precision | 70.3% |
| Pass recall | 84.9% |
| Pass F1-score | 0.77 |
| Fail recall | 26.9% |

Class-weighted model:

| Metric | Result |
|---|---:|
| Accuracy | 63.3% |
| Fail precision | 45% |
| Fail recall | 54% |
| Fail F1-score | 0.49 |
| Pass precision | 75% |
| Pass recall | 68% |
| Pass F1-score | 0.71 |

Class weighting improved detection of failing students, while reducing overall accuracy. This demonstrates a trade-off between overall performance and identifying at-risk students.

## Project Structure

```text
student-performance-prediction/
├── data/
│   └── raw/
│       └── student-mat.csv
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_regression_model.ipynb
│   └── 03_logistic_regression.ipynb
├── reports/
├── .gitignore
├── README.md
└── requirements.txt
```


after------------------

## Models and Results

### 1. Regression — Predicting Final Grade

We compared a mean baseline, Linear Regression, Ridge Regression, Random Forest, and Extra Trees using the same train/test split.

| Model | MAE | RMSE | R² |
|---|---:|---:|---:|
| Random Forest | **3.306** | **4.055** | **0.198** |
| Extra Trees | 3.417 | 4.275 | 0.109 |
| Ridge Regression | 3.489 | 4.253 | 0.118 |
| Linear Regression | 3.490 | 4.253 | 0.118 |
| Mean Baseline | 3.646 | 4.550 | -0.010 |

Random Forest achieved the lowest test MAE and RMSE among the models tested. However, its R² of 0.198 indicates limited predictive power.

A tuned Random Forest achieved a test MAE of 3.320 and R² of 0.189, so the original Random Forest remained the stronger model on this test split.

### 2. Classification — Pass/Fail Prediction

Students were classified as Pass when the final mathematics grade (G3) was at least 10, and Fail otherwise. Models were compared using stratified train/test splitting and five-fold cross-validation on the training set.

| Model | Test Accuracy | Fail Recall | Fail F1 |
|---|---:|---:|---:|
| Decision Tree | **65.8%** | 50.0% | **0.491** |
| Balanced Logistic Regression | 63.3% | **53.8%** | **0.491** |
| Random Forest | 64.6% | 50.0% | 0.481 |
| Extra Trees | 63.3% | 42.3% | 0.431 |
| Logistic Regression | 65.8% | 26.9% | 0.341 |

The Decision Tree provided a balance between overall accuracy and detecting failing students. Balanced Logistic Regression identified a slightly larger proportion of failing students, illustrating the trade-off between overall accuracy and failure detection.

The confusion matrices are saved at `reports/figures/classification_confusion_matrices.png`.

### Evaluation and Limitations

- The dataset contains 395 students, which limits how confidently results can generalize.
- Regression models excluded G1 and G2 to avoid using earlier exam grades as predictors.
- Regression performance was modest, and the classification models missed a substantial number of failing students.
- Results depend on the train/test split; cross-validation was used for classification model comparison.
- Predictions should support further investigation, not be the sole basis for academic decisions.

## Setup

Python 3.11 is recommended.

1. Clone the repository.
2. Create and activate a virtual environment.
3. Install dependencies.
4. Launch Jupyter Notebook.

```bash
python -m venv .venv
```

Windows Git Bash:

```bash
source .venv/Scripts/activate
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
jupyter notebook
```

Open the notebooks in numerical order and run their cells.

## Limitations

- The dataset is relatively small.
- Results are based on a single train/test split.
- Classification performance is weaker for the Fail class than for the Pass class.
- The models show associations in the dataset and do not establish that any feature causes a particular academic outcome.
- Predictions should not be used as the sole basis for decisions about students.

## License and Dataset Attribution

Please refer to the UCI dataset page for dataset terms and citation requirements. This repository is an educational machine learning project.
