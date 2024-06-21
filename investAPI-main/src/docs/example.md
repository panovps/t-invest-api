# Примеры запросов

На странице привели примеры запросов по некоторым методам в формате JSON.

## [PostOrder](/investAPI/orders/#postorder) – выставить заявку

Задача: выставить лимитную заявку на покупку инструмента.
```
{
"figi": "BBG000000001", \\ FIGI инструмента, по которому выставляется заявка. В данном случае используем Т-Банк Вечный портфель RUB
"quantity": "1", \\ Количество лотов инструмента
"price": { \\ Цена, по которой будет выставлена заявка
"nano": 600000000,
"units": "5"
},
"direction": "ORDER_DIRECTION_BUY", \\ Направление заявки, в данном случае — покупка
"accountId": "XXXXXXXXXX", \\ Номер счёта, с которого будет выставлена заявка
"orderType": "ORDER_TYPE_LIMIT", \\ Тип заявки, в данном случае — лимитная
"orderId": "string" \\ Ключ идемпотентности
}
```
## [ReplaceOrder](/investAPI/orders/#replaceorder) – изменить выставленную заявку

Задача: изменить выставленную ранее заявку.
```
{
"accountId": "XXXXXXXXXX", \\ Номер счёта, с которого выставлена заявка
"orderId": "XXXXXXXXX", \\ Номер выставленной заявки
"idempotencyKey": "string", \\ Ключ идемпотентности
"quantity": "4", \\ Новое количество лотов
"price": { \\ Новая цена заявки
"nano": 700000000,
"units": "5"
}
}
```
## [PostStopOrder](/investAPI/stoporders/#poststoporder) – выставить стоп-заявку

Задача: выставить лимитную заявку на покупку инструмента.

```
{
"figi": "BBG000000001", \\ FIGI инструмента, по которому выставляется заявка. В данном случае используем Т-Банк Вечный портфель RUB
"quantity": "2", \\ Количество лотов инструмента
"price": { \\ Цена, по которой будет выставлена заявка
"nano": 600000000,
"units": "5"
},
"stopPrice": { \\ Стоп-цена, она же цена активации заявки — это значит, когда цена инструмента на бирже достигнет установленной стоп-цены, заявка будет выставлена с указанными параметрами
"nano": 700000000,
"units": "5"
},
"direction": "STOP_ORDER_DIRECTION_BUY", \\ Направление сделки, в данном случае — покупка
"accountId": "XXXXXXXXXX", \\ Номер счёта, с которого будет выставлена заявка
"expirationType": "STOP_ORDER_EXPIRATION_TYPE_GOOD_TILL_CANCEL", \\ Срок действия заявки. В данном случае — пока не будет отменена
"stopOrderType": "STOP_ORDER_TYPE_STOP_LIMIT" \\ Тип стоп-заявки. В данном случае — стоп-лимит
}
```



## [GetOperationsByCursor](/investAPI/operations/#getoperationsbycursor) – получить операции по счёту с курсором

Задача: получить список операций по счёту за год с постраничным выводом.
```
{
"accountId": "XXXXXXXXX",  \\ Номер счёта, единственный обязательный параметр в этом методе. Можно указать только его и получить первые 100 операций по счёту
"instrumentId": "BBG000000001", \\ Параметр, в котором вы можете указать FIGI или instrument_uid инструмента, по которому хотите получить операции. В данном случае используем Т-Банк Вечный портфель RUB
"from": "2021-11-07T12:49:35.896Z", \\ Дата начала периода, с которого отображаются операции
"to": "2022-11-07T12:49:35.896Z", \\ Дата окончания периода, по который отображаются операции
"limit": 1000, \\ Лимит вывода количества операций. Максимальный лимит — 1000, значение по умолчанию — 100
"operationTypes": [
"OPERATION_TYPE_BUY" \\ Тип операций – покупка
],
"state": "OPERATION_STATE_EXECUTED" \\ Статус операций, в данном случае — исполненные
}
```
## [GetOperations](/investAPI/operations/#getoperations) – получить операции по счёту

Задача: получить список операций по счёту за год.
```
{
"accountId": "XXXXXXXXXX",  \\ Номер счёта, единственный обязательный параметр в этом методе. Можно указать только его и получить первые 100 операций по счёту
"figi": "BBG000000001", \\ Параметр, в котором вы можете указать FIGI инструмента, по которому хотите получить операции. В данном случае используем Т-Банк Вечный портфель RUB
"from": "2021-11-07T12:49:35.896Z", \\ Дата начала периода, с которого отображаются операции
"to": "2022-11-07T12:49:35.896Z", \\ Дата окончания периода, по который отображаются операции
"state": "OPERATION_STATE_EXECUTED" \\ Статус операций, в данном случае — исполненные
}
```
## [GetCandles](/investAPI/marketdata/#getcandles) – получить свечи

Задача: получить минутные свечи за день.
```
{
"from": "2022-11-08T05:47:40.866Z", \\ Дата начала периода запрошенных свечей
"to": "2022-11-09T05:47:40.866Z", \\ Дата окончания периода запрошенных свечей
"interval": "CANDLE_INTERVAL_1MIN", \\ Интервал свечей
"instrumentId": "BBG000000001"  \\ Параметр, в котором вы можете указать FIGI или instrument_uid инструмента, по которому хотите получить операции. В данном случае используем Т-Банк Вечный портфель RUB
}
```