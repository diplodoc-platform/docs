# Интеграция SDK

SDK под Android предоставляется в виде библиотеки в формате AAR. Библиотека доступна в [Maven-репозитории](https://mvnrepository.com/artifact/io.appmetrica.analytics/analytics).

Ниже описаны этапы подключения и инициализации AppMetrica SDK:

## Шаг 1. Добавьте библиотеку в проект {#integration}

Если вы используете Gradle для сборки приложения, добавьте следующую зависимость в Gradle файл приложения:

{% list tabs %}

- build.gradle.kts

  ```kotlin translate=no
  dependencies {
      // AppMetrica SDK.
      implementation("io.appmetrica.analytics:analytics:{{ io-appmetrica-analytics-analytics }}")
  }
  ```

- build.gradle

  ```groovy translate=no
  dependencies {
      // AppMetrica SDK.
      implementation 'io.appmetrica.analytics:analytics:{{ io-appmetrica-analytics-analytics }}'
  }
  ```

{% endlist %}

## Шаг 2. Инициализируйте библиотеку {#initialization}

{% note alert "" %}

В библиотеке AppMetrica есть особенности, которые необходимо учитывать при инициализации. Подробнее в разделе [Особенности библиотеки AppMetrica](android-features.md).

{% endnote %}

Инициализируйте библиотеку в приложении. Для этого объявите производный класс от базового класса `Application` и переопределите метод `onCreate()` следующим образом:

{% list tabs group=instructions %}

- Kotlin

  ```kotlin translate=no
  class YourApplication : Application() {
      override fun onCreate() {
          super.onCreate()
          // Creating an extended library configuration.
          val config = AppMetricaConfig.newConfigBuilder(API_KEY).build()
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(this, config)
      }
  }
  ```

- Java

  ```java translate=no
  public class YourApplication extends Application {
      @Override
      public void onCreate() {
          super.onCreate();
          // Creating an extended library configuration.
          AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY).build();
          // Initializing the AppMetrica SDK.
          AppMetrica.activate(this, config);
      }
  }
  ```

{% endlist %}

{% cut "Что такое API key?" %}

{{ api-key }}

{% endcut %}

При инициализации библиотеки с расширенной стартовой конфигурацией включается [логирование](android-logs.md).

## Шаг 3. (Опционально) Настройте определение местоположения {#location}

Определение местоположения позволяет оценить географическое распределение пользователей. По умолчанию отправка местоположения устройства отключена, но ее можно включить при инициализации конфигурации. Подробнее см. раздел [{#T}](android-operations.md#track-location).

## Шаг 4. (Опционально) Настройте отправку событий, атрибутов профиля и Revenue (#send)

Чтобы собирать информацию о действиях в приложении, настройте отправку собственных событий. Подробнее в разделе [Отправка собственных событий](../../../data-collection/about-events.md).

Чтобы собирать информацию о пользователях, настройте отправку атрибутов профиля. Подробнее в разделе [Профили](../../../data-collection/about-profiles.md).

{% note info "" %}

В отличие от событий, атрибут профиля может принимать только одно значение. При отправке нового значения атрибута старое значение перезаписывается.

{% endnote %}

Чтобы отслеживать покупки в приложении, настройте отправку Revenue. Подробнее в разделе [In-App покупки](../../../data-collection/about-revenue.md).

## Шаг 5. Протестируйте работу библиотеки {#test}

{% note alert "" %}

Перед проверкой работы библиотеки убедитесь, что SDK инициализирована с соблюдением [рекомендаций](android-features.md#recommendations).

{% endnote %}

Перед началом тестирования желательно настроить [передачу данных на дополнительный API key](android-operations#reporter-different-apikey) или [добавить приложение с новым API key](https://appmetrica.yandex.{{ domain }}/about). Это поможет отделить тестовые данные от основной статистики.

Чтобы проверить работу библиотеки:

1. Запустите приложение с AppMetrica SDK и используйте его некоторое время.
2. Убедитесь, что устройство подключено к интернету.
3. В интерфейсе AppMetrica убедитесь, что:
   - В отчете [Аудитория](../../../mobile-reports/audience-report.md) появился новый пользователь.
   - В отчете **Вовлечённость** → **Сессии** увеличилось число сессий.
   - В отчете [События](../../../mobile-reports/events-report.md) и [Профили](../../../mobile-reports/profile-report.md) появились отправленные события и атрибуты профиля.

## Узнайте больше {#learn-more}

- [Настройка отправки собственных событий](android-operations.md#report-event)
- [Настройка отправки атрибутов профиля](android-operations.md#send-attribute-profile)
- [Настройка отправки событий Ecommerce](android-operations.md#send-ecommerce)
- [Настройка отправки событий Revenue](android-operations.md#send-revenue)
- [Настройка отправки событий Ad Revenue](android-operations.md#send-adrevenue)
- [Как включить отправку данных о местоположении пользователей?](../../../troubleshooting/troubleshooting.md#region)
- [Как проверить, что у меня установлены последние версии Android-библиотек?](../../../troubleshooting/troubleshooting.md#newest-android-version)

<!-- - [Пример интеграции библиотеки ССЫЛКА НУЖНА НОВАЯ](https://github.com/yandexmobile/metrica-sample-android)-->

## Возможные проблемы и их решение {#faq}

- [Не увеличивается число сессий](android-errors.md#session)
- [Нет событий](android-errors.md#events)
- [Ошибка при добавлении библиотеки в проект](android-errors.md#add-in-project)
- [Некорректная длительность пользовательской сессии при ручном отслеживании](android-errors.md#listen-root)
- [Высокое энергопотребление библиотекой AppMetrica](android-errors.md#power)
- [Конфликт при использовании автосбора Ad Revenue для Fyber](android-errors.md#fyber-unsupport-adrevenue)
- [В списке нет моей проблемы](android-errors.md#not-found)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
