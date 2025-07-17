# Сегментация

Все методы API отчетов позволяют возвращать результаты, рассчитанные не только по всему сайту, но и по отдельному сегменту данных. Для задания сегмента используйте параметр `filters`.

Вы можете сегментировать запрос по измерениям и метрикам. При этом измерение и метрика могут быть не указаны в запросе.

Фильтры по измерениям будут применены к исходным (не сгруппированным) данным, фильтры по метрикам — уже к сгруппированным строкам результата.

Для задания фильтра в URL-адресе запроса необходимо использовать [URL-кодирование](http://ru.wikipedia.org/wiki/URL#.D0.9A.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_URL).

## Формат фильтра {#format}

```xml translate=no
attribute operator 'value'
```

где

- `attribute` — группировка или метрика. Например, `ym:ge:mobileDeviceModel` или `ym:ge:users`.
- `operator` — [оператор фильтрации](../api_v1/relations/relations.md). Указывает какой тип фильтра будет применен. Например, `==`.
- `value` — значение для сравнения. В строке со значением должны быть экранированы символы `'` и `\` с помощью символа `\`.

При этом действует лимит: количество уникальных группировок и метрик — до 10, количество отдельных фильтров — до 20, длина строки в фильтре — до 2000 символов.

Например, чтобы получить данные только по визитам из Москвы, используйте фильтр:

```xml translate=no
filters=ym:ge:regionCity=='Москва'
```

Для разных группировок доступны разные операторы фильтрации (например, см. столбец Типы соответствий в разделе [Приложение](attributes/mobmet_events/app.md)).

Чтобы сочетать фильтры между собой в запросе, используйте бинарные операторы `AND` и `OR`, а также унарный оператор `NOT`:

```xml translate=no
&metrics=ym:ge:users&dimensions=ym:ge:age&filters=NOT(ym:ge:age!=18)
```

```xml translate=no
ym:ge:regionCity=='Москва' OR ym:ge:regionCity=='Санкт-Петербург'
```

А также задавайте приоритет с помощью круглых скобок:

```xml translate=no
(ym:ge:regionCity=='Москва' OR ym:ge:regionCity=='Санкт-Петербург') AND ym:ge:gender=='мужской'
```

Фильтры по измерениям и по метрикам можно комбинировать только на верхнем уровне (вне скобок) и только через оператор `AND`.


{% note info %}

Язык запроса (параметр `lang`) влияет на значения фильтров. Рекомендуем всегда указывать данный параметр.

{% endnote %}

## Пример использования сегментации {#example}

**Количество посетителей с учетом региона**

`dimensions=ym:ge:mobileDeviceModel`
 
`metrics=ym:ge:users`
 
`filters=ym:ge:regionCityName=='Москва'`
 
{% list tabs %}
 
- cURL
 
  ```bash translate=no
  curl -X GET \
    'https://api.appmetrica.yandex.ru/stat/v1/data?id=1111&metrics=ym:ge:users&dimensions=ym:ge:mobileDeviceModel&filters=ym:ge:regionCityName==%27Москва%27' \
    -H 'Authorization: OAuth <your_token>'
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

- HTTP

  ```http translate=no
  GET /stat/v1/data?id=1111&metrics=ym:ge:users&dimensions=ym:ge:mobileDeviceModel&filters=ym:ge:regionCityName=='Москва' HTTP/1.1
  Host: api.appmetrica.yandex.ru
  Authorization: OAuth <your_token>
  ```

  где `<your_token>` — это OAuth-токен, который можно получить по [инструкции](../intro/authorization.md#get-oauth-token).

{% endlist %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
