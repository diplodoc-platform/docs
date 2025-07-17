# Класс AMAMutableRevenueInfo

Изменяемая версия класса [AMARevenueInfo](AMARevenueInfo.md) с информацией о покупках.

Объект `AMAMutableRevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportRevenue](AMAAppMetrica.md#method_reportRevenue) класса [AMAAppMetrica](AMAAppMetrica.md).

## Свойства {#property_summary}

#|
|| [payload](#property_payload) | Дополнительная информация о покупке. Например, можно использовать для категоризации ваших продуктов. ||
|| [productID](#property_productID) | Идентификатор покупки. Может содержать до 200 символов. ||
|| [quantity](#property_quantity) | Количество покупок (купленных товаров). ||
|| [receiptData](#property_receiptData) | Подробная информация о покупке из App Store. Свойство используется для валидации покупки в приложении. ||
|| [transactionID](#property_transactionID) | Идентификатор транзакции [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) из класса [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction). Свойство используется для валидации покупки в приложении. ||
|#

## Описание свойств {#property_detail}

### payload {#property_payload}

`(nonatomic, copy) NSDictionary *payload`

Дополнительная информация о покупке. Например, можно использовать для категоризации ваших продуктов.

Необходимо передать объект `NSDictionary`, который может быть преобразован в валидный JSON. Максимальный размер значения — 30 КБ.

### productID {#property_productID}

`(nonatomic, copy) NSString *productID`

Идентификатор покупки. Может содержать до 200 символов.

### quantity {#property_quantity}

`(nonatomic, assign) NSUInteger quantity`

Количество покупок (купленных товаров).

Используется в формуле расчета выручки:

```
Выручка = количество * стоимость
```

{% note info %}

Значение должно быть больше 0. Если значение равно 0 — покупка игнорируется.

{% endnote %}

### receiptData {#property_receiptData}

`(nonatomic, copy) NSData *receiptData`

Подробная информация о покупке из App Store. Свойство используется для валидации покупки в приложении. Подробнее в [документации Apple](https://developer.apple.com/library/content/releasenotes/General/ValidateAppStoreReceipt/Chapters/ValidateRemotely.html).

Пример получения `receiptData` см. в разделе [Отправка Revenue](../ios-operations.md#send-revenue).

{% note alert %}

Значение должно быть получено до вызова `[[SKPaymentQueue defaultQueue] finishTransaction:transaction]` и передано вместе с [transactionID](#property_transactionID).

{% endnote %}

### transactionID {#property_transactionID}

`(nonatomic, copy) NSString *transactionID`

Идентификатор транзакции [transactionIdentifier](https://developer.apple.com/documentation/storekit/skpaymenttransaction/1411288-transactionidentifier) из класса [SKPaymentTransaction](https://developer.apple.com/documentation/storekit/skpaymenttransaction). Свойство используется для валидации покупки в приложении.

Пример получения `transactionIdentifier` см. в разделе [Отправка Revenue](../ios-operations.md#send-revenue).

{% note alert %}

Значение должно быть передано вместе с [receiptData](#property_receiptData).

{% endnote %}
