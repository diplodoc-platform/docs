# Каты и табы

Благодаря расширениям YFM вы можете использовать интерактивные элементы разметки: каты и табы.

{% note info %}

Содержимое катов и табов может включать любую разметку YFM.

{% endnote %}

## Каты {#cuts}

Используйте каты, чтобы скрыть часть контента. Например, дополнительную информацию или длинные блоки кода.

```markdown
{% cut "Заголовок ката" %}

Контент, который отобразится по нажатию.

{% endcut %}
```

**Результат:**

{% cut "Заголовок ката" %}

Контент, который отобразится по нажатию.

{% endcut %}

## Табы {#tabs}

Используйте табы для взаимоисключающих разделов. Например, чтобы разделить инструкции для разных ОС.

Для корректного отображения табов отделяйте пустыми строками:
* `{% list tabs %}` и `{% endlist %}`;
* текст одного таба и название следующего таба.

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
