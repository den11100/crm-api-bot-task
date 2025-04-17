# API: Отправка ссылки с просьбой дозапонить анкету пациента

## Назначение

Отправка анкеты пациенту в WhatsApp по номеру телефона, указанному в заказе. Сообщение отправляется с номера ОКС B2C

## Эндпоинт

**POST** `/api/wa/notification/patient-information-questionnaire`

## Заголовки

- `Content-Type: application/json`
- `X-Api-Key: <API_KEY>` — обязательный заголовок.

Если `X-Api-Key` не соответствует ожидаемому значению, возвращается ошибка `400 Bad API key`.

## Тело запроса (JSON)

```json
{
  "phone": "79991234567",
  "url": "https://example.com/questionnaire/abc123"
}
```

# Примеры ответов API

## Успешный ответ

Если задача на отправку анкеты успешно создана и сохранена:

**HTTP 200 OK**

```json
{
  "status": 200,
  "data": "bot_task.id: 12345"
}
```


## Ошибка: Валидация модели BotTask
Если задача `BotTask` не сохраняется из-за ошибок валидации:

**HTTP 422 Unprocessable Entity**

```json
{
  "name": "Unprocessable Entity",
  "message": "Ошибка валидации: текст ошибки",
  "code": 0,
  "status": 422,
  "type": "yii\\web\\HttpException"
}
```
