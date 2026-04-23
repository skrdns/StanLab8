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

```
order-management-system/
├── docs/           # Вся документація (Markdown)
├── frontend/       # React застосунок
├── backend/        # API сервер
├── docker-compose.yml
└── .env.example
```

---

## 3. Правила роботи з документацією

- Вся документація знаходиться в `/docs`
- Редагуйте лише `.md` файли
- **Забороняється** зберігати документи у форматі Word або PDF
- Кожна зміна документації — окремий git commit:

```bash
git commit -m "docs(SSD): add FR-07 bulk order creation"
git commit -m "docs(SDD): update auth endpoint to OAuth2"
```

---

## 4. Генерація сайту документації

```bash
pip install mkdocs mkdocs-material
cd docs
mkdocs serve        # локальний перегляд → http://127.0.0.1:8000
mkdocs build        # генерація статичного сайту у ./site/
mkdocs gh-deploy    # публікація на GitHub Pages
```

---

## 5. Корисні посилання

- [Функціональні вимоги (SSD)](../architecture/SSD.md)
- [Архітектура (SDD)](../architecture/SDD.md)
- [Інфраструктура (ISD)](../architecture/ISD.md)
- [Test Strategy](../quality/test-strategy.md)
