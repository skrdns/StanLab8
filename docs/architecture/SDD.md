# SDD — Software Design Document

**Версія:** 1.0  
**Дата:** 2025  
**Базується на:** [SSD](SSD.md)

---

## 1. Архітектура

Використовується **клієнт-серверна архітектура (моноліт)**.
Frontend (React)
REST API (HTTP/HTTPS)
Backend (Python / Node.js)
PostgreSQL Database

---

## 2. Основні компоненти

| Компонент | Технологія | Відповідальність |
|-----------|------------|-----------------|
| Frontend | React / HTML | UI, взаємодія з API |
| Backend | Python / Node.js | Бізнес-логіка, REST API |
| Database | PostgreSQL | Збереження даних |

---

## 3. API Endpoints

| Метод | Endpoint | Опис | Вимога |
|-------|----------|------|--------|
| POST | `/auth/login` | Авторизація користувача | [FR-01](SSD.md) |
| POST | `/auth/register` | Реєстрація користувача | [FR-01](SSD.md) |
| POST | `/orders` | Створити замовлення | [FR-02](SSD.md) |
| PUT | `/orders/{id}` | Оновити замовлення | [FR-03](SSD.md) |
| DELETE | `/orders/{id}` | Скасувати замовлення | [FR-04](SSD.md) |
| GET | `/orders` | Список замовлень | [FR-05](SSD.md) |
| GET | `/admin/orders` | Адміністративний перегляд | [FR-06](SSD.md) |

---

## 4. Модель даних

### Таблиця `users`

| Поле | Тип | Опис |
|------|-----|------|
| id | UUID | Унікальний ідентифікатор |
| email | VARCHAR | Email користувача |
| password_hash | VARCHAR | Хеш пароля |
| role | ENUM | `client` або `admin` |

### Таблиця `orders`

| Поле | Тип | Опис |
|------|-----|------|
| id | UUID | Унікальний ідентифікатор |
| user_id | UUID | Зовнішній ключ до users |
| status | ENUM | `pending`, `active`, `cancelled` |
| created_at | TIMESTAMP | Дата створення |

---

## 5. Безпека

- Авторизація через JWT-токени (термін дії: 24 год)
- HTTPS для всіх запитів
- Розмежування прав: клієнт бачить лише свої замовлення
