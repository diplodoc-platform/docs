# Cuts

Use cuts to hide part of the content. For example, additional information or long code blocks.

{% include [blank-lines](../../_includes/blank-lines-note.md) %}

```markdown
{% cut "Заголовок ката" %}

Контент, который отобразится по нажатию.

{% endcut %}
```

**Result:**

{% cut "Cut title" %}

Content that will be displayed on click.

{% endcut %}

## Anchor links{#anchor}

You can set an anchor for a cut; following a link with an anchor automatically navigates to the cut and opens it. This also works for cuts nested inside one another.

```markdown
Ссылка для раскрытия [внешнего ката](#outside-cut), ссылка для раскрытия [вложенного ката](#inside-cut).

{% cut "Заголовок внешнего ката" %}{#outside-cut}

Контент первого уровня.

{% cut "Заголовок вложенного ката" %}{#inside-cut}

Контент второго уровня.

{% endcut %}

{% endcut %}
```

**Result:**

Link to open [an outer cut](#outside-cut), link to open [a nested cut](#inside-cut).

{% cut "Outer cut title" %}{#outside-cut}

First-level content.

{% cut "Nested cut title" %}{#inside-cut}

Second-level content.

{% endcut %}

{% endcut %}

## Cut groups{#group}

Cuts can be combined into groups using the `name` parameter. When one cut is expanded, other cuts in the same group are closed.

```markdown
{% cut "Кат 1" %}{name=cutgroup}

Контент первого ката.

{% endcut %}

{% cut "Кат 2" %}{name=cutgroup}

Контент второго ката.

{% endcut %}

{% cut "Кат 3" %}{#cut-3 name=cutgroup}

Контент второго ката.

{% endcut %}
```

**Result:**

{% cut "Cut 1" %}{name=cutgroup}

Content of the first cut.

{% endcut %}

{% cut "Cut 2" %}{name=cutgroup}

Content of the second cut.

{% endcut %}

{% cut "Cut 3" %}{#cut-3 name=cutgroup}

Content of the third cut.

{% endcut %}

{% note info %}

Cuts do not support the ability to expand [an element by default](./common-params.md#selected).

{% endnote %}