# 🚢 Module 1 — Titanic: EDA + бинарная классификация

**Автор:** [Галямеев Михаил Русланович], [ПКТб-23-1]
**Дата обучения:** 26/27
**Датасет:** Titanic — Machine Learning from Disaster ([Kaggle](https://www.kaggle.com/c/titanic))

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC |
|--------|----------|-----------|--------|-----|---------|
| Logistic Regression | 0.8045 | 0.7833 | 0.6812 | 0.7287 | **0.8486** |
| Decision Tree | 0.7821 | 0.7419 | 0.6667 | 0.7023 | 0.8132 |
| Random Forest (бонус) | 0.8101 | 0.8302 | 0.6377 | 0.7213 | 0.8475 |

**Время обучения:** 0.0044 с (LR), 0.0026 с (DT), 0.2340 с (RF).
**Лучшая модель по ROC-AUC:** Logistic Regression (0.8486), цель ROC-AUC ≥ 0.80 достигнута.

## 📁 Структура

```
module-1-titanic/
├── README.md
├── notebook.ipynb              # отчёт из 14 разделов
├── requirements.txt
├── data/
│   ├── train.csv
│   ├── test.csv
│   └── titanic_info.md         # описание датасета
├── models/
│   ├── lr_model.pkl
│   ├── dt_model.pkl
│   ├── rf_model.pkl
│   ├── scaler.pkl
│   ├── le_sex.pkl
│   ├── feature_cols.json
│   └── metrics.json
└── examples/
    ├── eda_plots.png
    ├── roc_curves.png
    └── confusion_matrices.png
```

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/[username]/ml-course-galyameev/main/module-1-titanic"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/lr_model.pkl").content))
scaler = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/scaler.pkl").content))
```

Все подробности, графики и выводы — в [`notebook.ipynb`](./notebook.ipynb).
