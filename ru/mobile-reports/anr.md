# ANR

ANR (Application Not Responding) — ситуация, при которой на главном потоке задача выполняется длительное время. В это время интерфейс приложения перестает обновляться и реагировать на действия пользователя. В итоге открывается диалоговое окно, предлагающее пользователю подождать или закрыть приложение.

С помощью отчета можно определить, в каких случаях ANR случается чаще всего. Используйте эти сведения для подготовки исправлений.

Можно сконфигурировать механизм сбора ANR и настроить тайм-ауты:

{% list tabs %}

- Android

  1. [Включите сбор ANR](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/javadoc/io/appmetrica/analytics/AppMetricaConfig.Builder.html#withAnrMonitoring(boolean)). По умолчанию сбор ANR выключен.

  1. [Задайте тайм-аут](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/javadoc/io/appmetrica/analytics/AppMetricaConfig.Builder.html#withAnrMonitoringTimeout(int)) — время, которое должен висеть поток, чтобы зафиксировался факт ANR. Значение по умолчанию — 5 секунд, минимальное значение — 5 секунд.

  {% list tabs group=instructions %}

    - Java

      ```java translate=no
      // Creating an extended library configuration.
      AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY)
              // Enabling ANR monitoring. Default value is false.
              .withAnrMonitoring(true)
              // Override ANR timeout if need. Default value is 5.
              .withAnrMonitoringTimeout(7)
              .build();
      // Initializing the AppMetrica SDK.
      AppMetrica.activate(getApplicationContext(), config);
      ```

    - Kotlin

      ```kotlin translate=no
      // Creating an extended library configuration.
      val config = AppMetricaConfig.newConfigBuilder(API_KEY)
          // Enabling ANR monitoring. Default value is false.
              .withAnrMonitoring(true)
              // Override ANR timeout if need. Default value is 5.
              .withAnrMonitoringTimeout(7)
          .build()
      // Initializing the AppMetrica SDK.
      AppMetrica.activate(applicationContext, config)
      ```

    {% endlist %}

- iOS

  {% list tabs group=instructions %}

  - Swift

    ```swift translate=no
    var configuration = AppMetricaCrashesConfiguration()

    // Enables detection of situations when the main application thread stops responding (ANR)
    configuration.applicationNotRespondingDetection = true 

    // Sets the time interval that the watchdog will wait before reporting the ANR status
    configuration.applicationNotRespondingWatchdogInterval = 4.0 

    // Sets the frequency with which the watchdog will check the ANR status
    configuration.applicationNotRespondingPingInterval = 0.1 

    AppMetricaCrashes.crashes().setConfiguration(configuration)
    ```

    или

    ```swift translate=no
    AppMetricaCrashes.crashes().enableANRMonitoring()
    ```

  - Objective-C  

    ```obj-c translate=no
    AMAAppMetricaCrashesConfiguration *configuration = [[AMAAppMetricaCrashesConfiguration alloc] init];

    // Enables detection of situations when the main application thread stops responding (ANR)
    configuration.applicationNotRespondingDetection = YES; 

    // Sets the time interval that the watchdog will wait before reporting the ANR status
    configuration.applicationNotRespondingWatchdogInterval = 4.0; 

    // Sets the frequency with which the watchdog will check the ANR status
    configuration.applicationNotRespondingPingInterval = 0.1; 

    [[AMAAppMetricaCrashes crashes] setConfiguration:configuration];
    ```
    
    или

    ```obj-c translate=no
    [[AMAAppMetricaCrashes crashes] enableANRMonitoring];
    ```
  {% endlist %}

{% endlist %}

## Период отчета {#period-anr}

Отчет можно просмотреть за конкретный день или период времени.

{% include [period](_includes/period.md) %}

## Группировка {#group-anr}

Данные для расчета группируются по:

- Группе ANR.
- Версии приложения.
- Устройству.
- Версии ОС.
- Производителю.

## Показатели {#measure}

![](../../_images/anr-info-{{locale}}.png)

Для анализа доступны следующие показатели:

- **ANRs** — количество ошибок.
- **Устройства** — количество устройств, на которых наблюдалась ошибка хотя бы один раз за выбранный период.
- **% от всех устройств** — доля устройств, с которых была отправлена ошибка, от общего числа устройств, запускавших приложение в выбранный период.
- **Обнаружен в версии** — версия приложения, в которой ошибка наблюдалась впервые.
- **Последнее воспроизведение** — версия приложения, в которой ошибка наблюдалась в последний раз.

Чтобы перейти на страницу с информацией о ANR-группе, в правом верхнем углу нажмите на название ANR-группы.

## Символизация ANR {#symbolization-anr}

{% note info %}

Нельзя пересобрать маппинги для предыдущих сборок. Но если есть архивы, сформированные нашим [крэш-плагином](../sdk/android/analytics/android-crash.md) для предыдущих сборок, то их можно загрузить вручную.

{% endnote %}

Если mapping или dSYM-файл не был загружен при сборке приложения, в списке групп будет отображаться предупреждение о несимволизированных ANR.

![](../../_images/symbolization-anr-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 330px;"}

Как символизировать ANR:

{% list tabs %}

  - Android

    ![](../../_images/mapping-upload-manual-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    Чтобы загрузить mapping-файлы:

      1. Откройте **Настройки** → **Крэши**.
      2. Убедитесь, что загрузка файлов выбрана для ОС Android.
      3. Выберите файл для загрузки.

    Список отсутствующих файлов можно посмотреть на странице **Настройки** → **Крэши** вашего приложения в AppMetrica.

  - iOS

    Загрузите [dSYM-файлы на iOS](../data-collection/upload-dsym.md). Список отсутствующих файлов можно посмотреть на странице **Настройки** → **Крэши** вашего приложения в AppMetrica.

{% endlist %}

## Просмотр лога ANR {#show-crash-log-anr}

Чтобы просмотреть лог:

1. На странице нажмите на название нужной ANR-группы.
2. В таблице нажмите кнопку **Посмотреть ANR-лог**.

В логе отображается информация об устройстве и ANR.

Чтобы посмотреть события, которые предшествовали ANR, из лога можно перейти в карточку профиля. Для этого нажмите кнопку **Посмотреть события сессии**.

## Добавление комментария {#comment-anr}

Вы можете оставить комментарий к ANR. Это может быть полезно, если отчет просматривают несколько человек. Например, в комментарии можно указать ссылку на задачу в трекере.

Чтобы добавить комментарий, откройте нужную группу и введите текст в поле **Комментарий**.

## Закрытие ANR {#close-anr}

Чтобы отфильтровать из отчета исправленные ANR, их можно закрывать. Если после закрытия ANR будет обнаружен в версиях, в которых он ранее не был обнаружен, ANR переоткроется.

Чтобы закрыть ANR, откройте нужную группу. В правом верхнем углу в блоке **Статус ANR-группы** установите режим **Закрыт**.

![](../../_images/anr-status-{{locale}}.png){style="border: solid 1px #cccccc; max-width: 200px;"}

## Экспорт данных {#export}

Описание ANR-лога можно выгрузить в TXT-файл. Для этого откройте нужную ANR-группу, нажмите кнопку **Посмотреть ANR-лог** → **Экспорт**.

## Узнать больше {#learn-more}

- [Отладка и исправление ANR на Unity-Android](https://developer.android.com/games/engines/unity/unity-anrs?hl=en)
- [Отладка и исправление ANR на Android](https://developer.android.com/topic/performance/anrs/diagnose-and-fix-anrs?hl=en)
- [Крэши/ошибки](../data-collection/about-crashes-and-errors.md)
- [Загрузка mapping-файлов и отладочных символов на Android](../data-collection/upload-mapping.md)
- [Загрузка dSYM-файлов на iOS](../data-collection/upload-dsym.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
