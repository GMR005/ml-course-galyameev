# Описание датасета Online Shoppers Purchasing Intention

**Источник:** UCI Machine Learning Repository, ID 468
**Оригинальный файл:** `online_shoppers_intention.csv`
**Авторы:** C. O. Sakar, S. Polat, M. Katircioglu, Y. Kastro
**Год:** 2018
**Лицензия/условия:** открытый датасет UCI для исследовательских целей

## Общая информация

| Параметр | Значение |
|----------|----------|
| Всего записей (сессий) | 12330 |
| Исходных признаков | 17 |
| Целевая переменная | `Revenue` (bool) |
| Пропуски | отсутствуют |
| Числовых признаков | 10 |
| Категориальных/логических | 7 (`Month`, `VisitorType`, `Weekend` и технические ID) |
| Тип задачи | бинарная классификация |

## Распределение классов

| Класс | Количество | Доля |
|-------|------------|------|
| `False` — нет покупки | 10422 | 84,53% |
| `True` — покупка | 1908 | 15,47% |

Дисбаланс сильный, поэтому в работе используются `class_weight='balanced'`,
`scale_pos_weight`, `auto_class_weights='Balanced'`, а основная метрика — ROC-AUC.

## Структура признаков

| Тип | Признаки |
|-----|----------|
| Числовые: административные | `Administrative`, `Administrative_Duration` |
| Числовые: информационные | `Informational`, `Informational_Duration` |
| Числовые: товарные | `ProductRelated`, `ProductRelated_Duration` |
| Числовые: метрики качества | `BounceRates`, `ExitRates`, `PageValues`, `SpecialDay` |
| Категориальные: технические | `OperatingSystems`, `Browser`, `Region`, `TrafficType` |
| Категориальные: поведенческие | `VisitorType`, `Weekend` |
| Временные | `Month` |
| Целевая | `Revenue` |

## Созданные признаки

| Признак | Формула / смысл |
|---------|-----------------|
| `TotalPages` | `Administrative + Informational + ProductRelated` |
| `TotalDuration` | сумма длительностей по трём типам страниц |
| `AvgPageValue` | `PageValues / (TotalPages + 1)` |
| `BounceExitRatio` | `BounceRates / (ExitRates + 0.001)` |
| `IsNewVisitor` | `VisitorType == 'New_Visitor'` |
| `IsWeekend` | `Weekend` в формате 0/1 |
| `MonthNum` | номер месяца 1–12 (словарь обрабатывает `June`) |
| `IsHighTraffic` | `TrafficType > 10` |

После One-Hot Encoding `VisitorType` и `Month` итоговое число признаков — 36.

## Разбиение

- train: 9864 сессий
- test: 2466 сессий
- Пропорция 80/20, `stratify=y`, `random_state=42`

## Файлы

- `data/online_shoppers_intention.csv` — исходные данные
- `data/dataset_info.md` — это описание
