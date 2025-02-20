# Табы

Используйте табы для взаимоисключающих разделов. Например, чтобы разделить инструкции для разных ОС.

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

{% endcut %}

## Элемент по умолчанию

Если нужно, чтобы элемент был раскрыт по умолчанию, добавьте к нему атрибут `{selected}`.

```markdown
{% list tabs %}

- Название таба 1

  Текст таба 1.

- Название таба 2 {selected}

  Пункт будет открыт по умолчанию.

- Название таба 3

  Текст таба 3.

{% endlist %}
```

**Результат:**

{% list tabs %}

- Название таба 1

  Текст таба 1.

- Название таба 2 {selected}

  Пункт будет открыт по умолчанию.

- Название таба 3

  Текст таба 3.

{% endlist %}


## Синхронизация

Чтобы одновременно переключать единообразные вкладки в пределах одной страницы, примените атрибут `group`:

```markdown
{% list tabs group=instructions %}

  - Python

    About python

    - Tab with list
    - One
    - Two

  - Tab with list
    1. One
    2. Two

  - Next

    hello world

{% endlist %}



{% list tabs group=instructions %}

  - Python

    About python

    - Tab with list
    - One
    - Two

  - Tab with list
    1. One
    2. Two

    {% note info %}
    Попробуйте перезагрузить страницу, чтобы увидеть, что вкладка `Tab with list` активна.
    {% endnote %}

  - Next

    hello world 2

    {% note info %}
    Попробуйте перезагрузить страницу, чтобы увидеть, что вкладка `Next` активна.
    {% endnote %}


{% endlist %}
```

**Результат:**

{% list tabs group=instructions %}

  - Python

    About python

    - Tab with list
    - One
    - Two


  - Tab with list

    1. One
    2. Two


  - Next

    hello world

{% endlist %}



{% list tabs group=instructions %}

  - Python

    About python

    - Tab with list
    - One
    - Two


  - Tab with list

    1. One
    2. Two

    {% note info %}

    Попробуйте перезагрузить страницу, чтобы увидеть, что вкладка `Tab with list` активна.
    
    {% endnote %}


  - Next

    hello world 2

    {% note info %}

    Попробуйте перезагрузить страницу, чтобы увидеть, что вкладка `Next` активна.

    {% endnote %}

{% endlist %}
