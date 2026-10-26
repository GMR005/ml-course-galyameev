# Telco Customer Churn — описание датасета

**Источник:** https://www.kaggle.com/datasets/blastchar/telco-customer-churn

## Основные характеристики

- Всего записей: 7043
- Всего столбцов: 21
- Признаков без customerID и Churn: 19
- Целевая переменная: Churn
- Класс No (остался): 5174 (73.46%)
- Класс Yes (ушёл): 1869 (26.54%)

## Пропуски

- TotalCharges: 11 пустых значений (0.16%).
- Остальные столбцы не содержат пропусков.

## Признаки

- Демографические: gender, SeniorCitizen, Partner, Dependents.
- Услуги: PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup,
  DeviceProtection, TechSupport, StreamingTV, StreamingMovies.
- Аккаунт: Contract, PaperlessBilling, PaymentMethod, MonthlyCharges, TotalCharges, tenure.

## Особенности

- TotalCharges хранится как object и требует pd.to_numeric(errors='coerce').
- Выраженный дисбаланс классов: примерно 73.5% / 26.5%.
- Для задачи используются ансамблевые модели: Random Forest, XGBoost, LightGBM, CatBoost.
