# Tabs

Use tabs for mutually exclusive sections. For example, to separate instructions for different operating systems.

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

**Result:**

{% list tabs %}

- Tab 1 title

  Tab 1 text.

  * You can use lists.
  * And **other** markup.

- Tab 2 title

  Tab 2 text.

{% endlist %}

{% include [common-params](../../_includes/common-params-note.md) %}
