# Загрузка dSYM-файлов на iOS

Информация о крэшах на iOS отправляется в [десимволизированном](https://developer.apple.com/library/archive/technotes/tn2151/_index.html) виде. Из таких крэш‑логов сложно извлечь данные для анализа. Чтобы крэш-логи можно было анализировать, загрузите dSYM-файлы в AppMetrica.

Для загрузки dSYM-файлов в AppMetrica SDK включен инструмент командной строки [helper](#helper). Для сборки с помощью [fastlane](https://docs.fastlane.tools) поддержан [плагин загрузки](https://github.com/yandexmobile/metrica-plugin-fastlane). С их помощью можно настроить автоматическую загрузку dSYM-файлов при сборке приложения.

Пожалуйста, отправляйте dSYM файлы только для тех приложений, которые вы хотите опубликовать.

## Автоматическая загрузка при сборке {#auto}

Используйте [fastlane](https://docs.fastlane.tools) для сборки приложения:

1. Установите fastlane-плагин `appmetrica`:

    ```bash translate=no
    fastlane add_plugin appmetrica
    ```
    
    Подробнее о добавлении плагина в [документации fastlane](https://docs.fastlane.tools/plugins/using-plugins/#add-a-plugin-to-your-project).
    
2. Добавьте в файл `fastlane/Fastfile` следующее:

    ```bash translate=no
    lane :release do
    # Your actions before.
    gym(
    workspace: "MyApp.xcworkspace",
    configuration: "Release",
    scheme: "MyApp",
    export_method: "app-store"        # Pass the correct export_method.
    )
    upload_symbols_to_appmetrica(post_api_key: "Post API key")
    # Your actions after.
    end
    ```
    
    Post API key можно получить в разделе **Настройки** в AppMetrica. Он используется для идентификации вашего приложения.
    
    {% note alert "" %}
    
    Для сборки приложения используется action [gym](https://docs.fastlane.tools/actions/gym/#gym) с экспортом. Если вы собираете приложение с помощью Xcode, приложение будет перекомпилировано после загрузки в App Store Connect. Тогда сгенерированые при сборке dSYM-файлы нельзя будет использовать.
    
    {% endnote %}

3. Добавьте этап загрузки dSYM-файлов с помощью инструмента `helper` в Xcode. Инструмент `helper` включен в AppMetrica SDK, начиная с версии 3.8.0. Он находится в архиве SDK. [Справочник инструмента helper](#helper).

   1. Откройте проект в Xcode.
   2. В навигаторе по проекту выберите файл проекта.
   3. В блоке **Targets** выберите ваше приложение.
   4. Откройте вкладку **Build Phases**.
   5. Нажмите кнопку **+**&nbsp;→ **New Run Script Phase**.
   6. В текстовое поле **Type a script** добавьте:

       ```bash translate=no
       if [ -d "${PODS_ROOT}/AppMetricaCrashes" ]; then
       HELPER_PATH=`find "${PODS_ROOT}/AppMetricaCrashes" -name "helper"`
       if [ -x  "${HELPER_PATH}" ]; then
       "${HELPER_PATH}" auto --post-api-key="Post API key"&
       else
       echo "AppMetricaСrash helper was not found"
       fi
       fi
       ```

       {% note info "" %}

       Режим `auto` использует переменную окружения `CONFIGURATION`. Если сборка собирается с конфигурацией `Debug`, dSYM-файлы не загружаются.

       {% endnote %}

## Загрузка отсутствующего dSYM-файла {#after-upload}

Если при сборке приложения dSYM-файл не был загружен, в отчетах по крэшам будет отображаться предупреждение о несимволизированных крэшах.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/dsym-warning.png){style="border: solid 1px #cccccc; max-width: 800px;"}

Чтобы их символизировать, загрузите отсутствующие dSYM-файлы. Список отсутствующих файлов можно посмотреть на странице **Настройки** → **Крэши** вашего приложения в AppMetrica.

Отсутствующие dSYM-файлы можно загрузить:

{% list tabs %}

- С помощью fastlane

  1. Установите fastlane-плагин `appmetrica`:

      ```bash translate=no
      fastlane add_plugin appmetrica
      ```

      Подробнее о добавлении плагина в [документации fastlane](https://docs.fastlane.tools/plugins/using-plugins/#add-a-plugin-to-your-project).

  2. Добавьте в файл `fastlane/Fastfile` следующее:

      ```bash translate=no
      lane :refresh_dsyms do
      download_dsyms
      upload_symbols_to_appmetrica(post_api_key: "Post API key")
      clean_build_artifacts
      end
      ```

      В действии `download_dsyms` можно указать необходимую версию приложения и номер сборки:
      ```bash translate=no
      ...
      download_dsyms(version: "1.0.0", build_number: "345")
      ...
      ```

      Подробнее о действии `download_dsyms` в документации [fastlane](https://docs.fastlane.tools/actions/download_dsyms/).

- Через веб-интерфейс

  1. Найдите необходимый архив с dSYM-файлом:

      {% cut "Через Xcode Organizer" %}

      1. В интерфейсе Xcode нажмите **Window** → **Organizer**.
      2. Во вкладке **Archives** выберите нужную версию приложения.
      3. Нажмите кнопку **Download dSYM**.

         <img src="https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/xcode-archives_organizer.png">

      {% endcut %}

      {% cut "Через App Store Connect" %}

      1. В интерфейсе iTunes Connect откройте страницу **Activity**.
      2. Во вкладке **All Builds** выберите нужный номер сборки.
      3. Нажмите **Download dSYM**.

         <img src="https://yastatic.net/s3/doc-binary/src/dev/appmetrica/ru/images/common/itunes-connect.png">

      {% endcut %}

      Можно использовать dSYM-файл, который был сгенерирован при сборке.

  1. В интерфейсе AppMetrica перейдите в настройки приложения из меню слева.
  2. Откройте вкладку **Крэши** → **iOS**.
  3. Нажмите кнопку **Выберите файл** и загрузите ZIP-архив, содержащий директории `app.dSYM` или `app`.
  
- С помощью helper

  Для загрузки с помощью плагина необходимо подключить AppMetrica SDK не нижее версии 3.8.0.
  Чтобы загрузить в AppMetrica отсутствующие dSYM-файлы, в терминале выполните команду:
  
  ```bash translate=no
  helper -k <post-api-key> <file_path>
  ```

  `file_path` — список dSYM-файлов или папок, в которых они лежат.

  [Справочник инструмента helper](#helper).

{% endlist %}

## Справочник инструмента helper {#helper}

{% note info "" %}

Инструмент `helper` включен в AppMetrica SDK, начиная с версии 3.8.0. Он находится в архиве SDK.

{% endnote %}

Helper — инструмент командной строки, который позволяет загружать dSYM-файлы в AppMetrica.

```bash translate=no
$ helper [auto] [-o | --package-output-path=<path>] [-v | --verbose]
         [--version] -k <post-api-key> | --post-api-key=<key> [file ...]
```

**Параметры**

#|
|| `auto` | Автоматический режим загрузки. В нем `helper` использует следующие переменные:
- `CONFIGURATION` — используется для определения конфигурации. Если сборка собирается с конфигурацией `Debug`, dSYM-файлы не загружаются.
- `DWARF_DSYM_FOLDER_PATH` — используется для нахождения dSYM-файлов. Она обычно зависит от переменной `BUILT_PRODUCTS_DIR`.
- `AMA_POST_API_KEY` — [Post API key](*Post API key). Если указан, в автоматическом режиме можно использовать короткую команду `helper auto&`. ||
|| `‑k` | Post API key. Его можно получить в разделе **Настройки** в AppMetrica. Он используется для идентификации вашего приложения. ||
|| `‑o` | Путь к папке, в которой хранятся временные файлы.

По умолчанию используется системная папка. ||
|| `‑v` | Включает отображение дополнительной информации. ||
|| `‑‑version` | Выводит версию. ||
|| `file` | Список dSYM-файлов или папок, в которых они лежат.

По умолчанию используется локальная рабочая папка.||
|#

`&` позволяет запускать `helper` параллельно, не блокируя сборку всего проекта. Пример команды:
```
helper auto --post-api-key="Post API key"&
```

## Узнать больше {#learn-more}

- [Отчет Крэши и ошибки](../mobile-reports/crashes-and-errors.md)
- [Документация Apple](https://developer.apple.com/library/archive/technotes/tn2151/_index.html)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*Post API key]: Post API key можно получить в разделе **Настройки** в AppMetrica. Он используется для идентификации вашего приложения.
