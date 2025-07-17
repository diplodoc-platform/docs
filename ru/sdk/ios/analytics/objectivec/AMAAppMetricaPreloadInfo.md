# Класс AMAAppMetricaPreloadInfo

Класс содержит информацию для отслеживания предустановленных приложений.

## Методы экземпляра

#|
|| [-initWithTrackingIdentifier:](#method_initWithTrackingIdentifier) | Инициализирует объект класса `AMAAppMetricaPreloadInfo` с указанным `trackingID`. ||
|| [-setAdditionalInfo:forKey:](#method_setAdditionalInfo) | Задает дополнительные параметры в виде пар <q>ключ-значение</q>, которые используются для [отслеживания предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md). ||
|#

## Описание методов {#method_detail}

### -initWithTrackingIdentifier: {#method_initWithTrackingIdentifier}

```objectivec translate=no
- (instancetype)initWithTrackingIdentifier:(NSString *)trackingID
```

Инициализирует объект класса `AMAAppMetricaPreloadInfo` с указанным `trackingID`.

**Параметры:**

#|
|| `trackingID` | Tracking ID для отслеживания предустановленных приложений. ||
|#

**Возвращает:**

Объект класса `AMAAppMetricaPreloadInfo`.

### -setAdditionalInfo:key: {#method_setAdditionalInfo}

```objectivec translate=no
- (void)setAdditionalInfo:(NSString *)info forKey:(NSString *)key
```

Задает дополнительные параметры в виде пар <q>ключ-значение</q>, которые используются для [отслеживания предустановленных приложений](../../../../mobile-tracking/preinstalled-app-attr.md).

Метод может быть вызван многократно для задания нескольких пар дополнительных сведений.

**Параметры:**

#|
|| `info` | Значение дополнительного параметра. Не может быть `nil`. Пары со значением `nil` будут проигнорированы. ||
|| `key` | Ключ дополнительного параметра. Не может быть `nil`. Пары с ключом `nil` будут проигнорированы. ||
|#
