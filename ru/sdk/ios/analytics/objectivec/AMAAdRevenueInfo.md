# Класс AMAAdRevenueInfo

Класс содержит неизменяемую информацию о рекламной выручке (Ad Revenue).

Чтобы изменить информацию о рекламной выручке, воспользуйтесь классом [AMAMutableAdRevenueInfo](AMAMutableAdRevenueInfo.md).

Объект `YMMAdRevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportAdRevenue](AMAAppMetrica.md#method_reportAdRevenue) класса [AMAAppMetrica](AMAAppMetrica.md).

## Методы экземпляра {#instance_summary}

#|
|| [-initWithAdRevenue:adRevenue:currency:](#method_initWithAdRevenue__adRevenue__currency) | Инициализирует экземпляр класса `AMAAdRevenueInfo` для передачи информации о рекламной выручке. ||
|#

## Свойства {#property_summary}

#|
|| [adRevenue](#property_adRevenue) | Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным. ||
|| [currency](#property_currency) | Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217. ||
|| [adType](#property_adType) | Тип объявления. Смотрите возможные значения в [AMAAdType](AMAAdType.md). ||
|| [adNetwork](#property_adNetwork) | Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [precision](#property_precision) | Точность. Например: «publisher_defined», «estimated». Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [payload](#property_payload) | Точность. Например: «publisher_defined», «estimated». Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|#

## Описание методов {#method_detail}

### -initWithAdRevenue:adRevenue:currency: {#method_initWithAdRevenue__adRevenue__currency}

```objectivec translate=no
- (instancetype)initWithAdRevenue:(NSDecimalNumber *)adRevenue currency:(NSString *)currency
```

Инициализирует экземпляр класса `AMAAdRevenueInfo` для передачи информации о рекламной выручке.

**Параметры:**

#|
|| `adRevenue` | Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным. ||
|| `currency` | Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217. ||
|#

**Возвращает:**

Объект класса `AMAAdRevenueInfo`.

## Описание свойств {#property_detail}

### adRevenue {#property_adRevenue}

`(nonatomic, strong, readonly) NSDecimalNumber *adRevenue`

Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным.

### currency {#property_currency}

`(nonatomic, copy, readonly) NSString *currency`

Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217.

### adType {#property_adType}

`(nonatomic, assign, readonly) AMAAdType adType`

Тип объявления. Смотрите возможные значения в [AMAAdType](AMAAdType.md).

### adNetwork {#property_adNetwork}

`(nonatomic, copy, nullable, readonly) NSString *adNetwork`

Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitID {#property_adUnitID}

`(nonatomic, copy, nullable, readonly) NSString *adUnitID`

Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitName {#property_adUnitName}

`(nonatomic, copy, nullable, readonly) NSString *adUnitName`

Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementID {#property_adPlacementID}

`(nonatomic, copy, nullable, readonly) NSString *adPlacementID`

Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementName {#property_adPlacementName}

`(nonatomic, copy, nullable, readonly) NSString *adPlacementName`

Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### precision {#property_precision}

`(nonatomic, copy, nullable, readonly) NSString *precision`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### payload {#property_payload}

`(nonatomic, copy, nullable, readonly) NSDictionary<NSString *, NSString *> *payload`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica.
