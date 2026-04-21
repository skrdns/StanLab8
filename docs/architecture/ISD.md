# ISD — Infrastructure Specification Document

**Версія:** 1.0  
**Дата:** 2025  
**Базується на:** [SDD](SDD.md)

---

## 1. Середовище розгортання

- **Хмарний провайдер:** AWS / Azure
- **Контейнеризація:** Docker + Docker Compose
- **ОС:** Ubuntu 22.04 LTS

---

## 2. Компоненти інфраструктури

| Компонент | Технологія | Призначення |
|-----------|------------|-------------|
| Web сервер | Nginx | Reverse proxy, SSL termination |
| Backend | Docker container | Бізнес-логіка, REST API |
| База даних | PostgreSQL 15 | Збереження даних |
| Load balancer | AWS ALB | Розподіл навантаження |

---

## 3. Docker Compose конфігурація

```yaml
version: '3.8'
services:
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
      - "443:443"

  backend:
    build: ./backend
    environment:
      - DATABASE_URL=postgresql://db:5432/orders
      - JWT_SECRET=${JWT_SECRET}

  db:
    image: postgres:15
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=orders
      - POSTGRES_PASSWORD=${DB_PASSWORD}

volumes:
  pgdata:
```

---

## 4. Масштабування

- Горизонтальне масштабування backend-сервісів через Docker replicas
- Auto-scaling groups для пікових навантажень
- Read replicas для PostgreSQL при зростанні навантаження

---

## 5. Моніторинг

- Логи: централізований збір через AWS CloudWatch
- Аптайм: перевірка доступності кожні 60 секунд
- Алерти: при downtime понад 1 хв — сповіщення команді
