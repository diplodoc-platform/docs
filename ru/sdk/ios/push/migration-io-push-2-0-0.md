# Руководство по миграции на версию 2.0.0

При миграции приложения с `YandexMobileMetricaPush` на `AppMetricaPush` будут сохранены основные идентификаторы и данные, то есть процесс перехода на новую версию не должен вызвать проблем и аномалий в отчетах.

Для миграции на новую версию выполните следующие шаги:

1. Обновите AppMetrica SDK по [инструкции](../analytics/migration-io-5-0-0.md).
2. Замените зависимости. Необходимые изменения указаны в [разделе по переименованию зависимостей](#rename-modules).
3. Убедитесь, что вы не используете [2 версии AppMetrica Push SDK одновременно](#two-versions).
4. Импортируйте зависимости в коде. Необходимые изменения указаны в [разделе про импортирование зависимостей](#import-modules).
5. В коде проекта замените те классы и методы, которые были просто переименованы. Необходимые изменения указаны в [разделе по переименованию API](#rename-api).
6. При возникновении вопросов напишите в [поддержку](../../../troubleshooting/feedback-new.md).

## Переименованные зависимости {#rename-modules}

{% list tabs %}

- CocoaPods

  ```ruby translate=no
  pod 'YandexMobileMetricaPush', '~> 1.3.0'
  ```
  
  Замените на:
  
  ```ruby translate=no
  pod 'AppMetricaPush', '~> 2.0.0' # Основной модуль для работы с Push SDK, обязателен для подключения
  pod 'AppMetricaPushLazy', '~> 2.0.0' # Дополнительный модуль для Lazy пушей
  ```

- Package.swift

  #### Если используется Package.swift манифест

  1. Удалите из файла `Package.swift` в вашем проекте зависимость `.package` с `metrica-push-sdk-ios`, а также все указания на зависимости в разделе `targets:` внутри вашего проекта.
  2. Вставьте следующий код для добавления новой зависимости от `push-sdk-ios`:

     ```swift translate=no
     dependencies: [
        .package(
           url: "https://github.com/appmetrica/push-sdk-ios",
           from: "2.0.0"
        )
     ],
     ```

  3. Добавьте необходимые модули к таргетам вашего проекта.

     Модули AppMetrica Push SDK, которые вы можете подключить в зависимости от потребностей вашего проекта:

     * `AppMetricaPush` — обязательный основной модуль Push SDK. Должен быть подключен для работы.
     * `AppMetricaPushLazy` — дополнительный модуль для Lazy пушей.

     ```swift translate=no
     .target(
        name: "MyTargetName",
        dependencies: [
           .product(name: "AppMetricaPush", package: "push-sdk-ios"),
           // .product(name: "AppMetricaPushLazy", package: "push-sdk-ios"), // Этот модуль отлючен
        ]
     ),
     ```

{% endlist %}

## Одновременное использование двух версий AppMetrica Push SDK {#two-versions}

Переименованы группа и названия основных артефактов, поэтому в одном приложении могут использоваться сразу две версии AppMetrica Push SDK: AppMetrica Push версий 1.3.0 и ниже (`YandexMobileMetricaPush`) и версий 2.0.0 и выше (`AppMetricaPush`). Такая ситуация нежелательна из-за двойной обработки пуш-уведомлений и необходимости реализовывать свой `UINotificationCenterDelegate` для вызова обработчиков из разных версий AppMetrica Push SDK.

### Как убедиться, что не используется YandexMobileMetricaPush

{% list tabs %}

- CocoaPods

  Откройте файл `Podfile.lock` и выполните поиск `YandexMobileMetricaPush`.

  Так же по блоку `PODS` в файле `Podfile.lock` можно понять какая зависимость ссылается на `YandexMobileMetricaPush`.

  ```
  PODS:
    ...
     FizzLibarry (10.0.0):
      - BuzzLibrary (= 11.0.0)
      - YandexMobileMetricaPush (< 2.0.0, >= 1.3.0)
    ...
  ```

- SPM в Xcode

  #### Если зависимости установлены через Xcode

  Откройте проект в Xcode. Убедитесь, что в `Package Dependencies` нет `YandexMobileMetricaPush`.

- Package.swift

  #### Если используется Package.swift манифест
  
  Если ваш проект использует Package.swift манифест для управления зависимостями, выполните в терминале команду `swift package show-dependencies` в директории вашего проекта. Это выведет список всех зависимостей проекта, включая транзитивные.

  ```bash translate=no
  .
  └── fizz-library<https://github.com/appmetrica/fizz@10.0.0>
    ├──buzz-library<https://github.com/appmetrica/buzz@28.0.0>
    ├── metrica-sdk-push-ios<https://github.com/yandexmobile/metrica-sdk-push-ios@1.3.0>
  ```

  Также можно проверить файл `Package.resolved` на наличие зависимости  `YandexMobileMetricaPush`.

  ```json translate=no
  {
    "object": {
      "pins": [
        //...
        {
          "package": "YandexMobileMetricaPush",
          "repositoryURL": "https://github.com/yandexmobile/metrica-sdk-push-ios",
          "state": {
            "branch": null,
            "revision": "37012eb6d43ad7d9fc32801855f0eb62a53deec7",
            "version": "1.3.0"
          }
        },
        //...
      ]
    },
    // ...
  }
  ```

{% endlist %}

## Импортирование зависимостей {#import-modules}

{% list tabs group=instructions %}

- Swift

  ```swift translate=no
  import YandexMobileMetricaPush
  ```

  Замените на:

  ```swift translate=no
  import AppMetricaPush
  import AppMetricaPushLazy // дополнительный модуль для Lazy пушей
  ```

- Objective-C

  ```obj-c translate=no
  #import <YandexMobileMetricaPush/YandexMobileMetricaPush.h>
  ```

  Замените на:

  ```obj-c translate=no
  #import <AppMetricaPush/AppMetricaPush.h>
  #import <AppMetricaPushLazy/AppMetricaPushLazy.h> // дополнительный модуль для Lazy пушей
  ```

{% endlist %}

## Переименование API {#rename-api}

{% list tabs group=instructions %}

- Swift

  Префикс `YMP` удален.

  * Интерфейс `YMPYandexMetricaPush` переименован в `AppMetricaPush`.
    * Метод `userNotificationCenterDelegate` удален. Используйте свойство `userNotificationCenterDelegate`.
    * Метод `userNotificationCenterHandler` удален. Используйте свойство `userNotificationCenterHandler`.
  * Протокол `YMPUserNotificationCenterDelegate` переименован в `UserNotificationCenterDelegate`.
  * Протокол `YMPUserNotificationCenterHandling` переименован в `UserNotificationCenterHandling`.
  * Перечисление `YMPYandexMetricaPushEnvironment` переименовано в `AppMetricaPushEnvironment`.

- Objective-C

  Префикс `YMP` сменился на `AMP`.

  * Интерфейс `YMPYandexMetricaPush` переименован в `AMPAppMetricaPush`.
    * Метод класса `userNotificationCenterDelegate` переименован в свойство класса `userNotificationCenterDelegate`.
    * Метод класса `userNotificationCenterHandler` переименован в свойства класса `userNotificationCenterHandler`.
  * Протокол `YMPUserNotificationCenterDelegate` переименован в `AMPUserNotificationCenterDelegate`.
  * Протокол `YMPUserNotificationCenterHandling` переименован в `AMPUserNotificationCenterHandling`.
  * Перечисление `YMPYandexMetricaPushEnvironment` переименовано в `AMPAppMetricaPushEnvironment`.

{% endlist %}
