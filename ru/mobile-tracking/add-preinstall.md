# Создание трекера для предустановок

Предустановки — установки приложения, которые происходят без непосредственного участия пользователей устройств. AppMetrica поддерживает несколько способов трекинга предустановленных приложений.

## Создание трекера для предустановок от производителя устройств {#apk}

{% note alert %}

Для получения корректной статистики по активациям предустановленного приложения нельзя использовать tracking URL из созданного трекера. Для каждого партнера необходимо создать отдельный трекер.

{% endnote %}

### Шаг 1. Создание трекера в интерфейсе AppMetrica {#apk-web}

1. В интерфейсе AppMetrica перейдите в раздел **Трекинг** → **Создать трекер**.

2. В блоке **Описание кампании** заполните поля:

   - **Предустановка** — включите опцию для трекинга предустановок.
   - **PAI** — оставьте опцию выключенной. Подробнее о [создании трекера для PAI предустановок](#pai).
   - **Название** — имя трекера. После создания трекер будет доступен в списке трекеров с указанным названием.
   - **Приложение** — выберите приложение, для которого создается трекер.
   - **Партнёр** — рекламный партнер, которому будут отнесены клики, установки и целевые события.
      Если в списке нет нужного партнера, [добавьте его](add-partner.md). После добавления новый партнер будет доступен в списке.

### Шаг 2. Получение tracking_ID {#tracking-id}

1. [Найдите созданный трекер в списке](https://appmetrika.yandex.{{ domain }}/campaign/list) и перейдите на его страницу. ID, который указан на странице, используется в качестве tracking_ID при [настройке AppMetrica SDK](#apk-sdk-setting).

![](../../_images/tracking-id-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

### Шаг 3. Настройка AppMetrica SDK {#apk-sdk-setting}

{% list tabs %}

- Android

  Отслеживание предустановленных приложений доступно при использовании [расширенной конфигурации библиотеки AppMetrica](../sdk/android/analytics/android-operations.md). Чтобы задать параметры для отслеживания предустановленных приложений выполните следующее:
  
  1. Создайте объект с параметрами, необходимыми для отслеживания:

      ```java translate=no
      public class MyApp extends Application {
            @Override
            public void onCreate() {
                super.onCreate();
                // Creating an instance of a constructor for app pre-installation information.
                PreloadInfo.Builder preloadInfoBuilder = PreloadInfo.newBuilder(tracking_ID);
                // Creating an instance of information about app pre-installation.
                PreloadInfo preloadInfo = preloadInfoBuilder.build();
      ```

  2. Создайте расширенную конфигурацию библиотеки AppMetrica и укажите параметры для отслеживания предустановленных приложений. Затем произведите инициализацию библиотеки в приложении, используя расширенную конфигурацию.

      ```java translate=no
      public class MyApp extends Application {
            @Override
            public void onCreate() {
                super.onCreate();
                // Creating an extended library configuration.
                AppMetricaConfig.Builder configBuilder = AppMetricaConfig.newConfigBuilder(API_key);
                // Setting necessary parameters (for example, enabling logging).
                configBuilder.setLogEnabled();
                // ...
                // Setting tracking parameters for pre-installed apps.
                configBuilder.setPreloadInfo(preloadInfo);
                // Creating an extended configuration instance.
                AppMetricaConfig extendedConfig = configBuilder.build();
                // Initializing the AppMetrica SDK.
                AppMetrica.activate(getApplicationContext(), extendedConfig);
            }
      }
      ```

      Инициализируйте AppMetrica SDK данным образом для всех процессов приложения.

  3. Включите отслеживание активности пользователей, используя метод класса `AppMetrica`:

      ```java translate=no
      ...
      AppMetrica.enableActivityAutoTracking(this);
      ```

- iOS

  Отслеживание предустановленных приложений доступно при использовании [расширенной конфигурации библиотеки AppMetrica](../sdk/ios/analytics/ios-operations.md).Чтобы задать сведения для отслеживания предустановленных приложений выполните следующее:
  
  - Objective-C
  
    1. Создайте объект с параметрами, необходимыми для отслеживания:

        ```objectivec translate=no
        AMAAppMetricaPreloadInfo *preloadInfo = [[AMAAppMetricaPreloadInfo alloc] initWithTrackingIdentifier:@"tracking_ID"];
        ```

    2. Создайте расширенную конфигурацию библиотеки AppMetrica и задайте в ней информацию для отслеживания предустановленных приложений. Затем произведите инициализацию библиотеки в приложении, используя расширенную конфигурацию.

        ```objectivec translate=no
        // Creating an extended library configuration.
        AMAAppMetricaConfiguration *configuration = [[AMAAppMetricaConfiguration alloc] initWithApiKey:@"API_key"];
        // Setting up the configuration.
        configuration.preloadInfo = preloadInfo;
        // ...
        // Initializing the AppMetrica SDK.
        [AMAAppMetrica activateWithConfiguration:configuration];
        
        ```

  - Swift
  
    1. Создайте объект с параметрами, необходимыми для отслеживания:

        ```swift translate=no
        let preloadInfo = AppMetricaPreloadInfo.init(trackingIdentifier: "tracking_ID")
        ```

    2. Создайте расширенную конфигурацию библиотеки AppMetrica и задайте в ней информацию для отслеживания предустановленных приложений. Затем произведите инициализацию библиотеки в приложении, используя расширенную конфигурацию.

        ```swift translate=no
        // Creating an extended library configuration.
        let configuration = AppMetricaConfiguration.init(apiKey: "API key")
        // Setting up the configuration
        configuration?.preloadInfo = preloadInfo
        // ...
        // Initializing the AppMetrica SDK.
        AppMetrica.activate(with: configuration!)
        ```

{% endlist %}

| Параметр | Описание |
| -------- | -------- |
| `API_key` | Уникальный идентификатор приложения, который выдается в веб-интерфейсе AppMetrica при [добавлении приложения](https://appmetrika.yandex.{{ domain }}/application/new) |
| `tracking_ID` | Числовой идентификатор трекера, который указывается в интерфейсе AppMetrica при создании трекера. |

## Создание трекера для PAI предустановок {#pai}

1. В интерфейсе AppMetrica перейдите в раздел **Трекинг** → **Создать трекер**.

2. В блоке **Описание кампании** заполните поля:

   - **Предустановка** — включите опцию для трекинга предустановок.
   - **PAI** — включите опцию, если вы создаете трекер для PAI предустановок. Подробнее о [PAI предустановках](preinstalled-app-attr.md#pai).
   - **Название** — имя трекера. После создания трекер будет доступен в списке трекеров с указанным названием.
   - **Приложение** — выберите приложение, для которого создается трекер.
   - **Партнёр** — рекламный партнер, которому будут отнесены клики, установки и целевые события.
      Если в списке нет нужного партнера, [добавьте его](add-partner.md). После добавления новый партнер будет доступен в списке.

3. В блоке ниже заполните поле **utm_campaign**. Параметр используется для подсчета предустановок с типом PAI. Введите значение, полученное от производителя, либо сгенерируйте значение параметра и передайте его производителю.

## См. также

- [Трекинг предустановленных приложений](preinstalled-app-attr.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
