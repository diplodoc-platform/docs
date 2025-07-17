# Создание ремаркетинг-трекера

{% note alert %}

Трекер можно создать только после подключения AppMetrica SDK. Подробнее в разделе Интеграция SDK [Android](../sdk/android/analytics/quick-start.md) | [iOS](../sdk/ios/analytics/quick-start.md).

{% endnote %}

Ниже описаны этапы создания трекера для [ремаркетинг-кампании](*ремаркетинг-кампании).

С помощью ремаркетинг-трекера AppMetrica отслеживает возвращение пользователей в приложение ([re-engagement](*re-engagement)) и новые установки. Результаты remarketing-кампании доступны в [отчете Remarketing](../mobile-reports/remarketing-report.md).

{% note info %}

Для рекламных кампаний в Яндекс.Директе можно настроить таргетинг по сегментам из AppMetrica. Для этого необходимо сохранить сегмент в AppMetrica и добавить его в сервисе [Яндекс.Аудитории](https://yandex.ru/support/audience/segments/app-metrica.html). Подробнее в разделе [Как настроить ретаргетинг](https://yandex.ru/adv/news/kak-nastroit-retargeting-dlya-reklamy-mobilnykh-prilozheniy).

{% endnote %}

## Шаг 1. Подготовьте приложение {#step1}

Перед началом ремаркетинг-кампании, подготовьте ваше приложение:

{% list tabs %}

- Android

  1. Добавьте [поддержку deeplink](https://developer.android.com/training/app-links/deep-linking#adding-filters) в своем приложении.
  1. Если используется AppMetrica SDK версии ниже 4.0.0, добавьте [отслеживание открытий deeplink для Android](../data-collection/deeplinks.md).
  
- iOS

  1. Убедитесь, что у вас AppMetrica SDK версии 3.1.2 или выше.
  2. Добавьте [поддержку Universal Links](../sdk/ios/analytics/ios-universal-links.md) в своем приложении.
  3. Добавьте отслеживание открытий deeplink на [iOS](../sdk/ios/analytics/ios-operations.md#deeplink).

{% endlist %}

## Шаг 2. Заполните описание кампании {#step2}

1. В интерфейсе AppMetrica перейдите в раздел **Трекинг** → **Создать трекер**.

2. В блоке **Описание кампании** включите опцию **Это ремаркетинговый трекер** и заполните поля:
    - **Название** — имя трекера. После создания трекер будет доступен в списке трекеров с заданным именем.
    - **Приложение** — приложение, для которого создается трекер.
    - **Партнёр** — рекламный партнер, которому будут отнесены клики, установки, целевые события. Если в списке нет нужного партнера, его можно [добавить](add-partner.md). После добавления новый партнер будет доступен в списке.

    {% note info %}

    После создания трекера изменить партнера в настройках невозможно.

    {% endnote %}

3. Если вы хотите использовать SmartLink для настройки целевой ссылки, включите эту опцию.
   Smartlink позволит создать одну ссылку, которая будет вести в приложение или в соответствующие магазины приложений на разных платформах:

   * Используйте опцию, если рекламная сеть принимает HTTP трекинг-ссылку.
   * Не используйте, если рекламная сеть принимает deeplink.

   При включении Smartlink добавьте в приложении [поддержку Universal Links](../sdk/ios/analytics/ios-universal-links.md).

## Шаг 3. Настройте целевую ссылку / SmartLink {#step3}

{% list tabs %}

- Настройка целевой ссылки

  Заполните поля раздела **Настройка целевой ссылки**:

  ![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/add-destination-url-remarketing.png){style="border: solid 1px #cccccc; max-width: 800px;"}

  Доступные поля:
  
  - **Платформа** — целевая платформа: Android и iOS.
  - **Целевая ссылка** — ссылка в магазин приложений или на страницу, с которой пользователь может установить приложение.
  - **Deeplink** — ссылка вида `myapp://some_data`, с помощью которой можно передать данные в приложение.

      {% note alert %}

      Deeplink обязателен для remarketing-кампаний.

      {% endnote %}
  
- Настройка SmartLink

  {% include [smart-link](_includes/smart-link.md) %}

{% endlist %}

## Шаг 4. _(Опционально)_ Настройте атрибуцию {#step4}

{% include [attribution](_includes/attribution.md) %}

## Шаг 5. _(Опционально)_ Настройте постбеки {#step5}

{% include [postback](_includes/postback.md) %}

## Шаг 6. Используйте трекинг-ссылку и re-engagement deeplink {#step6}

{% note alert %}

Не используйте атрибут `target="_blank"` при вставке ссылки в разметку. Некоторые браузеры могут блокировать переход при открытии ссылки в новом окне.
Не располагайте ссылку в элементе `iframe`.

{% endnote %}

![](https://yastatic.net/s3/doc-binary/src/dev/appmetrica/{{locale}}/images/mobile-tracking/use-tracking-url-remarketing.png){style="border: solid 1px #cccccc; max-width: 800px;"}

Трекинг-ссылку и re-engagement deeplink можно использовать в рекламной кампании после успешного тестирования. Для этого в блоке **Трекинг-ссылка** скопируйте ссылку вида `https://redirect.appmetrica.yandex.com/serve/123456`.

В трекинг-ссылке можно указать предопределенные, статические (UTM) и произвольные параметры, которые будут передаваться в целевую ссылку, deeplink и postback URL. Например, можно отключить JavaScript-редирект с помощью параметра `appmetrica_js_redirect=0`:
```
https://redirect.appmetrica.yandex.com/serve/123456?appmetrica_js_redirect=0
```
Подробнее в разделе [Параметры трекинг-ссылки](tracking-specification.md).

## Пример {#example}

Ремаркетинг-кампания мобильного приложения e-commerce, цель которого — направить пользователя на определенный экран (например, на страницу товара).
 
В зависимости от используемой рекламной сети, существует два сценария создания ремаркетинг-кампании:
 
- Рекламная сеть принимает HTTP-ссылку.
- Рекламная сеть принимает deeplink.
 
{% note info %}

В iOS 12.3 и выше deeplink в трекинг-ссылках не работают. Для корректной работы ремаркетинг-кампаний нужно добавить в приложение [поддержку Universal Links](../sdk/ios/analytics/ios-universal-links.md).
 
{% endnote %}
 
{% list tabs %}
 
- Трекинг-ссылка
 
  Если вам нужно вести пользователя в приложение, в том числе на iOS, используйте [app-to-app трекинг-ссылку](../sdk/ios/analytics/ios-universal-links.md#types). Она будет работать для обеих платформ.
  Допишите необходимые параметры в app-to-app трекинг-ссылку:
  - В Android переход в приложение происходит через редирект на deeplink, указанный в трекере. Можно передать необходимые параметры из трекинг-ссылки в Android deeplink. Подробнее в разделе [{#T}](tracking-specification.md).
  - В iOS приложение открывается самой ссылкой и метки из ссылки при переходе будут получены в AppMetrica и попадут в отчет.
 
- Re-engagement deeplink
 
  Допишите необходимые параметры в полученный deeplink.
 
{% endlist %}

## См. также {#learn-more}

- [{#T}](remarketing-attribution.md)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}

[*ремаркетинг-кампании]: Рекламная кампания, которая направлена на возвращение пользователей в установленное приложение.

[*re-engagement]: {{ re-engagement }}

[*Постбеки]: GET-запрос по заданной ссылке (postback URL), в который можно передать определенные параметры. Для одной кампании можно добавить до 5 запросов. Подробнее о [политике отправки postback](policy.md).

[*PostbackURL]: Ссылка, по которой отправляется сообщение о событии (установка или целевое событие). Получателем события является партнер. В postback URL можно [передать дополнительные параметры](postback-specification.md).
