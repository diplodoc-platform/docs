# Подключение и инициализация

Чтобы интегрировать AppMetrica в приложение Flutter, используйте плагин [AppMetrica SDK for Flutter](https://pub.dev/packages/appmetrica_plugin):

## Шаг 1. Установите плагин AppMetrica SDK for Flutter в свой проект {#integration}

Из корня проекта вызовите команду:
    
```bash translate=no
flutter pub add appmetrica_plugin
```

После добавления плагина в файле `pubspec.yaml` появится строка с зависимостью:

```yaml translate=no
dependencies:
    appmetrica_plugin: ^{{ appmetrica-flutter-plugin }}
```
## Шаг 2. Инициализируйте библиотеку {#initialization}   

1. Добавьте импорт `appmetrica_plugin`:
    ```java translate=no
    import 'package:appmetrica_plugin/appmetrica_plugin.dart';
    ```

2. Инициализируйте библиотеку с помощью `AppMetrica.activate` и вашего API key:
    
    ```bash translate=no
    AppMetrica.activate(AppMetricaConfig("insert_your_api_key_here"));
    ```
    
3. Отправьте событие с помощью `AppMetrica.reportEvent`, чтобы протестировать работу:
    
    ```bash translate=no
    AppMetrica.reportEvent('My first AppMetrica event!');
    ```

## Узнайте больше {#learn-more}

- [Настройка отправки событий Ecommerce](flutter-operations.md#send-ecommerce)
- [Настройка отправки событий Revenue](flutter-operations.md#send-revenue)
- [Настройка отправки событий Ad Revenue](flutter-operations.md#send-adrevenue)    

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
