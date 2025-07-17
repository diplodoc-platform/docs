# Класс MutableAdRevenueInfo

Изменяемая версия класса [AdRevenueInfo](AdRevenueInfo.md) с информацией о рекламной выручке.

Объект `MutableAdRevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportAdRevenue](AppMetrica.md#reportadrevenueonfailure-method_reportadrevenue) класса [AppMetrica](AppMetrica.md).

## Свойства {#property_summary}

#|
|| [adType](#property_adType) | Тип объявления. Смотрите возможные значения в [AdType](AdType.md). ||
|| [adNetwork](#property_adNetwork) | Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitID](#property_adUnitID) | Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adUnitName](#property_adUnitName) | Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementID](#property_adPlacementID) | Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [adPlacementName](#property_adPlacementName) | Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [precision](#property_precision) | Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|| [payload](#property_payload) | Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica. ||
|#

## Описание свойств {#property_detail}

### adType {#property_adType}

`var adType: AdType`

Тип объявления. Смотрите возможные значения в [AdType](AdType.md).

### adNetwork {#property_adNetwork}

`var adNetwork: String?`

Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitID {#property_adUnitID}

`var adUnitID: String?`

Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitName {#property_adUnitName}

`var adUnitName: String?`

Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementID {#property_adPlacementID}

`var adPlacementID: String?`

Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementName {#property_adPlacementName}

`var adPlacementName: String?`

Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### precision {#property_precision}

`var precision: String?`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### payload {#property_payload}

`var payload: [String: String]?`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica.
