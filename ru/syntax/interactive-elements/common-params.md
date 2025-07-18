# Общие параметры

Табы, радиобаттоны, аккордеоны и дропдауны поддерживают синхронизацию. Выбранный элемент запоминается и автоматически открывается на всех страницах документационного проекта с тем же значением `group`. Например, выбрав таб **MacOS** на одной странице, пользователь увидит его активным на всех страницах. Состояние интерактивных элементов сохраняется после перезагрузки страницы.

## Синхронизация

Чтобы синхронизировать переключение одинаковых элементов на странице, используйте атрибут `group`:

{% list tabs %}

- Табы

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


- Радиобаттоны

  ```markdown
  {% list tabs radio group=instructions %}

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



  {% list tabs radio group=instructions %}

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

  {% list tabs radio group=instructions %}

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



  {% list tabs radio group=instructions %}

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



{% endlist %}
