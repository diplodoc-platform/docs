# Общие параметры

## Синхронизация {#group}

Табы, радиобаттоны, аккордеоны и дропдауны поддерживают синхронизацию — переключение одинаковых элементов на странице. Для этого используйте атрибут `group`. 

Выбранный элемент запоминается и автоматически открывается на всех страницах документационного проекта с тем же значением `group`. Например, выбрав таб **MacOS** на одной странице, пользователь увидит его активным на всех страницах. Состояние интерактивных элементов сохраняется после перезагрузки страницы.

### Примеры

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

  {% list tabs group=instructions_tabs %}

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


  {% list tabs group=instructions_tabs %}

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

  {% list tabs radio group=instructions_radio %}

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



  {% list tabs radio group=instructions_radio %}

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


- Аккордеон

  ```markdown
  
  {% list tabs accordion group=instructions %}

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



  {% list tabs accordion group=instructions %}

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

  {% list tabs accordion group=instructions_accordion %}

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



  {% list tabs accordion group=instructions_accordion %}

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


- Дропдаун

  ```markdown
  
  {% list tabs dropdown group=instructions %}

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



  {% list tabs dropdown group=instructions %}

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

  {% list tabs dropdown group=instructions_dropdown %}

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



  {% list tabs dropdown group=instructions_dropdown %}

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


## Элемент по умолчанию {#selected}

Если нужно, чтобы элемент был раскрыт по умолчанию, добавьте к нему атрибут `{selected}`.

### Примеры

{% list tabs %}

- Табы

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


- Радиобаттоны

  ```markdown
  {% list tabs radio %}

  - Название пункта 1

    Текст.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.

  - Название пункта 3

    Текст.

  {% endlist %}
  ```

  **Результат:**

  {% list tabs radio %}

  - Название пункта 1

    Текст.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.

  - Название пункта 3

    Текст.

  {% endlist %}
  
- Аккордеон

  ```markdown
  {% list tabs accordion %}

  - Название пункта 1

    Контент для пункта 1.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.
  
  - Название пункта 3

    Контент для пункта 3.

  {% endlist %}
  ```

  **Результат:**

  {% list tabs accordion %}

  - Название пункта 1

    Контент для пункта 1.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.
  
  - Название пункта 3

    Контент для пункта 3.

  {% endlist %}


- Дропдаун

  ```markdown
  {% list tabs dropdown %}

  - Название пункта 1

    Контент для пункта 1.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.

  - Название пункта 3

    Контент для пункта 3.

  {% endlist %}
  ```

  **Результат:**

  {% list tabs dropdown %}

  - Название пункта 1

    Контент для пункта 1.

  - Название пункта 2 {selected}

    Пункт будет открыт по умолчанию.

  - Название пункта 3

    Контент для пункта 3.

  {% endlist %}


{% endlist %}

