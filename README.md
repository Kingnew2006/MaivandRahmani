# задание 1.1 

```mermaid
graph TD
    A[Начало] --> B[Кипячение воды]
    B --> C{Есть ли чай?}
    C -->|Да| D[Заварить чай]
    C -->|Нет| E[Купить чай]
    E --> D
    D --> F[Пить чай]
    F --> G[Конец]
```

# задание 1.2

```mermaid
sequenceDiagram
    title Заказ такси
    participant a as клиент
    participant b as приложение
    participant c as сервер
    participant d as водитель
    
    a->>b: Вызов такси
    b->>c: запрос на пойск
    c->>d: новый заказ
    d-->>c: Принятие заказа 
    c-->>b: данный водителя 
    b-->>a: Заказ принят
    d->>a: Забирает клиента
```

# задание 2.1

```mermaid
    classDiagram
    class Book {
        +String title
        +String author
        +String ISBN
        +Boolean isAvailable
    }

    class User {
        +String name
        +Integer userId
        +List~Book~ borrowedBooks
    }

    class Library {
        +List~Book~ books
        +List~User~ users
    }

    User *-- Book : "берёт книги"
    Library o-- Book : "содержит книги"
    Library o-- User : "зарегистрированные пользователи"
```

 # задание 2.2

 ```mermaid
    gantt
    title Разработка мобильного приложения
    dateFormat  YYYY-MM-DD
    section Preparation
    Preparation          :a1, 2025-11-01, 5d
    section Design
    Design               :after a1, 7d
    section Frontend
    Frontend             :after a1, 10d
    section Backend
    Backend              :after a1, 12d
    section Testing
    Testing              :after Frontend, 5d
```

# задание 3.1

```mermaid
    graph TD
    subgraph Frontend
        React
        Redux
        Router
    end

    subgraph Backend
        NodeJS
        Express
        MongoDB
    end

    subgraph External
        Stripe
        SendGrid
    end

    React --> Router
    React --> Redux
    Frontend --> Backend
    Backend --> Stripe
    Backend --> SendGrid
```

# задание 3.2

```mermaid
stateDiagram
    [*] --> Новый
    Новый --> Подтвержденный
    Подтвержденный --> Оплаченный
    Оплаченный --> Отправленный
    Отправленный --> Доставленный
    Новый --> Отмененный
    Оплаченный --> Возвращенный

    state Оплаченный {
        [*] --> ОжиданиеПлатежа
        ОжиданиеПлатежа --> Подтвержден
    }

```

# задание 4.1

```mermaid
journey
    title Покупка билетов в кино
    section Поиск фильма
      Найти фильм: 5: Пользователь рад
    section Выбор сеанса
      Выбрать сеанс: 4
    section Выбор мест
      Выбрать места: 4
    section Оплата
      Оплатить: 3
    section Получение билетов
      Получить билеты: 5
    section Оценка
      Оценить опыт: 5

```

# задание 4.2

```mermaid
erDiagram
    USERS {
        int id PK
        string name
        string email
    }
    POSTS {
        int id PK
        string content
        int author FK
    }
    COMMENTS {
        int id PK
        string content
        int post FK
        int author FK
    }
    LIKES {
        int user FK
        int post FK
    }
    SUBSCRIPTIONS {
        int subscriber FK
        int subscribed_to FK
    }

    USERS ||--o{ POSTS : "создает"
    USERS ||--o{ COMMENTS : "пишет"
    POSTS ||--o{ COMMENTS : "имеет"
    USERS ||--o{ LIKES : "лайкает"
    POSTS ||--o{ LIKES : "получает лайки"
    USERS ||--o{ SUBSCRIPTIONS : "подписан"
```

# задание 5

# 📦 Сервис доставки еды – Полная документация
## 1. Блок-схема процесса заказа
```mermaid
    graph TD
    A[Начало] --> B[Выбор блюда]
    B --> C[Добавление в корзину]
    C --> D{Оформление заказа?}
    D -->|Да| E[Оплата]
    D -->|Нет| B
    E --> F[Подтверждение заказа]
    F --> G[Курьер забирает заказ]
    G --> H[Доставка клиенту]
    H --> I[Конец]
```
## 2. Диаграмма последовательности
```mermaid
sequenceDiagram
    title Процесс доставки еды
    participant Client as Клиент
    participant App as Приложение
    participant Restaurant as Ресторан
    participant Courier as Курьер
    
    Client->>App: Сделать заказ
    App->>Restaurant: Передача заказа
    Restaurant->>Courier: Передача готового заказа
    Courier-->>Restaurant: Подтверждение получения
    Courier->>Client: Доставка заказа
    Client-->>App: Подтверждение получения
```
## 3. Диаграмма классов
```mermaid
classDiagram
    class User {
        +String name
        +Integer userId
        +String address
    }

    class Order {
        +Integer orderId
        +List~MenuItem~ items
        +String status
        +Date orderDate
    }

    class MenuItem {
        +String name
        +Float price
    }

    class Restaurant {
        +String name
        +String location
        +List~MenuItem~ menu
    }

    class Courier {
        +String name
        +Integer courierId
        +String vehicle
    }

    User "1" --o "*" Order : делает
    Order "*" -- "*" MenuItem : содержит
    Restaurant "1" --o "*" MenuItem : предлагает
    Courier "1" --o "*" Order : доставляет
```
## 4. ER-диаграмма базы данных
```mermaid
erDiagram
    USERS {
        int id PK
        string name
        string address
    }
    ORDERS {
        int id PK
        int user_id FK
        int restaurant_id FK
        string status
        date order_date
    }
    MENU_ITEMS {
        int id PK
        string name
        float price
        int restaurant_id FK
    }
    RESTAURANTS {
        int id PK
        string name
        string location
    }
    COURIERS {
        int id PK
        string name
        string vehicle
    }

    USERS ||--o{ ORDERS : делает
    RESTAURANTS ||--o{ MENU_ITEMS : предлагает
    RESTAURANTS ||--o{ ORDERS : принимает
    COURIERS ||--o{ ORDERS : доставляет
```
## 5. User Journey клиента
```mermaid
journey
    title Путь клиента при заказе еды
    section Поиск и выбор
      Выбор блюда: 5: Радость
      Добавление в корзину: 4
    section Оплата
      Оплата: 3: Нейтрально
    section Доставка
      Ожидание курьера: 2: Немного раздражение
      Получение заказа: 5: Радость
    section Оценка
      Оставить отзыв: 4
```
## 6. Диаграмма Ганта разработки проекта
```mermaid
    gantt
    title Разработка сервиса доставки еды
    dateFormat  YYYY-MM-DD
    section Planning
    ProjectPlanning :a1, 2025-11-01, 5d
    section Design
    UI/UX Design   :after a1, 7d
    section Frontend
    Frontend Dev   :after a1, 10d
    section Backend
    Backend Dev    :after a1, 12d
    section Testing
    Testing        :after Frontend Dev, 5d
```

# задание 6

```mermaid
pie title Доля автомобилей на российском рынке
    "Иномарки" : 55
    "Отечественные" : 35
    "Совместное производство" : 10
```

 
 
