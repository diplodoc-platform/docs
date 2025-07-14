## Синхронизация

Чтобы синхронизировать переключение одинаковых элементов на странице, используйте атрибут `group`:

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

  - Next

    hello world 2


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

  - Next

    hello world 2

{% endlist %}

Выбранный элемент запоминается и автоматически открывается на всех страницах документационного проекта с тем же значением `group`. Например, выбрав таб **MacOS** на одной странице, пользователь увидит его активным на всех страницах.

{% note info %}

Состояние интерактивных элементов сохраняется после перезагрузки страницы.

{% endnote %}

