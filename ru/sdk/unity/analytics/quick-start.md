# Подключение и инициализация

AppMetrica Unity — плагин для игровой платформы [Unity3d](http://docs.unity3d.com/). Он включает поддержку AppMetrica SDK для Android и iOS.

Ниже описаны этапы подключения и инициализации AppMetrica Unity Plugin:

## Шаг 1. Подключите плагин AppMetrica Unity {#integration}

{% list tabs %}

- OpenUPM

  Добавьте зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

  ```json translate=no
  {
    "scopedRegistries": [
      {
        "name": "package.openupm.com",
        "url": "https://package.openupm.com",
        "scopes": [
          "com.google.external-dependency-manager",
          "io.appmetrica.analytics"
        ]
      }
    ],
    "dependencies": {
      "com.google.external-dependency-manager": "{{ google-external-dependency-manager }}",
      "io.appmetrica.analytics": "{{ appmetrica-unity-plugin }}"      
    }
  }
  ```

- UPM (GitHub)

  1. Подключите External Dependency Manager согласно [документации](https://github.com/googlesamples/unity-jar-resolver/tree/master?tab=readme-ov-file#getting-started).

  2. Добавьте AppMetrica Unity Plugin в зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

    ```json translate=no
    {
      "dependencies": {
        "io.appmetrica.analytics": "https://github.com/appmetrica/appmetrica-unity-plugin.git#v{{ appmetrica-unity-plugin }}"
      }
    }
     ```

{% endlist %}

## Шаг 2. Инициализируйте библиотеку {#initialization}

Рекомендуется активировать AppMetrica используя [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html).

Создайте static метод с атрибутом `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` и произведите активацию AppMetrica с помощью метода `AppMetrica.Activate()`.

Пример:

```csharp translate=no
using Io.AppMetrica;
using UnityEngine;

public static class AppMetricaActivator {
    [RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]
    private static void Activate() {
        AppMetrica.Activate(new AppMetricaConfig("APIKey") {
            FirstActivationAsUpdate = !IsFirstLaunch(),
        });
    }

    private static bool IsFirstLaunch() {
        // Implement logic to detect whether the app is opening for the first time.
        // For example, you can check for files (settings, databases, and so on),
        // which the app creates on its first launch.
        return true;
     }
}
```

## Узнайте больше {#learn-more}

- [Настройка отправки событий Ecommerce](unity-operations.md#send-ecommerce)
- [Настройка отправки событий Revenue](unity-operations.md#send-revenue)
- [Настройка отправки событий Ad Revenue](unity-operations.md#send-adrevenue)
- [Как включить отправку данных о местоположении пользователей?](../../../troubleshooting/troubleshooting.md#region)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
