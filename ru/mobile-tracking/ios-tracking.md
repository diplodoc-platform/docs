# Трекинг в iOS 14.5+

## Изменения в iOS 14.5 {#new-ios-version}

Начиная с версии iOS 14.5 у приложений и рекламных сетей по умолчанию нет доступа к IDFA — сквозному идентификатору устройства, который помогает «узнавать» одного и того же пользователя между приложениями.

[Запросить](ios-tracking.md) у пользователя доступ к IDFA можно двумя способами:

- показать окно выбора при запуске приложения — но только один раз;
- предложить перейти в системные настройки;
 Если пользователь откажется — идентифицировать устройство не получится.

Владелец устройства мог и раньше запретить приложениям получать IDFA (через те же системные настройки), но это делали лишь несколько процентов пользователей. Теперь доля аудитории без IDFA значительно вырастет.

Вместе с этим ограничением новые правила Apple запрещают попытки идентифицировать устройство другими способами, в том числе эвристическими: компания не разрешает использовать fingerprint и probability matching.

## На что повлияет отсутствие доступа к IDFA? {#idfa}

**Поведенческий таргетинг**

:   В ряде рекламных сетей ухудшится возможность таргетинга по поведенческим признакам аудитории. Приложения перестанут «узнавать» пользователя и показывать ему релевантную рекламу, ее эффективность снизится.

**Оптимизация рекламных кампаний**

:   Рекламный партнер не сможет на лету корректировать настройки, чтобы показывать рекламу пользователям, которые совершают больше конверсий — без IDFA не получится выделить из всей аудитории наиболее конверсионных пользователей.

**Атрибуция установки приложения**

:   В трекерах перестанет работать атрибуция iOS-установок и последующих целевых действий (для устройств без IDFA). Если пользователь не разрешит доступ к IDFA, трекер не сможет отследить конкретные источники трафика, поэтому установки по умолчанию будут попадать в органику.

**Полнота статистики**

:   Статистика от Apple будет агрегированной и не «склеится» с остальными показателями в отчетах — сравнить эффективность площадок будет сложнее. Кроме того, не получится достоверно оценить LTV пользователей, которых привела та или иная рекламная сеть.

## SKAdNetwork {#SKAdNetwork}

Applе предлагает собственную атрибуцию — [SKAdNetwork](https://developer.apple.com/documentation/storekit/skadnetwork). Она будет работать даже для тех пользователей, которые не дали разрешение на отслеживание — это единственный способ подсчета полноценной статистики.

Для этого рекламные сети должны отправлять в Apple данные о рекламных размещениях, а разработчики и издатели — о конверсиях из своих приложений. Отправка происходит через специальный фреймворк от Apple — SKAdNetwork, который должны поддержать обе стороны. Через него же Apple будет возвращать статистику, но в непривычном виде: платформа не будет формировать отчеты. Вместо этого рекламные сети будут получать от Apple агрегированные данные о кликах и установках. Они смогут собирать их в отдельные отчеты и транслировать рекламодателям.

Трекеры в новой модели по умолчанию не получают данные от SKAdNetwork. Но рекламные сети могут [передавать](ios-tracking-skadnetwork.md) полученные от Apple данные в трекеры, чтобы рекламодатели могли оценивать эффективность разных каналов в едином интерфейсе.

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/apple-attribution.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Как выглядит статистика в AppMetrica {#report}

Для анализа источников установок с iOS 14.5+ доступен отдельный отчет с агрегированными данными от рекламных сетей, которые они получают через SKAdNetwork.

Отчет User Acquisition содержит информацию об источниках установки приложения, полученных из SKAdNetwork. Здесь недоступны сегментация и метрики по событиям, посчитанные по данным AppMetrica.

[Подробнее про отчет](../mobile-reports/user-acquisition-skadnetwork.md).

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/report-ios-14-2.png){style="border: solid 1px #cccccc; max-width: 800px;"}

## Apple Search Ads {#apple-search-ads}

Выход iOS 14.5 не повлияет на возможности Apple Search Ads — собственной платформы Apple для продвижения приложений, в которой атрибуция работает иначе. Другой новый фреймворк от Apple — AdServices — обеспечивает атрибуцию конкретного девайса, но при этом не раскрывает разработчику IDFA устройства. Это позволяет сохранить привычные преимущества трекинга — точный подсчет конверсий и действий в приложении в привязке к пользователю, а также возможность сегментировать пользователей и исследовать их поведение в приложении.

{% note info %}

Apple Search Ads не работает через SKAdNetwork.

{% endnote %}

О трекинге кампаний Apple Search Ads можно прочитать на [странице](searchads-settings.md).

## Запрос доступа к IDFA через App Tracking Transparency {#request}

При работе с iOS 14 используйте новый фреймворк [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency). С его помощью отобразите системное диалоговое окно в своем приложении. В окне пользователь выберет разрешить или запретить доступ к IDFA.

{% note info %}

Системное диалоговое окно может отображаться только один раз при каждой установке приложения. Если пользователь выберет **Ask App Not to Track**, возможности показать это окно снова для этого приложения не будет.

{% endnote %}

1. Системное диалоговое окно нельзя менять, но в него можно добавить текст с пояснением. Для этого добавьте ключ `NSUserTrackingUsageDescription` в `Info.plist`. Например:

    ```no-highlight translate=no
    <key>NSUserTrackingUsageDescription</key>
    <string>This identifier will be used to deliver personalized ads to you.</string>
    ```

    Текст из `Info.plist` будет показан пользователю в системном диалоговом окне. В тексте объясните пользователю, почему приложение запрашивает разрешение на использование IDFA.

2. Чтобы отобразить диалоговое окно с запросом доступа к IDFA, вызовите метод [requestTrackingAuthorization(completionHandler:)](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547037-requesttrackingauthorization).

    {% cut "Пример системного диалогового окна" %}

    ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/common/alert-ios-14.png){style="border: solid 1px #cccccc; max-width: 800px;"}

    {% endcut %}

3. Прежде чем загружать рекламу дождитесь получения callback. Тогда Yandex Mobile Ads SDK сможет использовать IDFA в запросах за рекламой.

    ```objectivec translate=no
    #import <AppTrackingTransparency/AppTrackingTransparency.h>
    ...
    - (void)requestTrackingAuthorization {
    [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
    // Start ad loading
    }];
    }
    ```

4. Чтобы проверить статус авторизации App Tracking Transparency, используйте свойство [trackingAuthorizationStatus](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547038-trackingauthorizationstatus).

Больше информации по App Tracking Transparency доступно в документации [Apple](https://developer.apple.com/documentation/apptrackingtransparency).

[Подробнее](ios15-tracking.md) о трекинге в приложениях iOS 15.

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
