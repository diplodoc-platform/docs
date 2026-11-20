# Табы

Используйте табы для взаимоисключающих разделов. Например, чтобы разделить инструкции для разных ОС.

{% include [blank-lines](../../_includes/blank-lines-note.md) %}

```markdown
{% list tabs %}

- Название таба 1

  Текст таба 1.

  * Можно использовать списки.
  * И **другую** разметку.

- Название таба 2

  Текст таба 2.

{% endlist %}
```

**Результат:**

{% list tabs %}

- Название таба 1

  Текст таба 1.

  * Можно использовать списки.
  * И **другую** разметку.

- Название таба 2

  Текст таба 2.

{% endlist %}

<video controls playsinline preload="metadata" poster="ru/_assets/screencaster/tabs-ru.png" style="width:100%">
  <source src="ru/_assets/screencaster/tabs-ru.mp4" type="video/mp4" />
  <track kind="subtitles" src="ru/_assets/screencaster/tabs-ru.vtt" srclang="ru" label="Русский" default />
</video>

Видео сгенерировано с помощью [скриншотницы Diplodoc](../../guides/screencaster.md).

{% include [common-params](../../_includes/common-params-note.md) %}
