# Руководство по миграции на версию 2.0.0

## Одновременное использование двух версий AppMetrica Push SDK {#two-versions}

В одном приложении могут использоваться сразу две версии AppMetrica Push SDK.

{% note alert %}

Это делать не рекомендуется, так как может приводить к аномалиям в отчетах. То есть нельзя одновременно активировать `AppMetricaPush` и использовать префаб `AppMetricaPush` из старой версии. Это не приведет к сбоям и крэшам в приложении, но вызовет искажение и нарушение статистики. При миграции на новую версию плагина проверьте, что у вас нет папки `Assets/AppMetricaPush`, новая версия плагина поставляется через UPM и будет располагаться в `Library/PackageCache/io.appmetrica.analytics.push@hash`.

{% endnote %}

## Руководство по миграции {#about-migration}

Руководство содержит примеры, демонстрирующие различия между версиями плагина `1.1.0` и `2.0.0`. В разделе рассматриваются только те методы, в которых нарушена обратная совместимость.

Для миграции на новую версию выполните следующие шаги:

1. Удалите старую версию плагина.
2. Добавьте новую версию плагина используя UPM. Подробнее смотрите в [разделе про подключение плагина](#integration).
3. Замените префаб на активацию через [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html). Подробнее смотрите в [разделе про замену префаба](#init-change).
4. В коде проекта замените те классы и методы, которые были переименованы или поменяли только пакет. Подробнее смотрите в [разделе про переименования](#rename).

### Подключение AppMetrica Push Unity Plugin 2.0.0 {#integration}

Для подключения плагина используется [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

Добавьте зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

```json translate=no
{
  "dependencies": {
      "io.appmetrica.analytics.push": "https://github.com/appmetrica/push-unity-plugin.git#v2.0.0"
  }
}
```

### Замена префаба {#init-change}

1. Создайте static метод с атрибутом `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` и произведите активацию AppMetricaPush с помощью метода `AppMetricaPush.Activate()`.

   > **Пример:**
   >
   > ```csharp translate=no
   > using Io.AppMetrica;
   > using Io.AppMetrica.Push;
   > using UnityEngine;
   >
   > public static class AppMetricaActivator {
   >     [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
   >     private static void Activate() {
   >         AppMetrica.Activate(new AppMetricaConfig("APIKey"));
   >         AppMetricaPush.Activate();
   >     }
   > }
   > ```

   {% note info %}

   `AppMetricaPush.Activate()` должен вызываться после `AppMetrica.Activate()`.

   {% endnote %}

2. Удалите `AppMetricaPush` префаб с ваших сцен.

## Переименование API {#rename}

{% note info %}

Для работы с AppMetricaPush используйте static методы из класса `AppMetricaPush`. Для этого замените `AppMetricaPush.Instance` на `AppMetricaPush` и добавьте импорт `Io.AppMetrica.Push`.

{% endnote %}

* Интерфейс `IYandexMetricaPush` удален, методы перенесены в класс `AppMetricaPush`.
    * Метод `Initialize` переименован в `Activate`.
