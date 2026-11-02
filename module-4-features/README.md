# 🛒 Module 4 — Online Shoppers: Инженерия признаков

**Автор:** Галямеев М.Р., ПКТб-23-1
**Дата:** 2026-11-02

## 📊 Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время |
|--------|----------|-----------|--------|-----|---------|-------|
| Random Forest | 0,8735 | 0,5689 | 0,7565 | 0,6494 | 0,9272 | 0.32 сек |
| XGBoost | 0,8856 | 0,6092 | 0,7304 | 0,6643 | 0,9235 | 0.24 сек |
| LightGBM | 0,8743 | 0,5672 | 0,7958 | 0,6623 | 0,9277 | 0.16 сек |
| CatBoost | 0,8694 | 0,5549 | 0,7932 | 0,6530 | 0,9274 | 0.69 сек |
| **LightGBM (Optuna)** | **0,8625** | **0,5355** | **0,8482** | **0,6565** | **0,9322** | — |

**Лучшая модель:** LightGBM после Optuna, ROC-AUC = **0,9322** (baseline 0,9277, прирост +0,48%).

## 🚀 Быстрый старт

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/GMR005/ml-course-galyameev/main/module-4-features"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))
```

## 📁 Структура

- `notebook.ipynb` — полный отчёт (14 разделов)
- `models/` — 5 моделей, scaler и метаданные
- `data/` — датасет и описание
- `examples/` — графики EDA, ROC, Feature Importance и SHAP

## 📦 Данные

- **Источник:** UCI ML Repository (ID 468), `online_shoppers_intention.csv`
- **Объём:** 12330 сессий, 17 исходных признаков + `Revenue`
- **Дисбаланс:** 84,53% / 15,47%
- **После Feature Engineering:** 36 признаков
