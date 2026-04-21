# Developer Onboarding

**Версія:** 1.0  
**Архітектура:** [SDD](../architecture/SDD.md)  
**Інфраструктура:** [ISD](../architecture/ISD.md)

---

## 1. Початок роботи

### Клонування репозиторію
```bash
git clone https://github.com/org/order-management-system
cd order-management-system
```

### Налаштування середовища
```bash
cp .env.example .env
# Заповніть JWT_SECRET та DB_PASSWORD у файлі .env
```

### Запуск через Docker
```bash
docker-compose up -d
# Frontend: http://localhost:3000
# API:      http://localhost:8000
```

---

## 2. Структура проекту
