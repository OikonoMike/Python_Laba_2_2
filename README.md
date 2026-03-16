# Лабораторная работа №2. Модель задачи: дескрипторы и @property

---

## Структура репозитория
```
Python_Laba_2_2/
├── src/
│   ├── __init__.py
│   ├── models.py          # Модель задачи с дескрипторами и контракт для источников
│   ├── descriptors.py     # Пользовательские дескрипторы для валидации атрибутов задачи
│   ├── exceptions.py      # Исключения для задач платформы
│   ├── sources.py         # Источники задач
│   ├── collector.py       # Сборщик (который теперь генерирует ID)
│   ├── logger.py          # Логирование
│   └── main.py            # Основной файл запуска
├── tests/
│   ├── __init__.py
│   └── test_for_all.py    # Тесты
├── .gitignore
├── .pre-commit-config.yaml
├── pyproject.toml
├── README.md
└── requirements.txt
```
---

## Цель работы

Освоить управление доступом к атрибутам и защиту инвариантов доменной модели.

---

### Ключевые концепции
- **Data Descriptor** — дескриптор с `__get__` и `__set__` для валидации при записи (`PriorityDescriptor`, `StatusDescriptor`)
- **Non-Data Descriptor** — дескриптор только с `__get__` для чтения (`CreatedAtDescriptor`)
- **@property** — вычисляемые и защищённые свойства (`id`, `description`, `is_ready`)
- **Инкапсуляция** — разделение публичного API и внутреннего состояния (`_id`, `_status`, `_created_at`)
- **Валидация** — предотвращение некорректных состояний через исключения

### Описание компонентов

 - `src/models.py` - Класс `Task` с дескрипторами, property и методами перехода статусов
 - `src/descriptors.py` - Пользовательские дескрипторы: `PriorityDescriptor`, `StatusDescriptor`, `CreatedAtDescriptor`
 - `src/exceptions.py` - Специализированные исключения: `TaskValidationError`, `TaskStateError`
 - `src/sources.py` - Источники задач (обновлены под новую модель `Task`)
 - `src/collector.py` - Сборщик задач — генерирует уникальные ID для задач
 - `src/logger.py` - Логирование — записывает события в `src/shell.log`
 - `src/main.py` - Точка входа — демонстрирует работу всех компонентов
 - `tests/test_for_all.py` - Тесты для всех компонентов

## Для запуска программы

### 1) Клонирование репозитория
```bash
git clone https://github.com/OikonoMike/Python_Laba_2_2.git  
```

### 2) Установка зависимостей
```bash
pip install -r requirements.txt
```

### 3) Запуск программы
```bash
python -m src.main
```

### 4) Запуск тестов
```bash
pytest -v
```