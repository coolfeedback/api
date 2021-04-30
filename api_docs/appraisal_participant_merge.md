# AppraisalParticipantCreateOrMergeParticipationReason (Создание или объединение причины участия)
## Создание/Объединене причины участия

`POST /api/appraisals/{appraisalId}/participants/CreateOrMergeParticipationReason`

где ```appraisalId``` - идентификатор анкетирования

Пример сообщения в Body запроса:

```json
{
    "externalId": "externalID1104",
    "participantUserExternalId": "SU44617",
    "dateCompleted": "2018-07-01T00:00:00+03:00",
    "isMain": false,
    "textFeedback": "0KLRg9GCINGA0LDQt9C90YvQtSDQv9C+0LvQtdC30L3Ri9C1INGA0LXQutC+0LzQtdC90LTQsNGG0LjQuCA=",
    "textHint": "0KLRg9GCINGA0LDQt9C90YvQtSDQv9C+0LvQtdC30L3Ri9C1INGA0LXQutC+0LzQtdC90LTQsNGG0LjQuCA=",
    "status": 3,
    "participationReason": "0KLRg9GCINGA0LDQt9C90YvQtSDQv9C+0LvQtdC30L3Ri9C1INGA0LXQutC+0LzQtdC90LTQsNGG0LjQuCA=",
    "requestDate": "2019-01-15T00:00:00+03:00",
    "responseDate": "2018-12-25T00:00:00+03:00"
}
```

### Описание полей

|Поле|Тип|Ограничения|Описание|
|----|--------|------------|------------|
|externalId|string| Unique |Внешний идентификатор (опциональный)|
|participantUserExternalId|string|Not Null |Идентификатор пользователя из внешней системы, участника-опрашиваемого|
|dateCompleted| datetime (подробнее о формате [здесь](general.md))| - |Дата выполнения|
|isMain| boolean  |Not Null | Является ли участник основным опрашиваемым|
|textFeedback| string | - | Текстовый отзыв. Строка, закодированная в Base64. *Максимальная длина - 4000 символов*|
|textHint| string | - | Тестовая подсказка от основного опрашиваемого. Строка, закодированная в Base64. *Максимальная длина - 4000 символов*|
|status| Значения из [перечисления](#appraisalParticipant_status)| Not Null | Статус участника анкетирования|
|participationReason| string | - | Основание участия. Строка, закодированная в Base64. *Максимальная длина - 4000 символов*|
|requestDate| datetime (подробнее о формате [здесь](general.md))|-| Дата отправки |
|requestLastDate| datetime (подробнее о формате [здесь](general.md))|-| Дата получения ответа |

<a name="appraisalParticipant_status"></a>
#### Статус участника анкетирования
|Значение|Описание|
|----|--------|
| 1 | Запрошен | 
| 2 | Предоставлен |
| 3 | Не запрошен |
| 4 | Нет возможности оценить|
| 5 | Удален|

### Логика работы

Если не были переданы обязательные пераметры, то будет возвращен код ```400 BadRequest ```.
В случае создания записи, будет возвращен статус ```201 Created```. В случае нахождения такого участника по заданному анкетированию, будет обновлено поле participationReason и возвращен статус ```201 Created```. В теле ответа JSON с идентификатором созданной сущности:

```json
{
    "id": "c8a35627-db25-45e8-a09d-ee7d1c6e8e8c"
}
```
