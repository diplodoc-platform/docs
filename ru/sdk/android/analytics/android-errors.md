# Описание ошибок

{% note info "" %}

{% include notitle [android-logs-help](../../_includes/android-logs-help.md) %}

{% endnote %}

Ниже описаны распространенные ошибки, которые могут возникнуть при работе с AppMetrica SDK на Android.

## Не увеличивается число сессий {#session}

Проверьте настройки отслеживания сессий. Подробнее в разделе Отслеживание активности пользователей.

## Нет событий {#events}

1. Совершите в приложении минимум 10 действий, которые инициируют отправку событий.
Это необходимо, потому что события накапливаются и отправляются на сервер по несколько штук.

2. Подождите 10 минут и проверьте отчет. События отображаются в отчете не сразу.

## Ошибка при добавлении библиотеки в проект {#add-in-project}

```java translate=no
UNEXPECTED TOP-LEVEL EXCEPTION:
com.android.dex.DexIndexOverflowException: method ID not in [0, 0xffff]: 65536
at com.android.dx.merge.DexMerger$6.updateIndex(DexMerger.java:502)
at com.android.dx.merge.DexMerger.mergeMethodIds(DexMerger.java:491)
at com.android.dx.merge.DexMerger$IdMerger.mergeSorted(DexMerger.java:277)
at com.android.dx.command.dexer.Main.runMonoDex(Main.java:303)
at com.android.dx.command.dexer.Main.mergeLibraryDexBuffers(Main.java:454)
at com.android.dx.merge.DexMerger.mergeDexes(DexMerger.java:168)
at com.android.dx.merge.DexMerger.merge(DexMerger.java:189)
at com.android.dx.command.dexer.Main.run(Main.java:246)
at com.android.dx.command.dexer.Main.main(Main.java:215)
at com.android.dx.command.Main.main(Main.java:106)
```

Данная ошибка сообщает, что превышен лимит методов на этапе обработки DexIndexOverflowException. Рекомендуем пересмотреть используемые библиотеки — возможно, они очень тяжеловесны. Если их нельзя заменить легковесными аналогами, то можно использовать [несколько DEX-файлов](https://developer.android.com/tools/building/multidex.html). Это может увеличить время загрузки приложения.

## Некорректная длительность пользовательской сессии при ручном отслеживании {#listen-root}

При неправильной реализации [ручного отслеживания](android-listen.md#listen) сессии возможно неточное определение ее длительности.

Если данные о длительности сессий выглядят некорректно, убедитесь, что при завершении пользовательской сессии всегда вызывается метод `AppMetrica.pauseSession()`. Если метод не вызван, библиотека считает сессию активной и совершает регулярный обмен данными с серверной частью AppMetrica.

Рекомендуется проверить длительности таймаута сессии. Он устанавливается с помощью метода `withSessionTimeout()`. Таймаут указывает временной интервал, в течение которого сессия будет считаться активной даже после закрытия приложения.

## Высокое энергопотребление библиотекой AppMetrica {#power}

При повышенном энергопотреблении библиотекой, убедитесь, что при завершении пользовательской сессии всегда вызывается метод `AppMetrica.pauseSession()`. Если метод не вызван, библиотека считает сессию активной и совершает регулярный обмен данными с серверной частью AppMetrica.

Рекомендуется проверить длительности таймаута сессии. Он устанавливается с помощью метода `withSessionTimeout()`. Таймаут указывает временной интервал, в течение которого сессия будет считаться активной даже после закрытия приложения.

## Конфликт при использовании автосбора Ad Revenue для Fyber {#fyber-unsupport-adrevenue}

Автосбор Ad Revenue для Fyber не поддерживается и приводит к конфликту в коде на версиях от `6.4.0` до `7.0.0`.

Если вы вызываете метод `Interstitial.setInterstitialListener`, то исключите модуль `io.appmetrica.analytics:analytics-ad-revenue-fyber-v3` из списка зависимостей для предотвращения конфликта.

## В списке нет моей проблемы {#not-found}

Если в списке нет вашей проблемы, обратитесь в [службу поддержки](../../../troubleshooting/feedback-new.md). В обращении укажите:

1. Пример интеграции SDK в вашем приложении.
2. ID приложения в веб-интерфейсе AppMetrica.
3. ID устройства.

   {% cut "Как получить Google AID" %}

    1. Установите приложение [AppMetrica](https://play.google.com/store/apps/details?id=ru.yandex.mobile.appmetrica) на тестовое устройство.
    2. Авторизуйтесь и выберите из списка ваше приложение в AppMetrica.
    3. В левом верхнем углу нажмите ![hum](../../../../_images/hum.png) → **Устройство**.
    4. Google AID указан в поле **AID**. Укажите его в веб-интерфейсе AppMetrica.

       {% note tip %}

       Тестирование атрибуции можно включить в приложении AppMetrica. Для этого включите **Тест атрибуции**.

       {% endnote %}
       
4. Производителя и модель устройства, платформу и версию ОС, версию AppMetrica SDK.

   {% endcut %}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
