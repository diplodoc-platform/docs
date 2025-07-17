# Класс AMAMutableAdRevenueInfo

Изменяемая версия класса [AMAAdRevenueInfo](AMAAdRevenueInfo.md) информацией о рекламной выручке (Ad Revenue).

Объект `AMAMutableAdRevenueInfo` должен быть передан на сервер AppMetrica с помощью метода [reportAdRevenue](AMAAppMetrica.md#method_reportAdRevenue) класса [AMAAppMetrica](AMAAppMetrica.md).

## Свойства {#property_summary}

#|
|| [adType](#property_adType) | Тип объявления. Смотрите возможные значения в [AMAAdType](AMAAdType.md). ||
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

`(nonatomic, assign) AMAAdType adType`

Тип объявления. Смотрите возможные значения в [AMAAdType](AMAAdType.md).

### adNetwork {#property_adNetwork}

`(nonatomic, copy, nullable) NSString *adNetwork`

Рекламная сеть. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitID {#property_adUnitID}

`(nonatomic, copy, nullable) NSString *adUnitID`

Идентификатор рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adUnitName {#property_adUnitName}

`(nonatomic, copy, nullable) NSString *adUnitName`

Название рекламного блока. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementID {#property_adPlacementID}

`(nonatomic, copy, nullable) NSString *adPlacementID`

Идентификатор места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### adPlacementName {#property_adPlacementName}

`(nonatomic, copy, nullable) NSString *adPlacementName`

Название места размещения рекламы. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### precision {#property_precision}

`(nonatomic, copy, nullable) NSString *precision`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Максимальная длина — 100 символов. Если значение превышает этот предел, оно будет усечено AppMetrica.

### payload {##property_payload}

`(nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *payload`

Точность. Например: <q>publisher_defined</q>, <q>estimated</q>. Произвольный payload: дополнительная информация, представленная в виде пар ключ-значение. Максимальный размер составляет 30 КБ. Если значение превышает этот предел, оно будет усечено AppMetrica.
