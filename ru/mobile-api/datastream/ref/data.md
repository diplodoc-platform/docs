# Скачивание данных

{{ data }}

**Квотирование**

:   Разрешается не более 10 параллельных загрузок.

**Сжатые данные**

:   Рекомендуется в запросе передавать заголовок `Accept-Encoding: gzip`, чтобы по сети быстрее передавались большие файлы, сжатые при помощи кодека `gzip`.

## Формат запроса {#request-format}

```
GET {{ api-url }}/datastream/v1/application/{id}/data
  ? data_type=<string>
  & stream_window_timestamp=<string>
```
#|
|| `id` | Идентификатор приложения. ||
|| `data_type`* | Указывает, данные какого потока загружать.

Допустимые значения:

- `event`
- `installation`
- `session_start`
- `session_end`
- `push_token`
- `crash`
- `error`
- `click`
- `revenue`
- `ecommerce`
- `ad_revenue`
- `attributed_event`
- `deeplink`
||
|| `stream_window_timestamp`* | Секундный unix-timestamp, указывающий на окно данных. Какие окна данных доступны, можно узнать с помощью операции [Состояние потока](status.md). ||
|#

## Коды ответов {#codes}

| Код ответа | Описание |
| ----- | ----- |
| 404 | Отсутствие данных. Значение параметра `stream_window_timestamp` на данный момент отсутствует в ответе на запрос [Состояние потока](status.md). |
| 500 | Ошибка на стороне сервера AppMetrica. Повторный запрос не будет успешным. Обратитесь в [службу поддержки](../../../troubleshooting/feedback-new.md). |
| 503 | Ошибка на стороне сервера AppMetrica. Повторные запросы могут быть успешны. |

## Пример {#example}

Запрос:

```bash translate=no
curl -X GET '{{ api-url }}/datastream/v1/application/1111/data?data_type=event&stream_window_timestamp=1670202610' \
-o events1670202610.csv \
-H 'Authorization: OAuth oauth_token' \
-H 'Accept-Encoding: gzip'
```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
