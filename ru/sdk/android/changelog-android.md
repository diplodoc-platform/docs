# История изменений

## AppMetrica SDK

### Версия 7.9.0 {#s-7-9-0}

Релиз 8 мая 2025 г.

- Основные компоненты AppMetrica SDK перенесены в основной процесс приложения. Теперь AppMetrica SDK полностью работает в основном процессе приложения. Отказ от отдельного процесса снимает возможные интеграционные проблемы с другими библиотеками вроде Firebase Perfomance. 
- Добавлена поддержка для будущего автосбора ad revenue данных из плагинов.
- Исправлены возможные ANR:
   - `at com.android.billingclient.api.BillingClientImpl.zzaJ(BillingClientImpl.java:1)` ([issue#19](https://github.com/appmetrica/appmetrica-sdk-android/issues/19)).
   - `at io.appmetrica.analytics.impl.Uf.onInstallReferrerSetupFinished(Uf.java:3)` ([issue#20](https://github.com/appmetrica/appmetrica-sdk-android/issues/20)).

### Версия 7.8.0 {#s-7-8-0}

Релиз 10 апреля 2025 г.

- Добавлен опциональный модуль `io.appmetrica.analytics:analytics-screenshot`. Он отслеживает создание пользователем скриншота. При этом отправляется клиентское событие `appmetrica_system_event_screenshot`. Для корректной работы нужно добавить в AndroidManifest.xml разрешение [android.permission.DETECT_SCREEN_CAPTURE](https://developer.android.com/reference/android/Manifest.permission#DETECT_SCREEN_CAPTURE).
- Исправлена проблема дублирования автособранных данных об inapp-покупках.
- Исправлена проблема автоматического сбора сведений об очень старых inapp-покупках, которые могли засчитаться текущей датой и исказить отчет.
- **Обновление совместимых зависимостей:**
   - Google Play Services Location до `com.google.android.gms:play-services-location:21.0.1`;
   - Google Play Billing до `com.android.billingclient:billing:7.1.1`;
   - Google Play Ads до `com.google.android.gms:play-services-ads:24.1.0`;
   - AppLovin SDK до `com.applovin:applovin-sdk:13.1.0`;
   - FairBid SDK до `com.fyber:fairbid-sdk:3.59.0`;
   - AppHud SDK до `com.apphud:ApphudSDK-Android:2.9.1`;
   - Google Play Services AppSet ID до `com.google.android.gms:play-services-appset:16.1.0`;
   - Google Play Services Ads Identifiers до `com.google.android.gms:play-services-ads-identifier:18.2.0`.
- В `AppMetricaLibraryAdapter` добавлена возможность управлять доступом к рекламным идентификаторам.

### Версия 7.7.0 {#s-7-7-0}

Релиз 14 февраля 2025 г.

* В события ad revenue добавлена информация об исходном типе рекламы.
* Добавлен тип `APP_OPEN` для ad revenue событий в AdMob.
* Обновлен Apphud SDK до версии 2.8.4 в модуле ad revenue.
* Исправлены возможные ANR:
   - `at io.appmetrica.analytics.impl.nm.onDestroy(nm.java:1)` ([issue#16](https://github.com/appmetrica/appmetrica-sdk-android/issues/16)).
   - `at io.appmetrica.analytics.networktasks.internal.NetworkCore.stopTasks(NetworkCore.java:1)` ([issue#17](https://github.com/appmetrica/appmetrica-sdk-android/issues/17)).

### Версия 7.6.0 {#s-7-6-0}

Релиз 23 января 2025 г.

* Исправлена возможная проблема со статистикой (установки и новые пользователи) при одновременном использовании плагинов AppMetrica SDK (Unity, ReactNative, Flutter) и плагинов Yandex Ads SDK.
* Исправлен возможный ANR при обращении к API AppMetrica SDK до активации AppMetrica SDK.

### Версия 7.5.0 {#s-7-5-0}

Релиз 5 декабря 2024 г.

* Добавлен API для управления доступом к рекламным идентификаторам (GAID, Huawei OAID). Подробнее в [документации](analytics/android-operations.md#track-adv-identifiers).

### Версия 7.4.0 {#s-7-4-0}

Релиз 29 ноября 2024 г.

* Доработан механизм обработки реферрера, что позволило исправить ошибку получения отложенного диплинка и его параметров при установке приложения по трекинговой ссылке на последних версиях браузера с движком chromium (Google Chrome, Yandex Browser и т.д.).

### Версия 7.3.0 {#s-7-3-0}

Релиз 5 ноября 2024 г.

* Добавлены методы `AppMetrica#reportAnr()` и `IReporter#reportAnr()`, которые позволяют отправлять сведения об ANR вручную.
* Исправлено возможное падение `java.lang.IllegalArgumentException:... at io.appmetrica.analytics.impl.K7.a(K7.java:27)`.
* Исправлено предупреждение `Missing class com.google.android.gms.ads.AdValue` во время сборки приложения ([issue#10](https://github.com/appmetrica/appmetrica-sdk-android/issues/10)).

### Версия 7.2.2 {#s-7-2-2}

Релиз 23 октября 2024 г.

* Добавлена дополнительная проверка полной инициализации AppMetrica SDK.

### Версия 7.2.1 {#s-7-2-1}

Релиз 3 октября 2024 г.

* Улучшено определение факта непервого запуска приложения в рамках активации AppMetrica SDK через адаптер для сторонних библиотек.
* При отправке событий через адаптер для сторонних библиотек до его активации или с некорректными аргументами они будут проигнорированы вместо выбрасывания исключения.

### Версия 7.2.0 {#s-7-2-0}

Релиз 11 сентября 2024 г.

* Удален локальный механизм детектирования собственных крэшей AppMetrica SDK, AppMetrica Push SDK в пользу серверного решения.
* Добавлен модуль `io.appmetrica.analytics:analytics-apphud` для интеграции с Apphud.
* Добавлен API для упрощения отправки ILRD (Impression Level Revenue Data) из [Google AdMob](../../sdk/android/analytics/android-operations.md#google-admob) для рекламного формата App open ad.
* Улучшено логирование событий.

### Версия 7.1.0 {#s-7-1-0}

Релиз 21 августа 2024 г.

- Добавлен API для упрощения отправки ILRD (Impression Level Revenue Data) из:
  - [Digital Turbine](../../sdk/android/analytics/android-operations.md#digital-turbine)
  - [Google AdMob](../../sdk/android/analytics/android-operations.md#google-admob)
  - [Applovin MAX](../../sdk/android/analytics/android-operations.md#applovin)
- Добавлена ускоренная отправка на сервер некоторых событий (атрибуций из внешних SDK, `e-commerce`, `revenue`, `ad revenue` (Impression Level Revenue Data)).

### Версия 7.0.0 {#s-7-0-0}

Релиз 28 июня 2024 г.

**Ломающие изменения:**

* Текущая версия `minSdkVersion` повышена до `21` (Android 5.0).
* Версии `sourceCompatibility` и `targetCompatibility` повышены до Java 1.8.

**Дополнения:**

* Добавлена корректировка сообщений крэшей и ошибок c некорректным форматом. Корректировка исправит возможное падение

   ```java translate=no
   java.lang.IllegalArgumentException: Unpaired surrogate at index 14 at io.appmetrica.analytics.protobuf.nano.CodedOutputByteBufferNano.encodedLengthGeneral(Unknown Source)
   ```

* Исправлен возможный ANR `at io.appmetrica.analytics.impl.sk.a(sk.java:1)`.
* Исправлен возможный крэш

   ```java translate=no
   java.lang.NullPointerException: Attempt to invoke virtual method 'void io.appmetrica.analytics.impl.Nb.a(io.appmetrica.analytics.impl.ie)' on a null object reference at io.appmetrica.analytics.impl.Qb.b(SourceFile:10)
   ```

* Добавлен лимит в 100 событий, отправляемых в одном запросе на сервер. Введение лимита повысит производительность SDK в условиях нестабильного сетевого канала.
* Оптимизирована работа с потоками на клиентской стороне и удалены устаревшие проверки корректности интеграции SDK. Оптимизация снизит время синхронной части активации SDK.

### Версия 6.5.0 {#s-6-5-0}

Релиз 26 апреля 2024 г.

* Добавлена возможность отправки атрибуции из Singular (требуемый API доступен в [Singular SDK 12.5.1 и выше](https://support.singular.net/hc/en-us/articles/360041068651-Android-SDK-Change-Log)). Подробности в статье [Импорт атрибуций из других SDK](../../data-collection/attribution-integration.yaml).
* Удалена обфускация названий аргументов методов в API.

### Версия 6.4.0 {#s-6-4-0}

Релиз 11 апреля 2024 г.

* Добавлена поддержка автоматического получения `impression level revenue data` из источников: [Ironsource V7](https://developers.is.com/), [Fyber V3](https://developer.digitalturbine.com/hc/en-us).
* Исправлена ошибка, которая выводилась в системный лог:
   ```
   E ActivityThread: Failed to find provider info for com.yandex.preinstallsatellite.appmetrica.provider
   ```

### Версия 6.3.0 {#s-6-3-0}

Релиз 18 марта 2024 г.

* Добавлены дополнительная валидация формата `UUID` и восстановление некорректного значения `UUID`.
* Улучшен алгоритм детекта ANR — теперь ANR фиксируется только в том случае, если за отведенное время на главном потоке не смог выполниться единственный `Runnable`. Алгоритм находит “тяжелые“ задачи, приводящие к зависанию главного потока. Ранее детект ANR срабатывал, когда на главном потоке исполнялось большое количество небольших `Runnable` — в таких ситуациях стектрейс ANR обычно был неинформативен и малополезен.
* Теперь в результате подвисания одного `Runnable` будет формироваться один ANR отчет. Это уменьшит количество отчетов об ANR, но повысит их полезность.
* Исправлен возможный ANR `at io.appmetrica.analytics.internal.AppMetricaService.onCreate` ([issue#3](https://github.com/appmetrica/appmetrica-sdk-android/issues/3)).
* Исправлено возможное падение `org.json.JSONException: Forbidden numeric value: NaN` при отправке external атрибуций (`AppMetrica#reportExternalAttribution(...)`).

### Версия 6.2.1 {#s-6-2-1}

Релиз 26 января 2024 г.

* Исправлена ошибка в сериализации внешних атрибуций.

### Версия 6.2.0 {#s-6-2-0}

Релиз 22 января 2024 г.

* Добавлен метод `AppMetrica.reportExternalAttribution` для отправки атрибуций из сторонних библиотек. Подробности в статье [Импорт атрибуций из других SDK](../../data-collection/attribution-integration.yaml).
* Исправлена проблема, которая приводила к тому, что не выводились логи о сохранении и отправке событий на сервер.

### Версия 6.1.0 {#s-6-1-0}

Релиз 28 ноября 2023 г.

* Увеличен `buildToolsVersion` до `34.0.0`.
* Увеличен `targetSdkVersion` и `compileSdkVersion` до `34`.
* Обновлена версия kotlin-плагина до `org.jetbrains.kotlin:kotlin-gradle-plugin:1.6.21`.
* Поддержан автосбор покупок и подписок, совершаемых через библиотеку `com.android.billingclient:billing:6.0.0`. Удален автосбор покупок и подписок, совершаемых через библиотеку `com.android.billingclient:billing:4.+`. Теперь автосбор покупок и подписок доступен для версий `com.android.billingclient:billing:5.0.0` и выше.
* Исправлен возможный deadlock `at io.appmetrica.analytics.networktasks.internal.NetworkCore.onDestroy`.

### Версия 6.0.0 {#s-6-0-0}

Релиз 13 сентября 2023 г.

* Обновлены идентификатор библиотеки, корневой пакет и API. Подробнее в [инструкции по миграции](analytics/migration-io-6-0-0.md).
* Удалена интеграция с breakpad. Сейчас используется только Crashpad. Для отлова нативных крэшей нужно использовать зависимость `io.appmetrica.analytics:analytics-ndk-crashes:3.0.0`. Подробнее в разделе про [нативные крэши](analytics/android-operations.md#native-crashes).
* В модуле `io.appmetrica.analytics:analytics-ndk-crashes` обновлен крэшпад до коммита `9158eb7caa811b684c6bec7f9e9b5f52389d0ce0`.
* Разрешение `com.google.android.gms.permission.AD_ID` перемещено в модуль `io.appmetrica.analytics:analytics-identifiers`.
* Исправлен возможный warning при установке и запуске приложения `Class io.appmetrica.analytics.impl.ob.Zh failed lock verification and will run slower` и аналогичные ему.
* Исправлен возможный ANR `at io.appmetrica.analytics.impl.ob.p3$b.onServiceConnected(SourceFile:2)`.
* Работа с гео вынесена в отдельную зависимость: `io.appmetrica.analytics:analytics-location`. Теперь при необходимости можно отказаться от сбора координат AppMetrica SDK на этапе сборки приложения. Это может быть необходимо для отдельных категорий приложений в соответствии с политиками Google Play. Подробности в [документации](geo-exclude.md).
* Поддержан API для получения различных идентификаторов AppMetrica SDK (`DeviceId`, `DeviceIdHash`, `UUID`) — метод `AppMetrica#requestStartupParams`. Подробности в [документации](analytics/android-operations.md#get-ids).
* Поддержан API для указания типа устройства (телефон, планшет, ТV, авто). Подробности в [документации](analytics/android-operations.md#device-type).

### Версия 5.3.0 {#s-5-3-0}

Релиз 3 марта 2023 г.

* Исправлен возможный warning при установке и запуске приложения `Class com.yandex.metrica.impl.ob.Zh failed lock verification and will run slower` и аналогичные.
* Исправлен возможный ANR `at com.yandex.metrica.impl.ob.p3$b.onServiceConnected(SourceFile:2)`.
* Исправлены ошибки и повышена стабильность.

### Версия 5.2.0 {#s-5-2-0}

Релиз 19 сентября 2022 г.

* Добавлен API AdRevenue для передачи доходов рекламной монетизации на уровне показа (Impression-Level Revenue Data):
   * классы `AdRevenue`, `AdRevenue.Builder`.
   * Методы `reportAdRevenue(AdRevenue adRevenue)` в классе `YandexMetrica`, `reportAdRevenue(AdRevenue adRevenue)` в интерфейсе `IReportet`.
   * перечисление `AdType`.
* Версия targetSdkVersion = 33.

### Версия 5.0.1 {#s-5-0-1}

Релиз 29 июля 2022 г.

* Исправлена проблема, которая могла приводить к повторным ложным установкам.

### Версии 5.0.0 — 4.0.0

{% cut "5.0.0 — 4.0.0" %}

#### Версия 5.0.0 {#s-5-0-0}

Релиз 20 мая 2022 г.

{% note info %}

Начиная с версии AppMetrica Android SDK 5.0.0 и выше при переустановке приложения на смартфоне меняется appmetrica_device_id. Это обусловлено новыми политиками Google. Подробности в [документации](../../troubleshooting/troubleshooting.md#change-device-id).

{% endnote %}

* Получение рекламных идентификаторов вынесено в отдельную библиотеку `com.yandex.android:mobmetricalib-identifiers`. Подробнее в разделе [Получение рекламных идентификаторов](get-ad-id.md).
* По умолчанию выключен признак отправки информации о локации устройства. Чтобы включить отправку локации с событиями используйте один из методов: `withLocationTracking(boolean enabled)` или `setLocationTracking(boolean enabled)`.
* Добавлены @NonNull-аннотации для аргументов методов интерфейса `DeferredDeeplinkParametersListener`.
* Метод `reportNativeCrash` устарел и в будущих версиях будет удален.

#### Версия 4.2.0 {#s-4-2-0}

Релиз 17 февраля 2022 г.

* Добавлен новый API для отслеживания крэшей и ошибок из произвольных плагинов.

   Интерфейсы:
   * YandexMetricaPlugins;
   * IPluginReporter.

   Классы:
   * PluginErrorDetails;
   * PluginErrorDetails.Builder;
   * StackTraceItem;
   * StackTraceItem.Builder.

* Поддержан даунгрейд на версию 4.2.0 и выше с сохранением важных данных: идентификаторов устройства и т. д. Использовать даунгрейд не рекомендуется, это может привести к потере и искажению данных. Повторная атрибуция для таких пользователей не произойдет.
* Добавлена поддержка Google Play Billing Library версии 4.0.0. Поддержка версий 3.x продолжается.
* В методе `DeferredDeeplinkParametersListener` аргумент `referrer` стал `@NonNull`. В случае его отсутствия придет пустая строка.
* Убрали определение ROOT-статуса на устройствах с Android 12 и выше. На текущий момент все устройства с Android 12 будут считаться устройствами без ROOT-доступа.

* Исправлены ошибки и повышена стабильность:

   * Исправлен возможный крэш при попытке подключения к сервису MetricaService:
      ```
      Process: com.yandex :Metrica java.lang.RuntimeException: Unable to bind to service com.yandex.metrica.MetricaService Caused by: java.lang.IllegalArgumentException at android.os.Parcel.nativeAppendFrom(Native Method).
      ```
   * Исправлен возможный ANR в процессе:
      ```
      Metrica: at com.yandex.metrica.impl.ob.jg.a (jg.java) at com.yandex.metrica.MetricaService.onConfigurationChanged(MetricaService.java:2)
      ```
   * Исправлен возможный крэш:
      ```
      java.lang.NullPointerException: Attempt to read from null array at com.yandex.metrica.impl.ob.tz.a
      ```

#### Версия 4.1.1 {#s-4-1-1}

Релиз 17 декабря 2021 г.

* Добавлено разрешение [com.google.android.gms.permission.AD_ID](https://support.google.com/googleplay/android-developer/answer/6048248#zippy%3D%252Cpersistent-identifiers-including-android-id%252Ctargeting-devices-without-an-advertising-id%252Cadvertising-id-violations%252Chow-to-opt-out-of-personalized-ads). Подробности читайте в [документации](get-ad-id.md).
* В `DeferredDeeplinkListener.Error` и `DeferredDeeplinkParametersListener.Error` добавлено значение `NO_REFERRER`.
Добавлена предварительная поддержка [App Set ID](https://developer.android.com/training/articles/app-set-id) для получения реферрера из Google Play (зависимость `com.google.android.gms:play-services-appset:16.0.0`).
* Поддержана оптимизация SDK из-за исправления возможных [VerifyError](https://source.chromium.org/chromium/chromium/src/+/master:build/android/docs/class_verification_failures.md;bpv=1;bpt=0) при инициализации классов.
* Отключен сбор mac адресов.

#### Версия 4.0.0 {#s-4-0-0}

Релиз 20 сентября 2021 г.

* Google Play Install Referrer через BroadcastReceiver больше не поддерживается:
   * удален из AndroidManifest `MetricaEventHandler`;
   * удален метод `YandexMetrica#registerReferrerBroadcastReceivers`;
   * удален флаг `YandexMetricaConfig#installedAppCollecting`;
   * удалены методы `YandexMetricaConfig.Builder#withInstalledAppCollecting`.

* Добавлен метод `YandexMetricaConfig.Builder#withSessionsAutoTrackingEnabled(boolean enabled)` для автоматического отслеживания сессий.
* Добавлен метод `revenueAutoTrackingEnabled` для автоматического сбора данных по in-app покупкам.
* Поддержана публикация ".module" файла для [Google Play SDK Console](https://support.google.com/googlepl..-developer/answer/10358880?hl=ru).
* Реализован и включен по умолчанию автотрекинг диплинков.
* AppMetrica SDK [смигрирован на AndroidX](https://developer.android.com/jetpack/androidx/migrate).
* Добавлена базовая поддержка Android 12 — основной функционал AppMetrica SDK доступен на устройствах с Android 12 в приложениях с targetSdkVersion = 31.
* minSdkVersion повышен до 14.

{% endcut %}

## AppMetrica Gradle Plugin

### Версия 1.0.1 {#c-1-0-1}

Релиз 4 декабря 2024 г.

* Исправлено значение поля `version_name` в `info.txt` файле.

### Версия 1.0.0 {#c-1-0-0}

Релиз 27 ноября 2024 г.

* Поддержано подключение плагина с помощью `pluginManagement`. Плагин переименован в `io.appmetrica.analytics`.
* Все действия в плагине выполняются в отдельных gradle-тасках.
* Изменен список версий gradle и AGP, с которыми работает плагин.
* Поддержана работа при включенном configuration cache.
* Исправлена ошибка, из-за которой при определенных настройках  `R8` удалялись необходимые для работы ресурсы.

### Версия 0.11.0 {#c-0-11-0}

Релиз 2 мая 2024 г.

* Исправлена ошибка `Cannot write a file to a location pointing at a directory`.
* Удалено использование `Deprecated` класса `VersionNumber`.

### Версия 0.10.0 {#c-0-10-0}

Релиз 26 апреля 2024 г.

* Добавлен `keep` для ресурсов, добавляемых плагином для AGP `8.2.+`.

### Версия 0.9.0 {#c-0-9-0}

Релиз 26 февраля 2024 г.

* Добавлена поддержка AGP до версии `8.2.+` (кроме `8.0.+`) и gradle до `8.6`.

### Версия 0.8.2 {#c-0-8-2}

Релиз 31 октября 2023 г.

* Исправлен `StackOverflowError` при наличии циклических зависимостей.

### Версия 0.8.1 {#c-0-8-1}

Релиз 4 октября 2023 г.

* Исправлено возможное падение при проверке использования двух версий AppMetrica, если в проекте несколько модулей.

### Версия 0.8.0 {#c-0-8-0}

Релиз 14 сентября 2023 г.

* Изменено название плагина на `io.appmetrica.analytics:gradle:0.8.0`.
* Зависимость `com.yandex.android:mobmetricalib-ndk-crashes:1.1.0` обновлена до `io.appmetrica.analytics:analytics-ndk-crashes:3.0.0`.
* Добавлена поддержка работы с `io.appmetrica.analytics:analytics:6.0.0`.
* Добавлен параметр `allowTwoAppMetricas`, позволяющий убрать проверку на использование разных версий AppMetrica.

### Версия 0.7.0 {#c-0-7-0}

Релиз 19 апреля 2023 г.

* Дополнена ошибка об отсутствии mapping файлов.
* Добавлена поддержка AGP до версии `7.4.+` и gradle до `7.5`.

### Версия 0.6.2 {#c-0-6-2}

Релиз 28 июля 2022 г.

* Улучшена работа плагина.

### Версия 0.6.1 {#c-0-6-1}

Релиз 20 мая 2022 г.

* Улучшена работа плагина.

### Версия 0.6.0 {#c-0-6-0}

Релиз 17 мая 2022 г.

* Добавлен параметр mappingFile.
* Исправлена ошибка Cannot query the value of this property because it has no value available при получении mapping файла.

## AppMetrica Push SDK

### Версия 4.1.1 {#v-4-1-1}

Релиз 25 января 2025 г.

- Исправлена работа метода `PushServiceController.shouldSendToken`. Токен не отправляется, если `shouldSendToken == false` или `token == null`.
- Зависимость `androidx.legacy:legacy-support-v4` заменена на `androidx.core:core`.

### Версия 4.0.0 {#v-4-0-0}

Релиз 11 июля 2024 г.

- Текущая версия `minSdkVersion` повышена до `21` (Android 5.0).
- Конструктор `AppMetricaPushTracker` изменен с `AppMetricaPushTracker()` на `AppMetricaPushTracker(Context)`.
- Изменен интерфейс `PushServiceController`:
  - Метод `getTitle` переименован в `getTransportId`.
  - Добавлены методы `getExecutionRestrictions` и `shouldSendToken`.
- Улучшена доставка и скорость обработки push-нотификаций.

### Версия 3.3.0 {#v-3-3-0}

Релиз 3 мая 2024 г.

- Исправлена обработка пуша в `plugin-adapter`.

### Версия 3.2.0 {#v-3-2-0}

Релиз 22 апреля 2024 г.

- Обновлена поддерживаемая версия RuStore до `ru.rustore.sdk:pushclient:2.1.1`.
- Добавлен модуль `plugin-adapter` для корректной работы Push SDK при использовании в плагинах.
- Добавлено сохранение для названий переменных в публичном API.

### Версия 3.1.1 {#v-3-1-1}

Релиз 9 апреля 2024 г.

- Удалены отладочные логи.

### Версия 3.1.0 {#v-3-1-0}

Релиз 2 апреля 2024 г.

- Исправлена доставка silent-пушей при отключенных уведомлениях.

### Версии 3.0.0 — 2.0.0

{% cut "3.0.0 — 2.0.0" %}

#### Версия 3.0.0 {#v-3-0-0}

Релиз 18 ноября 2023 г.

- Обновлены идентификатор библиотеки, корневой пакет и API. Подробнее в [инструкции по миграции](push/migration-io-3-0-0.md).
- Добавлено API для кастомизации нотификации, создаваемой SDK.
- Удалена поддержка `com.yandex.android:mobmetricalib`.

#### Версия 2.3.3 {#v-2-3-3}

Релиз 10 ноября 2023 г.

- Исправлено падение при наличии двух версий AppMetrica SDK в приложении одновременно.

#### Версия 2.3.2 {#v-2-3-2}

Релиз 4 октября 2023 г.

- Исправлена ошибка

   ```
   No field Companion of type Lio/appmetrica/analytics/ModuleEvent$Companion
   ```

#### Версия 2.3.1 {#v-2-3-1}

Релиз 31 июля 2023 г.

- Повышены производительность и стабильность работы библиотеки.

#### Версия 2.2.0 {#v-2-2-0}

Релиз 2 июня 2022 г.

- `minSdkVersion` (в `appmetricapush-provider-hms`) увеличена до 17.
- Обновлена версия `hms` до 6.5.0.300.
- Ускорена активация PushSDK.

#### Версия 2.1.1 {#v-2-1-1}

Релиз 14 марта 2022 г.

- Исправлена ошибка `BadParcelableException: Parcelable protocol requires a Parcelable.Creator object called CREATOR`.

#### Версия 2.1.0 {#v-2-1-0}

Релиз 24 февраля 2022 г.

- Улучшено получение токенов.
- Метод YandexMetricaPush.getTokens возвращает новые токены при вызове из TokenUpdateListener.onTokenUpdated.
- Повышены производительность и стабильность работы библиотеки.

#### Версия 2.0.0 {#v-2-0-0}

Релиз 28 октября 2021 г.

- Исправлена ошибка, возникающая в некоторых случаях при обработке клика по пушу на Android 12.
- Переход с support-зависимостей на AndroidX.

{% endcut %}

