# Квотирование

Ограничения вызовов Logs API применяются к API key приложения. Это значит, что ограничения для <q>Приложения 1</q> не влияют на ограничения для <q>Приложения 2</q>.

При отправке запроса Logs API помещает его в очередь на обработку. В очереди может находиться не более трех одновременных запросов для одного API key. В случае превышения квоты Logs API возвращает:

```no-highlight translate=no
HTTP/1.1 429 Too Many Requests
Content-Type: text/plain

There are already 3 enqueued queries for given application_id. Wait until they are completed.
```

{% note info %}

Длительность нахождения запроса в очереди зависит от текущей загрузки сервера и объема обрабатываемых данных вашего приложения.

{% endnote %}

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
