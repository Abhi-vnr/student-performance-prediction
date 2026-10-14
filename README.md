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
