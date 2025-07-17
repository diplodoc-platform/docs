# Подключение и инициализация

AppMetrica Push Unity — это плагин для игровой платформы [Unity3d](http://docs.unity3d.com/), включающий поддержку AppMetrica Push SDK для платформ Android и iOS.

Ниже описаны этапы подключения и инициализации AppMetrica Unity Plugin:

## Шаг 1. Подключите плагин AppMetrica Unity {#integration-appmetrica}

Подключить плагин AppMetrica Unity согласно [инструкции](../analytics/quick-start.md).

{% note info %}

Требуется плагин AppMetrica Unity не ниже версии 6.1.0.

{% endnote %}

## Шаг 2. Подключите плагин AppMetrica Push Unity {#integration}

Для подключения плагина используется [Unity Package Manager](https://docs.unity3d.com/Manual/Packages.html).

Добавьте зависимости в [Packages/manifest.json](https://docs.unity3d.com/Manual/upm-manifestPrj.html):

```json translate=no
{
  "dependencies": {
    "io.appmetrica.analytics.push": "https://github.com/appmetrica/push-unity-plugin.git#v{{ appmetrica-push-unity-plugin }}"
  }
}
```

## Шаг 3. Инициализируйте библиотеку {#activate}

Рекомендуется активировать AppMetrica Push используя [RuntimeInitializeOnLoadMethodAttribute](https://docs.unity3d.com/ScriptReference/RuntimeInitializeOnLoadMethodAttribute.html).

Создайте static метод с атрибутом `[RuntimeInitializeOnLoadMethod(RuntimeInitializeLoadType.BeforeSceneLoad)]` и произведите активацию AppMetricaPush с помощью метода `AppMetricaPush.Activate()`.

> Пример:
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

## Шаг 4. Добавьте настройки для каждой нативной платформы {#platforms}

{% list tabs %}

- Android

  1. [Настройте](../../android/push/android-settings.md#firebase) приложение для использования Firebase. [Получите и добавьте в AppMetrica](../../android/push/android-settings.md#firebase-key) ключ сервера для использования Firebase Cloud Messaging.
  2. Чтобы настроить AndroidManifest.xml, внесите изменения в элемент `application` файла `AndroidManifest.xml`:

     ```xml translate=no
     <meta-data android:name="ymp_firebase_default_app_id" android:value="APP_ID"/>
     <meta-data android:name="ymp_gcm_default_sender_id" android:value="number:SENDER_ID"/>
     <meta-data android:name="ymp_firebase_default_api_key" android:value="API_KEY"/>
     <meta-data android:name="ymp_firebase_default_project_id" android:value="PROJECT_ID"/>
     ```

     {{ app-id }}

     {{ sender-id }}

     {{ api-key-push }}

     {{ project-id }}

- iOS
  
  1. Добавьте SSL-сертификат в AppMetrica по [инструкции](../../ios/push/ios-settings.md).
  2. Чтобы получать push-уведомления, запросите у пользователя разрешение и зарегистрируйте приложение для получения уведомлений. Рекомендуется использовать Unity-пакет [Mobile Notifications](https://docs.unity3d.com/Packages/com.unity.mobile.notifications@2.0/manual/index.html) и следовать [инструкции](https://docs.unity3d.com/Packages/com.unity.mobile.notifications@2.0/manual/iOS.html#authorization-request).

  {% note info %}

  AppMetrica Push Unity Plugin использует механизм <q>swizzling</q> для своей работы: перехватывает выполнение некоторых методов класса `UnityAppController` используя ObjectiveC runtime. Код механизма представлен в файле [AMPUAppMetricaPushAppController.m](https://github.com/appmetrica/push-unity-plugin/blob/main/Runtime/Plugins/iOS/AMPUAppMetricaPushAppController.m).

  {% endnote %}

{% endlist %}

### См. также

- [Настройка приложения на базе Android для отправки push-уведомлений](../../android/push/android-settings.md)
- [Настройка приложения на базе iOS для отправки push-уведомлений](../../ios/push/ios-settings.md)
- [Запуск push-кампании](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
