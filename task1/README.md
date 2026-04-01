# 🍕 Проект UML: Система доставки еды "FoodFast"

Данный репозиторий содержит документацию и диаграммы UML для системы автоматизации доставки еды **FoodFast**. Проект разработан для демонстрации навыков объектно-ориентированного анализа и проектирования.

---

## 📋 Лабораторная работа №1: Диаграмма классов

### Описание системы
Диаграмма классов моделирует архитектуру платформы **FoodFast**, связывающей клиентов, рестораны и курьеров. Система обеспечивает полный цикл заказа: от выбора блюд до доставки и оплаты.

### Основные классы

#### 1. Абстрактный класс `User`
Базовый класс для всех участников системы.
*   **Атрибуты:** `id`, `name`, `email`, `phone`, `passwordHash`
*   **Методы:**
    *   `login()` — аутентификация в системе
    *   `logout()` — завершение сеанса
    *   `updateProfile()` — редактирование личных данных
    *   `viewOrderHistory()` — просмотр истории заказов

#### 2. Наследники класса `User`
| Класс | Роль | Ключевые методы |
| :--- | :--- | :--- |
| **`Customer`** | Заказчик | `placeOrder()`, `trackDelivery()`, `addReview()`, `applyPromoCode()` |
| **`Courier`** | Курьер | `acceptDelivery()`, `updateLocation()`, `confirmDelivery()`, `setAvailability()` |
| **`RestaurantManager`** | Менеджер ресторана | `confirmOrder()`, `updateMenu()`, `changeOrderStatus()`, `viewDailyStats()` |
| **`Administrator`** | Администратор | `manageUsers()`, `resolveDisputes()`, `configureFees()`, `viewSystemLogs()` |
| **`Guest`** | Гость | `browseMenu()`, `register()` |

#### 3. Бизнес-объекты
*   **`Order` (Заказ)**
    *   *Атрибуты:* `id`, `createdAt`, `totalAmount`, `status` (New, Paid, Cooking, etc.), `deliveryAddress`
    *   *Методы:* `calculateTotal()`, `cancel()`
*   **`MenuItem` (Позиция меню)**
    *   *Атрибуты:* `id`, `name`, `description`, `price`, `category`, `isAvailable`
*   **`Payment` (Платеж)**
    *   *Атрибуты:* `id`, `amount`, `method`, `transactionId`, `status`
    *   *Методы:* `process()`, `refund()`
*   **`DeliveryRoute` (Маршрут)**
    *   *Атрибуты:* `id`, `startPoint`, `endPoint`, `estimatedTime`, `currentLocation`
*   **`Review` (Отзыв)**
    *   *Атрибуты:* `id`, `rating`, `comment`, `timestamp`

---

### 🔗 Отношения между классами

| Тип отношения | Классы | Описание |
| :--- | :--- | :--- |
| **Наследование** | `User` ← `Customer`, `Courier`, ... | Общие атрибуты пользователя и методы авторизации |
| **Композиция** | `Order` ◆ `OrderItem` | Позиции в заказе не существуют без самого заказа |
| **Композиция** | `Payment` ◆ `TransactionDetails` | Детали транзакции являются частью платежа |
| **Агрегация** | `Order` ◊ `MenuItem` | Заказ состоит из блюд (блюда существуют независимо) |
| **Ассоциация** | `Order` → `Customer` | Заказ размещается конкретным клиентом |
| **Ассоциация** | `Order` → `RestaurantManager` | Заказ обрабатывается менеджером ресторана |
| **Ассоциация** | `DeliveryRoute` → `Courier` | Маршрут назначается конкретному курьеру |
| **Зависимость** | `Guest` → `Customer` | Гость регистрируется и становится клиентом |
| **Зависимость** | `Customer` → `Payment` | Клиент инициирует оплату |

---

### 📐 Визуализация (PlantUML)

<img width="6332" height="4828" alt="image" src="https://github.com/user-attachments/assets/8cf87ffe-52b1-4635-a054-f5097ce7903c" />
