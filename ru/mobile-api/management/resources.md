# Ресурсы API

#|
|| **Операция** | **Описание** ||
|| [GET /management/v1/application/{id}](applications/getapplication.md) | Возвращает информацию об указанном приложении. ||
|| [GET /management/v1/applications](applications/getapplicationslist.md) | Возвращает информацию о приложениях, доступных пользователю. ||
|| [GET /management/v1/metadata/application/categories](applications/get-categories.md) | Возвращает список всех категорий приложений. ||
|| [POST /management/v1/applications](applications/createapplication.md) | Добавляет приложение в AppMetrica. ||
|| [PUT /management/v1/application/{id}](applications/updateapplication.md) | Изменяет настройки указанного приложения. ||
|| [POST /management/v1/application/{id}/grants](applications/access/grant.md) | Выдает доступ к статистике определенному пользователю или агентству. ||
|| [PUT /management/v1/application/{id}/grant](applications/access/edit.md) | Изменяет ранее выданные права доступа. ||
|| [GET /management/v1/tracking/partners](applications/access/list-partners.md) | Возвращает список партнеров. ||
|| [GET /v1/traffic/sources/events?appId={id}](applications/access/list-events.md) | Возвращает список пользовательских событий. ||
|| [DELETE /management/v1/application/{id}/grant?user_login={login}](applications/access/delete.md) | Удаляет ранее выданные права доступа. ||
|| [DELETE /management/v1/application/{id}](applications/deleteapplication.md) | Удаляет указанное приложение. ||
|| [GET /management/v1/application/{id}/events_certs_fingerprints/android](fingerprints/fingerprints-android-get.md) | {{ fingerptints-get }} ||
|| [POST /management/v1/application/{id}/events_certs_fingerprints/android/add](fingerprints/fingerprints-android-post.md) | {{ fingerptints-post }} ||
|| [DELETE /management/v1/application/{id}/events_certs_fingerprints/android/{fingerprint_id}](fingerprints/fingerprints-android-delete.md) | {{ fingerptints-delete }} ||
|| [GET /management/v1/logsapi/status](logs-api-status.md) | Проверяет доступность [Logs API](../logs/about.md). ||
|#

{{ feedback }}

<a href="../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../_includes/feedback-button.md) %}
