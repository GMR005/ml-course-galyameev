# 🏠 Module 2 — House Prices: предобработка данных и регрессия

**Автор:** Галямеев Михаил Русланович, ПКТб-23-1  
**Дата обучения:** 2026-10-13  
**Датасет:** House Prices — Advanced Regression Techniques ([Kaggle](https://www.kaggle.com/c/house-prices-advanced-regression-techniques))  
**Задача:** регрессия — предсказание цены продажи дома (`SalePrice`).

## 📊 Результаты

Метрики на тестовой выборке (20% train, `random_state=42`); обучение на
`np.log1p(SalePrice)`.

| Модель | RMSE (log) | MAE (log) | R² | RMSE ($) | MAE ($) | Время (с) |
|--------|-----------|-----------|-----|----------|---------|-----------|
| Linear Regression | 0.1256 | 0.0897 | 0.8936 | $22 787 | $15 533 | 0.028 |
| Ridge (alpha=100.0) | 0.1251 | 0.0894 | 0.8945 | $22 717 | $15 488 | 0.003 |
| Lasso (alpha=0.003) | 0.1222 | 0.0852 | 0.8993 | $22 008 | $14 727 | 0.071 |
| ElasticNet (**лучшая**) | 0.1186 | 0.0787 | **0.9051** | **$20 252** | **$13 421** | 0.058 |

- **Лучшая модель:** ElasticNet (`alpha=0.005`, `l1_ratio=0.7`), выбрана по
  5-фолдовой кросс-валидации. R² (log) = **0.9051**, R² в долларах = 0.9186.
- **Lasso** обнулил 44 из 220 признаков (оставил 176 значимых).
- Гиперпараметры подобраны через `GridSearchCV`.
- Подробные метрики — в [`models/metrics.json`](./models/metrics.json).

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO
import json

BASE_URL = "https://raw.githubusercontent.com/[username]/ml-course-galyameev/main/module-2-house-prices"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))
scaler = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/scaler.pkl").content))
feature_cols = requests.get(f"{BASE_URL}/models/feature_cols.json").json()
```

Загрузка и инференс без переобучения продемонстрированы в разделе 11 ноутбука.

## 📁 Структура

```
module-2-house-prices/
├── README.md
├── notebook.ipynb              # отчёт из 14 разделов
├── requirements.txt
├── data/
│   ├── train.csv
│   ├── test.csv
│   └── house_prices_info.md    # описание датасета
├── models/
│   ├── best_model.pkl          # ElasticNet (лучшая)
│   ├── lr_model.pkl
│   ├── ridge_model.pkl
│   ├── lasso_model.pkl
│   ├── enet_model.pkl
│   ├── scaler.pkl
│   ├── feature_cols.json
│   └── metrics.json
└── examples/
    ├── eda_plots.png
    ├── predictions_scatter.png
    └── residuals.png
```

## 📝 Кратко о пайплайне

1. EDA: распределение целевой до/после `log1p`, корреляции, пропуски.
2. Обработка пропусков: смысловые → `"None"`, связанные → `0`,
   `LotFrontage` → медиана по району, остальные → мода/медиана.
3. Обработка выбросов: IQR + доменные знания (`GrLivArea > 4000`).
4. Feature Engineering: `TotalSF`, `TotalBath`, `TotalPorch`, `HouseAge`,
   `RemodAge`, бинарные признаки, `OverallQual_TotalSF`.
5. Кодирование: порядковые → Label, номинальные → One-Hot.
6. Обучение 4 моделей, 5-фолдовая CV и `GridSearchCV`.
7. Оценка (RMSE/MAE/R²), интерпретация коэффициентов, функция `predict_price()`.
