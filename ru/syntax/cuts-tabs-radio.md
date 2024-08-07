# Каты, табы и радиобаттоны

Благодаря расширениям YFM вы можете использовать интерактивные элементы разметки: каты, табы и радиобаттоны.

{% note info %}

Содержимое катов, табов и радиобаттонов может включать любую разметку YFM.

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

## Радиобаттоны {#radio}

Радиобаттоны работают подобно табам. Например, для разделения инструкций для разных платформ.

```markdown
{% list tabs radio %}

- Название радиобаттона 1

  Текст радиобаттона 1  

- Название радиобаттона 1

  Текст радиобаттона 2

{% endlist %}
```


{% cut "Пример применения и результат" %}

```markdown
{% list tabs radio %}

- Название радиобаттона 1

  Текст радиобаттона 1.

  Можно вложить еще один перечень радиобаттонов.

  {% list tabs radio %}

  - Вложенный радиобаттон 1

    Текст вложенного радиобаттона

  - Вложенный радиобаттон 2

    Текст вложенного радиобаттона    

  {% endlist %}
  

- Название радиобаттона 2

  Текст радиобаттона 2.

{% endlist %}
```


**Результат:**

{% list tabs radio %}

- Название радиобаттона 1

  Текст радиобаттона 1.

  Можно вложить еще один перечень радиобаттонов.

  {% list tabs radio %}

  - Вложенный радиобаттон 1

    Текст вложенного радиобаттона

  - Вложенный радиобаттон 2

    Текст вложенного радиобаттона

  {% endlist %}
  

- Название радиобаттона 2

  Текст радиобаттона 2.

{% endlist %}

{% endcut %}



{% note warning %}

Для корректного отображения табов и радиобаттонов соблюдайте отступы:

- отделяйте пустыми строками:

  - `{% list tabs %}` (`{% list tabs radio%}` для радиобаттонов) и `{% endlist %}`;

  - текст одного таба и название следующего таба;

- отступ для содержимого таба - два пробела.

{% endnote %}
