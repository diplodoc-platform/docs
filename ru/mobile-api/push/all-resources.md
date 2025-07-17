# Ресурсы API

#|
|| **Операция** | **Метод и ресурс** ||
|| Создание группы | [POST /push/v1/management/groups](post-groups.md) ||
|| Получение списка групп | [GET /push/v1/management/groups](get-groups.md) ||
|| Получение группы | [GET /push/v1/management/group/{groupId}](get-group-id.md) ||
|| Обновление группы | [PUT /push/v1/management/group/{groupId}](put-group-id.md) ||
|| Архивирование группы | [DELETE /push/v1/management/group/{groupId}](delete-group-id.md) ||
|| Вывод группы из архива | [POST /push/v1/management/group/{groupId}/restore](post-group-id.md) ||
|| Отправка группы push-сообщений | [POST /push/v1/send-batch](post-send-batch.md) ||
|| Проверка статуса отправки по transferId | [GET /push/v1/status/{transferId}](get-status-id.md) ||
|| Проверка статуса отправки по clientTransferId | [GET /push/v1/status/{groupId}/{clientTransferId}](get-status-group-id.md) ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
