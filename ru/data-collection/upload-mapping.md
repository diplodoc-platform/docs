# Загрузка mapping-файлов и отладочных символов на Android

AppMetrica позволяет собирать информацию о нативных и java-крэшах. Их можно анализировать в отчете [Крэши и ошибки](../mobile-reports/crashes-and-errors.md). См. также раздел [Настройка сбора данных](about-crashes-and-errors.md).

Чтобы уменьшить размер приложения, код [оптимизируют](https://developer.android.com/studio/build/shrink-code) во время релизной сборки.

Если во время сборки Android-приложения сжимали и обфусцировали код, то информация о крэшах передается в обфусцированном виде. Чтобы извлечь данные для анализа из таких крэш-логов, AppMetrica выполняет деобфускацию на стороне сервера.

Для этого загрузите mapping-файлы или отладочные символы SO-файлов в AppMetrica: автоматически при сборке приложения или вручную через веб-интерфейс.

Чтобы отправлять файлы, подключите [AppMetrica Gradle Plugin](../sdk/android/analytics/android-gradle-plugin.md).

{% note info "" %}

Загружайте mapping-файлы, если вы используете [ProGuard](https://www.guardsquare.com/en/products/proguard/manual) или [R8](https://r8.googlesource.com/r8/). Если вы не сжимаете и не обфусцируете код, не подключайте плагин.

{% endnote %}

## Узнать больше {#learn-more}

- [Отчет Крэши и ошибки](../mobile-reports/crashes-and-errors.md)
- [Документация Android](https://developer.android.com/topic/performance/vitals/crash)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
