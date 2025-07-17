# AppMetrica Gradle Plugin

AppMetrica позволяет собирать информацию о нативных и java-крэшах. Их можно анализировать в отчете [Крэши](../../../mobile-reports/crashes-and-errors.md). См. также раздел [Крэши/ошибки](../../../data-collection/about-crashes-and-errors.md).

Чтобы уменьшить размер приложения, код [оптимизируют](https://developer.android.com/studio/build/shrink-code) во время релизной сборки.

Если во время сборки Android-приложения сжимали и обфусцировали код, то информация о крэшах передается в обфусцированном виде. Чтобы извлечь данные для анализа из таких крэш-логов, AppMetrica выполняет деобфускацию на стороне сервера.

Для этого загрузите mapping-файлы или отладочные символы SO-файлов в AppMetrica: автоматически при сборке приложения или вручную через веб-интерфейс.

Чтобы отправлять файлы, подключите AppMetrica Gradle Plugin.

## Ограничения {#restrictions}

- Загружайте mapping-файлы, если вы используете [ProGuard](https://www.guardsquare.com/en/products/proguard/manual) или [R8](https://r8.googlesource.com/r8/). Если вы не сжимаете и не обфусцируете код, не подключайте плагин.

- Работа плагина зависит от версий `com.android.tools.build:gradle` (AGP) и gradle. Поддерживается работа плагина со следующими версиями:

    - `com.android.tools.build:gradle` с `7.2.0` до `8.8.0` (кроме `8.0.*`);
    - gradle с `7.4` до `8.12`. Работа плагина с другими версиями не гарантируется.

    Работа плагина при использовании gradle `8.0` и AGP `7.4.*` вместе не гарантируется.

- Плагин не поддерживает [Configuration Cache](https://docs.gradle.org/current/userguide/configuration_cache.html) в Gradle. Все задачи плагина помечены как несовместимые с этой функцией, и при их использовании вы увидите предупреждение от Gradle.

- Для локальных сборок рекомендуется отключать плагин. Это позволит ускорить сборку проекта. Плагин необходимо включать только для сборок на CI.

## Подключение плагина {#connecting}

Чтобы подключить плагин: 

1. Добавьте в корневой Gradle файл зависимость:

   {% list tabs %}

   - build.gradle.kts

     ```kotlin translate=no
     plugins {
         id("io.appmetrica.analytics") version "{{ io-appmetrica-analytics-gradle }}" apply false
     }
     ```

   - build.gradle

     ```groovy translate=no
     plugins {
         id "io.appmetrica.analytics" version "{{ io-appmetrica-analytics-gradle }}" apply false
     }
     ```

   {% endlist %}

   {% cut "Подключение с использованием `buildscript`" %}

   Добавьте в корневой Gradle файл зависимость:

   {% list tabs %}

    - build.gradle.kts

      ```kotlin translate=no
      buildscript {
         repositories {
             mavenCentral()
         }
         dependencies {
             classpath("io.appmetrica.analytics:gradle:{{ io-appmetrica-analytics-gradle }}")
         }
      }
      ```

    - build.gradle

      ```groovy translate=no
      buildscript {
         repositories {
             mavenCentral()
         }
         dependencies {
             classpath 'io.appmetrica.analytics:gradle:{{ io-appmetrica-analytics-gradle }}'
         }
      }
      ```

   {% endlist %}

   {% endcut %}

2. Добавьте в Gradle файл приложения подключение плагина и его настройку:

   {% list tabs %}

   - build.gradle.kts

     ```kotlin translate=no
     plugins {
         id("com.android.application")
         id("io.appmetrica.analytics")
     }

     appmetrica {
         postApiKey = { applicationVariant -> "Post Api key for variant" }
         // or setPostApiKey("Post Api key")
         enable = { applicationVariant -> true }                           // Optional
         offline = { applicationVariant -> false }                         // Optional
         mappingFile = { applicationVariant -> null }                      // Optional
         enableAnalytics = true                                            // Optional
         allowTwoAppMetricas = { applicationVariant -> false }             // Optional
         ndk {                                                             // Optional
             enable = { applicationVariant -> false }
             soFiles = { applicationVariant -> listOfSoFiles }             // Optional
             additionalSoFiles = { applicationVariant -> listOfSoFiles }   // Optional
             addNdkCrashesDependency = { applicationVariant -> true }      // Optional
         }
     }
     ```

   - build.gradle

     ```groovy translate=no
     plugins {
         id 'com.android.application'
         id 'io.appmetrica.analytics'
     }

     appmetrica {
         postApiKey = { applicationVariant -> "Post Api key for variant" }
         // or postApiKey = "Post Api key"
         enable = { applicationVariant -> true }                           // Optional
         offline = { applicationVariant -> false }                         // Optional
         mappingFile = { applicationVariant -> null }                      // Optional
         enableAnalytics = true                                            // Optional
         allowTwoAppMetricas = { applicationVariant -> false }             // Optional
         ndk {                                                             // Optional
             enable = { applicationVariant -> false }
             soFiles = { applicationVariant -> listOfSoFiles }             // Optional
             additionalSoFiles = { applicationVariant -> listOfSoFiles }   // Optional
             addNdkCrashesDependency = { applicationVariant -> true }      // Optional
         }
     }
     ```

   {% endlist %}

   #|
   || **Параметр** | **Описание** ||
   || `postApiKey*` | Post API key или лямбда-функция, которая возвращает Post API key для `ApplicationVariant`. Подробнее про `ApplicationVariant` в документации [Android](https://developer.android.com/studio/build/build-variants) и [Javadoc](https://www.javadoc.io/doc/com.android.tools.build/gradle/0.7.2/com/android/build/gradle/api/ApplicationVariant.html).
   Post API key можно получить в разделе Настройки в AppMetrica. Он используется для идентификации вашего приложения.

   Если `offline = true`, то параметр не является обязательным. ||
   || `enable` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает, надо ли использовать плагин для этого варианта сборки.
   Если плагин не используется, apk не меняется и mapping-файл не загружается.

   По умолчанию возвращает `true` только для `buildType = 'release'`.

   {% note info %}

   Для указания типов сборок используйте один из параметров: `enable` или `mappingBuildTypes`.

   {% endnote %}
   ||
   || `mappingBuildTypes` | Список типов сборок `buildType`, для которых будет отправляться mapping-файл.
   Значение по умолчанию: `['release']`.

   Чтобы отключить загрузку mapping-файлов для определенного типа сборки, удалите из списка нужный `buildType`.

   {% note info %}

   Для указания типов сборок используйте один из параметров: `enable` или `mappingBuildTypes`.

   {% endnote %}
   ||
   || `offline` | Включает режим `offline`. Boolean или лямбда-функция, которая принимает `ApplicationVariant`.

   Допустимые значения:

   * `true` — не загружает файл в AppMetrica. Если включен, после сборки выводит путь до архива в лог. Его можно загрузить вручную через веб-интерфейс.
   * `false` — автоматически загружает mapping-файл.
   Значение по умолчанию: `false`. ||
   || `mappingFile` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает mapping, который надо загрузить. Если лямбда возвращает `null`, используется значение по умолчанию.

   Значение по умолчанию: `ApplicationVariant.mappingFileProvider`. ||
   || `enableAnalytics` | Включает отправку статистики об использовании плагина в AppMetrica. `Boolean`.

   Допустимые значения:

   * `true` — отправка статистики включена.
   * `false` — отправка статистики выключена.
   Значение по умолчанию: `true`. ||
   || `allowTwoAppMetricas` | Лямбда-функция, которая принимает `ApplicationVariant` и проверяет использование двух библиотек AppMetrica одновременно.

   Допустимые значения:

   * `false` — плагин проверяет, что в проекте используется только одна версия библиотеки `io.appmetrica.analytics:analytics` или `com.yandex.android:mobmetricalib`. Если это не так, выбрасывается исключение.
   * `true` — плагин проверяет использование двух библиотек AppMetrica одновременно, результат проверки пишется в лог.

   Значение по умолчанию: `false`. ||
   || `ndk` | Параметр необходим для загрузки символов из SO-файла, чтобы отслеживать нативные крэши. ||
   || `ndk.enable` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает, надо ли загружать символы из SO-файлов для этого варианта сборки.

   Значение по умолчанию: `false`. ||
   || `ndk.soFiles` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает список SO-файлов.

   По умолчанию плагин ищет SO-файлы в папках проекта Android Studio.

   Необходимо переопределить, если ваши SO-файлы лежат в необычном месте или если плагин не может их найти. ||
   || `ndk.additionalSoFiles` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает список дополнительных SO-файлов, символы которых необходимо загрузить. ||
   || `ndk.addNdkCrashesDependency` | Лямбда-функция, которая принимает `ApplicationVariant` и возвращает, надо ли добавлять зависимость от `io.appmetrica.analytics:analytics-ndk-crashes`.

   Значение по умолчанию: `true`. ||
   |#

3. Если параметр `ndk` включен, то для отправки отладочных символов используется задача Gradle `upload${variant.name.capitalize()}AppMetricaNdkSymbols`. Чтобы вызывать задачу автоматически, можно добавить в файл `app/build.gradle` следующий код:

   {% list tabs %}

   - build.gradle.kts

     ```kotlin translate=no
     android.applicationVariants.configureEach {
         val variant = this
         val uploadSymbolsTask = project.tasks.findByName("upload${variant.name.capitalize()}AppMetricaNdkSymbols")
         if (uploadSymbolsTask != null) {
             variant.assembleProvider.configure { it.finalizedBy(uploadSymbolsTask) }                     // Если используете apk
             project.tasks.named("bundle${variant.name.capitalize()}") { finalizedBy(uploadSymbolsTask) } // Если используете aab
         }
     }
     ```

   - build.gradle

     ```groovy translate=no
     android.applicationVariants.configureEach { variant ->
         def uploadSymbolsTask = project.tasks.findByName("upload${variant.name.capitalize()}AppMetricaNdkSymbols")
         if (uploadSymbolsTask != null) {
             variant.assembleProvider.configure { it.finalizedBy(uploadSymbolsTask) }                     // Если используете apk
             project.tasks.named("bundle${variant.name.capitalize()}") { finalizedBy(uploadSymbolsTask) } // Если используете aab
         }
     }
     ```

   {% endlist %}

## Ручная загрузка {#manual-loading}

Для ручной загрузки нужно подключить и использовать плагин с режимом `offline`. Это необходимо для связывания mapping-файла со сборкой приложения.

1. В файле app/build.gradle включите режим `offline` и запустите сборку.

   {% list tabs %}

   - build.gradle.kts

     ```kotlin translate=no
     appmetrica {
         offline = { true }
     }
     ```

   - build.gradle

     ```groovy translate=no
     appmetrica {
         offline = { true }
     }
     ```

   {% endlist %}

2. В интерфейсе AppMetrica перейдите в настройки приложения из меню слева.
3. Откройте вкладку **Крэши** → **Android**.
4. Нажмите кнопку **Выберите файл** и загрузите Zip-архив.

## Описание генерируемых файлов {#generated-files} 

Плагин для работы генерирует файлы в папке `app/build/appmetrica`.
Структура папок приведена ниже

```
app/build/appmetrica
└── release - название AndroidApplicationVariant
    ├── info.txt - файл с метаинформацией для поиска файла маппинга и символов
    ├── res - папка с ресурсами, которые будут использованы для сборки приложения
    │   ├── raw
    │   │   └── keep_appmetrica_resources.xml - правила для R8 по сохранению ресурсов
    │   └── values
    │       └── appmetrica_resources.xml - необходимые для работы ресурсы
    ├── result - папка с архивами, которые нужно самостоятельно загружать в режиме offline
    │   ├── mapping.zip - финальный архив с маппингами
    │   └── symbols.zip - финальный архив с символами
    └── symbols - папка с символами, которые получились из so файлов
        ├── libmyapplication_0E6CC10E8293F1B2DF0293FBE44887AD0.ysym
        ├── libmyapplication_3CDE92724603DA3A59BC6E311625A4000.ysym
        ├── libmyapplication_6F5C61C0E96CAEFD1E7ED491F806DA100.ysym
        └── libmyapplication_F3E083A014DD2840F0E730B6BB138E4A0.ysym
```

## Ошибки при сборке {#errors}

Возможные ошибки при сборке:

- `IllegalStateException` — включите обфускацию кода с помощью ProGuard или R8 Compiler;
- `HttpResponseException` — проверьте подключение к интернету.

При возникновении других ошибок обращайтесь в [техническую поддержку](../../../troubleshooting/feedback-new.md).

## Узнайте больше {#learn-more}

- [Отчет Крэши и ошибки](../../../mobile-reports/crashes-and-errors.md)
- [Документация Android](https://developer.android.com/topic/performance/vitals/crash)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
