# Module 3 — Customer Churn: ансамблевые методы

**Автор:** Галямеев Михаил Русланович, ПКТб-23-1
**Дисциплина:** Машинное обучение (продвинутый уровень)
**Дата:** 2026-10-26
**Ноутбук:** [`notebook.ipynb`](./notebook.ipynb)

## Результаты

| Модель | Accuracy | Precision | Recall | F1 | ROC-AUC | Время обучения |
|--------|----------|-----------|--------|-----|---------|----------------|
| Random Forest | 0.7722 | 0.5575 | 0.6872 | 0.6156 | 0.8403 | 0.238 сек |
| XGBoost | 0.7637 | 0.5424 | 0.7005 | 0.6114 | 0.8316 | 0.132 сек |
| LightGBM | 0.7601 | 0.5344 | 0.7487 | 0.6236 | 0.8379 | 0.120 сек |
| CatBoost | 0.7559 | 0.5279 | 0.7594 | 0.6228 | 0.8381 | 0.616 сек |
| **LightGBM (Optuna)** | **0.7445** | **0.5119** | **0.8021** | **0.6250** | **0.8465** | — |

Лучшая модель — **LightGBM после Optuna**: ROC-AUC 0.8465, прирост +0.86 п.п. относительно baseline LightGBM (0.8379). Optuna выполнила 30 испытаний с 5-fold StratifiedKFold; лучший CV ROC-AUC — 0.8487.

## Что внутри

- `notebook.ipynb` — полный отчёт из 14 разделов с выполненными ячейками и графиками.
- `data/telco_churn.csv` — датасет Telco Customer Churn (7043 × 21).
- `data/churn_info.md` — описание датасета и признаков.
- `models/` — четыре baseline-модели, лучшая модель, scaler, кодировщики, список признаков и метрики.
- `examples/` — EDA, матрица ошибок, ROC-кривые, Feature Importance и SHAP-графики.

## Быстрый старт

```bash
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

## Загрузка лучшей модели из репозитория

```python
import joblib
import requests
from io import BytesIO

BASE_URL = "https://raw.githubusercontent.com/GMR005/ml-course-galyameev/main/module-3-churn"
model = joblib.load(BytesIO(requests.get(f"{BASE_URL}/models/best_model.pkl").content))
```

Если raw-ссылка ещё не опубликована, ноутбук автоматически использует локальную копию из `models/` и явно сообщает об этом.

## Ключевые выводы

- Тип контракта — главный драйвер оттока: Month-to-month 42.71%, One year 11.27%, Two year 2.83%.
- Первые 6–12 месяцев — критическое окно: 52.94% оттока в первые 6 месяцев против 9.51% после 49 месяцев.
- Fiber optic связан с повышенным риском (41.89% против 18.96% у DSL).
- Отсутствие OnlineSecurity и TechSupport повышает риск примерно в 2.7–2.8 раза.
- Для удержания важнее Recall: лучшая модель находит 80.21% уходящих клиентов, но требует настройки порога под стоимость ошибок.

## Источник данных

Telco Customer Churn: https://www.kaggle.com/datasets/blastchar/telco-customer-churn
