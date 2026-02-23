# Практична робота pz-UML
Курсант: Шмиголь Олександра

## 1. Use Case Diagram
```mermaid
usecaseDiagram
    actor Op as "Оператор БПЛА"
    actor An as "Аналітик"
    actor Com as "Командир"

    package "Система Delta" {
        usecase UC1 as "Внести дані про ціль"
        usecase UC2 as "Переглянути мапу"
        usecase UC3 as "Верифікувати дані (ML)"
        usecase UC4 as "Прийняти рішення"
    }

    Op --> UC1
    Op --> UC2
    An --> UC2
    An --> UC3
    Com --> UC2
    Com --> UC4

    sequenceDiagram
    participant Op as Оператор
    participant DB as База даних Delta
    participant ML as ML-Модуль
    participant An as Analytik

    Op->>DB: Внесення координат цілі
    DB->>ML: Запит на перевірку
    ML-->>ML: Обробка алгоритмом
    ML->>DB: Оновлення статусу
    DB->>An: Сповіщення про ціль
    An->>DB: Підтвердження/Відхилення

    flowchart TD
    A[Отримання даних] --> B{Валідація}
    B -- Коректно --> C[Перевірка ML]
    B -- Помилка --> D[Відхилити]
    C --> E{Надійність?}
    E -- Висока --> F[Візуалізація на мапі]
    E -- Низька --> G[Додаткова перевірка]
    F --> H[Кінець]
    G --> H
    D --> H