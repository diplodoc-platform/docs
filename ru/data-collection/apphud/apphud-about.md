# AppMetrica и Apphud

AppMetrica интегрирована с [Apphud](https://docs.apphud.com/docs/what-is-apphud), одним из ведущих решений для отслеживания покупок и подписок в мобильных приложениях. Apphud обеспечивает точность отслеживания доходов приложений на уровне 99,9%, что гарантирует учет всех возможных сценариев покупки.

Преимущества:

- Экономия ресурсов разработки — не нужны интеграции со сторонними решениями. Модуль Apphud можно настроить за [несколько шагов](#enable-apphud).
- Актуальность и точность данных — отслеживание подписок для каждого сценария покупки, адаптация к конкретному магазину и операционной системе. 
- Данные о доходах доступны в отчетах — можно сегмиентировать аудиторию по платежеспособности и другим параметрам покупки, выявлять каналы и регионы, которые приносят больше всего платящих пользователей. Смотрите отчеты о [доходах](../../mobile-reports/revenue-report.md), [событиях](../../mobile-reports/events-report.md), [аудитории](../../mobile-reports/audience-report.md) и [привлечении пользователей](../../mobile-reports/user-acquisition-report.md).

Возможности:

- App Store & iOS

    - Поддержка полных возвратов, включая обновления с суммой возврата.
    - Поддержка подписок, совместно используемых семьей — транзакции, совместно используемые с другими пользователями через Family Sharing, не учитываются.
    - Правильный учет комиссий App Store.
    - Поддержка платных ознакомительных и рекламных предложений.
    - Поддержка кодов предложений подписки.
    - Автоматическое восстановление покупок в SDK.

- Google Play & Android

    - Поддержка подписок с несколькими базовыми планами.
    - Поддержка сложных сценариев, например, бесплатная пробная версия + платная скидка + обычная цена.
    - Поддержка всех типов предложений: бесплатная пробная версия, скидка, фиксированная цена и абсолютная скидка.

## Как подключить Apphud {#enable-apphud}

Трекинг через Apphud — платная опция, которая доступна на [тарифах](../../common/pricing/uae-currency.md#pro-upgrade) Custom и Pro. У опции есть бесплатный лимит `MTR < 10000$`.

{% note warning "" %}

1. Опция трекинга через Apphud может быть недоступна в некоторых регионах.
2. Apphud работает только для Google Play и App Store. Для других магазинов приложений, например, Huawei AppGallery, информация не собирается.

{% endnote %}

1. Активируйте опцию Apphud в разделе **{{ organization }}** → **{{ tariff }}**.

   - Если у вас тариф Free, перейдите на тариф Custom или Pro и заполните реквизиты. После этого опция с бесплатным лимитом будет активирована автоматически.
   - Если у вас тариф Custom или Pro, опция с бесплатным лимитом будет активирована автоматически.

2. Обновите SDK AppMetrica. AppMetrica поддерживает трекинг через Apphud начиная с версий [Android 7.6.0](../../sdk/android/analytics/quick-start.md), [iOS 5.9.0](../../sdk/ios/analytics/quick-start.md).
3. Отключите автосбор покупок и подписок из Google Play, App Store в SDK AppMetrica.

   {% list tabs %}
   
   - Android
   
     {% list tabs group=instructions %}

     - Kotlin
       
       ```kotlin translate=no
       val config = AppMetricaConfig.newConfigBuilder(API_KEY)
                    .withRevenueAutoTrackingEnabled(false)
                    .build()
                AppMetrica.activate(context, config)
       ```

     - Java
       
       ```java translate=no
       AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
                    .withRevenueAutoTrackingEnabled(false)
                    .build();
                AppMetrica.activate(context, config);
       ```

     {% endlist %}
   
   - iOS
   
     {% list tabs group=instructions %}

     - Swift
       
       ```swift translate=no
       let configuration = AppMetricaConfiguration(apiKey: "API_KEY")!
       configuration.revenueAutoTrackingEnabled = false
       AppMetrica.activate(with: configuration)
       ```

     - Objective-C
       
       ```obj-c translate=no
       AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithAPIKey:@"API_KEY"];
       configuration.revenueAutoTrackingEnabled = NO;
       [AMAAppMetrica activateWithConfiguration:configuration];
       ```

     {% endlist %} 
   
   {% endlist %}

4. Отключите ручной сбор покупок (если он был настроен) из Google Play, App Store.
   
   Попробуйте поискать в коде вызовы `AppMetrica#reportRevenue(Revenue)` и удалить их. Подробности о реализации ручного сбора читайте в разделах для [Android](../../sdk/android/analytics/android-operations.md#send-revenue-key), [iOS](../../sdk/ios/analytics/ios-operations.md#send-revenue-key).
   
5. Если вы использовали [загрузку событий In-app Revenue](../../mobile-api/post/post-revenue.md) в [POST API](../../mobile-api/post/about.md) для сбора покупок и подписок из Google Play, App Store, — отключите его.
   
   {% note info %}
   
   Рекомендуется отключить все сборы (ручные и автоматические), чтобы информация не дублировалась в отчетах.
   
   {% endnote %}
   
   
6. Подключите модуль Apphud в коде приложения.

   {% list tabs %}
   
   - Android
     
     Версия модуля Apphud должна совпадать с версией SDK AppMetrica.
   
     ```kotlin translate=no
     dependencies {
       // AppMetrica SDK
       implementation("io.appmetrica.analytics:{{ io-appmetrica-analytics-analytics }}")
       // AppMetrica SDK Apphud module
       // You should use the same versions for AppMetrica and Apphud modules
       implementation("io.appmetrica.analytics:analytics-apphud:{{ io-appmetrica-analytics-analytics }}")
     }
     ```
   
   - iOS
   
     {% list tabs %}
     
     - Cocoapods
       
       ```ruby translate=no
       pod 'AppMetricaApphudAdapter', '~> {{ apphud-adapter-ios }}'
       ```
     
     - SPM

       ```swift translate=no
       dependencies: [
           .package(
               url: "https://github.com/appmetrica/appmetrica-sdk-apphud-adapter-ios",
               from: "{{ apphud-adapter-ios }}"
           )
       ]
       ```
     
     {% endlist %}
   
   {% endlist %}

7. Заполните информацию о вашем приложении в разделе **{{ settings }}** → **{{ tracking-apphud }}** интерфейса AppMetrica.

   {% list tabs %}

   - Android приложение
  
     - Название пакета Google Play.
     - Учетная запись службы JSON. 
    
       Для отслеживания изменений статуса подписок необходимо создать и загрузить в AppMetica json-файл сервисного аккаунта. Подробнее о том как создать json-файл читайте в [документации Apphud](https://docs.apphud.com/docs/google-play-service-credentials).

     - Уведомления разработчика Google в режиме реального времени.

       После загрузки JSON-файла в интерфейсе появится строка, которую необходимо скопировать в **Google Play Console** → **Your App** → **Monetization Setup**. Подробнее читайте в [документации Google](https://developer.android.com/google/play/billing/getting-ready?hl=ru#configure-rtdn).

     - Google Play Reduced Service Fee.
    
       Если вы зарегистрированы в программе [Google Play Reduced Service Fee](https://support.google.com/googleplay/android-developer/answer/11131145), укажите даты действия.

     ![](../../../_images/android-app-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

   - iOS приложение
  
     - Bundle ID.
     - App Store Apple ID. 
       
       Его можно найти в **[App Store Connect](https://appstoreconnect.apple.com/)** → **Apps** → **App Information**.
     - App Store Shared Secret.

       {% cut "Как получить App Store Shared Secret" %}
       
       1. Откройте App Store Connect, перейдите в раздел [Apps](https://appstoreconnect.apple.com/apps) и выберите свое приложение.
       2. В секции **Features** слева перейдите в **Subscriptions**.
       3. На странице найдите раздел **App-Specific Shared Secret**, нажмите кнопку **Manage**.
       4. Создайте и скопируйте **Shared Secret**.
       5. В интерфейсе AppMetrica перейдите в раздел **{{ settings }}** → **{{ tracking-apphud }}** → **{{ iOS-app }}**.
       6. Вставьте **Shared Secret** для приложения в поле **App Store Shared Secret**.
       
       {% endcut %}

     - Apple Small Business Program.
       
       Если вы зарегистрированы в программе [Apple Small Business Program](https://developer.apple.com/app-store/small-business-program), укажите даты действия.
       
     - Уведомления сервера App Store.
       
       - API сервера App Store (StoreKit 2). Ключ для покупки в приложении.
         Закрытый ключ (In-App Purchase Key) из App Store Connect, который необходимо загрузить в AppMetrica. Подробнее о том как создать In-App Purchase Key читайте в [документации Apphud](https://docs.apphud.com/docs/app-store-credentials).

      - URL-адрес уведомлений сервера App Store версии V1 или V2.
    
        После загрузки In-App Purchase Key в интерфейсе появится строка — это URL-адрес для настройки уведомлений от App Store Server Notifications.

        {% cut "Как настроить уведомления от App Store Server Notifications" %}
        
        1. Скопируйте URL-адрес для уведомлений сервера App Store.
        2. Откройте App Store Connect, перейдите в раздел [Apps](https://appstoreconnect.apple.com/apps) и выберите свое приложение.
        3. В секции **General** слева перейдите в **App Information**.
        4. Внизу открывшейся страницы, в блоке **App Store Server Notifications** у пункта **Production Server URL** нажмите кнопку **Edit**.
        5. В поле **Production Server URL** введите URL-адрес из AppMetrica.
        6. Ниже в форме выберите **Version 2 Notifications** и нажмите **Save**. 
        
        {% endcut %}

        ![](../../../_images/url-apple-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

     - Issuer ID.

       Идентификатор эмитента из App Store Connect. Его можно найти в **App Store Connect** → **Users and Access** → **Keys** → **App Store Connect API**.

     ![](../../../_images/ios-app-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

   {% endlist %}

## Доступ в личном кабинете Apphud {#access}

В интеграции AppMetrica когда пользователь загружает сертификаты для приложения, на email владельца организации создается личный кабинет в сервисе Apphud. Пользователь получает доступ к своему приложению и всем отчетам Apphud в рамках выбранного тарифа. 

### Доступ для сотрудников {#user-access}

В кабинете Apphud можно настроить доступ к приложению для других сотрудников.

Если пользователь, который загружал сертификаты, не является владельцем приложения, он может попросить владельца приложения пройти [процедуру восстановления доступа](https://docs.apphud.com/docs/access-recovery) и затем в кабинете Apphud выдать пользователю нужный доступ к приложению.

## Как отключить Apphud {#disable-apphud}

1. В интерфейсе AppMetrica перейдите в **{{ organization }}** → **{{ tariff }}**.
2. На карточке вашего тарифа нажмите кнопку **{{ settings-button }}**.
3. Найдите в списке опцию **{{ apphud-inapp }}** и справа установите **{{ disabled }}**.
   
   ![](../../../_images/apphud-off-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 700px;"}

4. Нажмите кнопку **{{ save }}**.
5. Если вы хотите отключить модуль Apphud в SDK, удалите зависимости в коде приложения.

<!-- ## Личный кабинет в Apphud {#account-apphud} -->

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}


