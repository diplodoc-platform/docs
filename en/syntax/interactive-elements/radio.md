# Radio buttons

Radio buttons work similarly to tabs. For example, for splitting instructions for different platforms.

```markdown
{% list tabs radio %}

- Название радиобаттона 1

  Текст радиобаттона 1  

- Название радиобаттона 1

  Текст радиобаттона 2

{% endlist %}
```


{% cut "Usage example and result" %}

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


**Result:**

{% list tabs radio %}

- Radio button name 1

  Radio button text 1.

  You can nest another list of radio buttons.

  {% list tabs radio %}

  - Nested radio button 1

    Nested radio button text

  - Nested radio button 2

    Nested radio button text

  {% endlist %}
  

- Radio button name 2

  Radio button text 2.

{% endlist %}

{% endcut %}



{% note warning %}

For correct display of tabs and radio buttons, follow the indentation rules:

- separate with empty lines:

  - `{% list tabs %}` (`{% list tabs radio%}` for radio buttons) and `{% endlist %}`;

  - the text of one tab and the name of the next tab;

- indent for tab content - two spaces.

{% endnote %}

{% include [common-params](../../_includes/common-params-note.md) %}
