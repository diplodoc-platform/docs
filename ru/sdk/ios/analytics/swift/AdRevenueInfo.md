# Класс AdRevenueInfo

Класс содержит неизменяемую информацию о рекламной выручке (Ad Revenue).

Чтобы изменить информацию о доходах, воспользуйтесь классом [MutableAdRevenueInfo](MutableAdRevenueInfo.md).

Объект `AdRevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportAdRevenue](AppMetrica.md#method_reportAdRevenue) класса [AppMetrica](AppMetrica.md).

## Методы экземпляра {#instance_summary}

#|
|| [init(adRevenue:currency:)](#method_init__adRevenue__currency) | Инициализирует экземпляр класса `AdRevenueInfo` для передачи информации о рекламной выручке. ||
|#

## Свойства {#property_summary}

#|
|| [adRevenue](#property_adRevenue) | Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным. ||
|| [currency](#property_currency) | Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217. ||
|| [adType](#property_adType) | Тип объявления. Смотрите возможные значения в [AdType](AdType.md). ||
|| [adNetwork](#property_adNetwork) | Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [precision](#property_precision) | Точность. Например: «publisher_defined», «estimated». Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [payload](#property_payload) | Точность. Например: «publisher_defined», «estimated». Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|#

## Описание методов {#method_detail}

### init(adRevenue:currency:) {#method_init__adRevenue__currency}

```swift translate=no
init(adRevenue: NSDecimalNumber, currency: String)
```

Инициализирует экземпляр класса `AdRevenueInfo` для передачи информации о рекламной выручке.

**Параметры:**

#|
|| `adRevenue` | Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным. ||
|| `currency` | Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217. ||
|#

**Возвращает:**

Объект класса `AdRevenueInfo`.

## Описание свойств {#property_detail}

### adRevenue {#property_adRevenue}

`var adRevenue: NSDecimalNumber { get }`

Сумма денег, полученных за счет дохода от рекламы. Не может быть отрицательным.

### currency {#property_currency}

`var currency: String { get }`

Валюта, в которой представлен `adRevenue`. Должен быть в формате ISO-4217.

### adType {#property_adType}

`var adType: AdType { get }`

Тип объявления. Смотрите возможные значения в [AdType](AdType.md).

### adNetwork {#property_adNetwork}

`var adNetwork: String? { get }`

Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitID {#property_adUnitID}

`var adUnitID: String? { get }`

Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitName {#property_adUnitName}

`var adUnitName: String? { get }`

Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementID {#property_adPlacementID}

`var adPlacementID: String? { get }`

Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementName {#property_adPlacementName}

`var adPlacementName: String? { get }`

Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### precision {#property_precision}

`var precision: String? { get }`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### payload {#property_payload}

`var payload: [String: String]? { get }`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica.
