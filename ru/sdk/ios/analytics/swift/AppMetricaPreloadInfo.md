# Класс AppMetricaPreloadInfo

Класс содержит информацию [для отслеживания предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md).

## Методы экземпляра {#instance_summary}

#|
|| [init?(trackingIdentifier:)](#method_initWithTrackingIdentifier) | Инициализирует объект класса `AppMetricaPreloadInfo` с указанным `trackingID`. ||
|| [setAdditional(info:forKey:)](#method_setAdditionalInfo) | Задает дополнительные параметры в виде пар <q>ключ-значение</q>, которые используются для [отслеживания предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md). ||
|#

## Описание методов {#method_detail}

### init?(trackingIdentifier:) {#method_initWithTrackingIdentifier}

```swift translate=no
init?(trackingIdentifier trackingID: String)
```

Инициализирует объект класса `AppMetricaPreloadInfo` с указанным `trackingID`.

**Параметры:**

#|
|| `trackingID` | Tracking ID для отслеживания предустановленных приложений. ||
|#

**Возвращает:**

Объект класса `AppMetricaPreloadInfo`.

### setAdditional(info:forKey:) {#method_setAdditionalInfo}

```swift translate=no
func setAdditional(info: String, forKey key: String)
```

Задает дополнительные параметры в виде пар <q>ключ-значение</q>, которые используются для [отслеживания предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md).

Метод может быть вызван многократно для задания нескольких пар дополнительных сведений.

**Параметры:**

#|
|| `info` | Значение дополнительного параметра. Не может быть `nil`. Пары со значением `nil` будут проигнорированы. ||
|| `key` | Ключ дополнительного параметра. Не может быть `nil`. Пары с ключом `nil` будут проигнорированы. ||
|#
