# API: Отправка ссылки с просьбой дозапонить анкету пациента

## Назначение

Отправка в wa сообщения, что необходимо дозаполнить анкету пациента - в сообщении присутствует ссылка на анкету

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


## Назначение

Для price<br>
Отправка в wa сообщения:<br>
К сожалению, заказ не был оплачен вовремя, и выбранное время записи к врачу стало недоступным.<br>
Вы можете выбрать новое удобное время по ссылке: {url}

## Эндпоинт

**POST** `/api/wa/notification/choose-new-appointment-slot`

## Тело запроса (JSON)

```json
{
  "phone": "79991234567",
  "url": "https://example.com/link/abc123"
}
```

## Успешный ответ

Если задача на отправку WA успешно создана:

**HTTP CODE 200 OK**

```json
{
    "status": "success",
    "data": {
        "bot_task_id": 176428
    }
}

```

**HTTP CODE 200 Ошибки**
```json
{
    "status": "fail",
    "error": "Не переданы обязательные параметры или пустые значения: ...",
    "code": 10
}

```
```json
{
    "status": "fail",
    "error": "Ошибка валидации: ...",
    "code": 11
}

```

> + могут приходить Стандартные ошибки HTTP CODE 400, 500

**HTTP 400 BadRequestHttpException**

```json
{
    "name": "Bad Request",
    "message": "Пустое тело запроса",
    "code": 0,
    "status": 400,
    "type": "yii\\web\\BadRequestHttpException"
}
```

