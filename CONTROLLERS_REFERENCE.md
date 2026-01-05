# 📋 Справочник контроллеров API

Полная документация всех эндпоинтов API.

---

## 📊 Таблица роутов

| Метод | Путь | Описание | Код
|--------|------|----------|-----|
| GET | /offers | Получить все | 200 |
| POST | /offers | Создать | 201 |
| GET | /offers/:id | Получить одно | 200/404 |
| PUT | /offers/:id | Обновить | 200 |
| DELETE | /offers/:id | Удалить | 204 |
| GET | /favorites | Получить избранные | 200 |
| POST | /favorites/:id | Добавить | 200 |
| DELETE | /favorites/:id | Удалить | 204 |
| GET | /options/house | Получить типы | 200 |

---

## 📑 Offer Controller

### GET /offers

**Описание:** Получить все предложения

**Пример запроса:**
```bash
curl http://localhost:3000/offers | jq
```

**Ответ (200):**
```json
[
  {
    "_id": "507f1f77bcf86cd799439012",
    "title": "Beautiful apartment",
    "description": "Amazing place",
    "city": "Paris",
    "preview": "https://example.com/preview.jpg",
    "images": ["https://example.com/img1.jpg"],
    "isPremium": false,
    "type": "apartment",
    "bedrooms": 2,
    "guests": 4,
    "price": 100,
    "amenities": ["WiFi"],
    "coordinates": {
      "latitude": 48.85661,
      "longitude": 2.351499
    }
  }
]
```

---

### POST /offers

**Описание:** Создать новое предложение

**Пример запроса:**
```bash
curl -X POST http://localhost:3000/offers \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Beautiful apartment",
    "description": "Amazing place",
    "city": "Paris",
    "preview": "https://via.placeholder.com/800x600",
    "images": ["https://via.placeholder.com/800x600"],
    "isPremium": false,
    "type": "apartment",
    "bedrooms": 2,
    "guests": 4,
    "price": 100,
    "amenities": ["WiFi"],
    "coordinates": {
      "latitude": 48.85661,
      "longitude": 2.351499
    }
  }'
```

**Ответ (201):**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Beautiful apartment",
  "description": "Amazing place",
  "city": "Paris",
  "preview": "https://via.placeholder.com/800x600",
  "images": ["https://via.placeholder.com/800x600"],
  "isPremium": false,
  "type": "apartment",
  "bedrooms": 2,
  "guests": 4,
  "price": 100,
  "amenities": ["WiFi"],
  "coordinates": {
    "latitude": 48.85661,
    "longitude": 2.351499
  }
}
```

**Ошибка (400):**
```json
{
  "error": "Invalid data",
  "message": "All fields are required"
}
```

---

### GET /offers/:id

**Описание:** Получить одно предложение

**Параметры:**
- `id` (path) - ID предложения (ObjectId MongoDB)

**Пример:**
```bash
curl http://localhost:3000/offers/507f1f77bcf86cd799439012 | jq
```

**Ответ (200) - Найдено:**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Beautiful apartment",
  ...
}
```

**Ответ (404) - Не найдено:**
```json
{
  "error": "Not found",
  "message": "Offer not found"
}
```

---

### PUT /offers/:id

**Описание:** Обновить предложение

**Параметры:**
- `id` (path) - ID предложения

**Пример:**
```bash
curl -X PUT http://localhost:3000/offers/507f1f77bcf86cd799439012 \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Updated title",
    "price": 150
  }'
```

**Ответ (200):**
```json
{
  "_id": "507f1f77bcf86cd799439012",
  "title": "Updated title",
  "price": 150,
  ...
}
```

---

### DELETE /offers/:id

**Описание:** Удалить предложение

**Пример:**
```bash
curl -X DELETE http://localhost:3000/offers/507f1f77bcf86cd799439012
```

**Ответ (204):**
Никакого содержимого

---

## 💌 Favorites Controller

### GET /favorites

**Описание:** Получить все избранные

```bash
curl http://localhost:3000/favorites | jq
```

**Ответ:**
```json
[
  "507f1f77bcf86cd799439012",
  "507f1f77bcf86cd799439013"
]
```

---

### POST /favorites/:id

**Описание:** Добавить в избранные

```bash
curl -X POST http://localhost:3000/favorites/507f1f77bcf86cd799439012
```

**Ответ (200):**
```json
{
  "message": "Added to favorites"
}
```

---

### DELETE /favorites/:id

**Описание:** Удалить из избранных

```bash
curl -X DELETE http://localhost:3000/favorites/507f1f77bcf86cd799439012
```

**Ответ (204):**
Никакого содержимого

---

## 🎫 Options Controller

### GET /options/house

**Описание:** Получить типы домов

```bash
curl http://localhost:3000/options/house | jq
```

**Ответ (200):**
```json
[
  "apartment",
  "house",
  "room",
  "hotel"
]
```

### GET /options/whole-house

**Описание:** Получить варианты отдельных домов

```bash
curl http://localhost:3000/options/whole-house | jq
```

**Ответ (200):**
```json
[
  "whole house",
  "private room"
]
```

---

## 📋 Таблица Кодов Ответов

| Код | Описание | Показывает |
|------|----------|----------|
| 200 | OK | Успешный гет |
| 201 | Created | Объект создан |
| 204 | No Content | Успешно удалено |
| 400 | Bad Request | Неверные данные |
| 404 | Not Found | Не найдено |
| 500 | Server Error | Ошибка сервера |

---

## 📄 Пример данных

### Полное оферта

```json
{
  "title": "Beautiful 3 bedrooms apartment in the city center",
  "description": "Amazing and very cozy apartment in center of Paris.",
  "city": "Paris",
  "preview": "https://16.design.htmlacademy.pro/static/hotel/1.jpg",
  "images": [
    "https://16.design.htmlacademy.pro/static/hotel/1.jpg",
    "https://16.design.htmlacademy.pro/static/hotel/2.jpg",
    "https://16.design.htmlacademy.pro/static/hotel/3.jpg",
    "https://16.design.htmlacademy.pro/static/hotel/4.jpg",
    "https://16.design.htmlacademy.pro/static/hotel/5.jpg",
    "https://16.design.htmlacademy.pro/static/hotel/6.jpg"
  ],
  "isPremium": true,
  "type": "apartment",
  "bedrooms": 3,
  "guests": 4,
  "price": 120,
  "amenities": ["WiFi", "Kitchen", "Washer", "Parking", "Air conditioning"],
  "coordinates": {
    "latitude": 48.85661,
    "longitude": 2.351499
  }
}
```

---

✅ **Примеры готовы** - Где использовать

**curl** - В терминале и bash скриптах
**Postman** - Графически и коллекций
**REST Client** - В VS Code в файле api.http
**Jest** - Напишите тесты

При чтении **TESTING_GUIDE.md** вы сытеете как использовать эти данные в каждом орудии! 🚀
