# Common parameters

## Synchronization {#group}

Tabs, radio buttons, accordions, and dropdowns support synchronization — switching identical elements on the page. To do this, use the `group` attribute. 

The selected element is remembered and automatically opens on all pages of the documentation project with the same `group` value. For example, by selecting the **MacOS** tab on one page, the user will see it active on all pages. The state of interactive elements is preserved after the page is reloaded.

### Examples

{% list tabs %}

- Tabs

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

  **Result:**

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


- Radio buttons

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

  **Result:**

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


- Accordion

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

  **Result:**

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


- Dropdown

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

  **Result:**

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


## Default element {#selected}

If you need the element to be expanded by default, add the `{selected}` attribute to it.

### Examples

{% list tabs %}

- Tabs

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

  **Result:**

  {% list tabs %}

  - Tab 1 title

    Tab 1 text.

  - Tab name 2 {selected}

    The item will be open by default.

  - Tab name 3

    Tab 3 text.

  {% endlist %}


- Radio buttons

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

  **Result:**

  {% list tabs radio %}

  - Name of item 1

    Text.

  - Item name 2 {selected}

    The item will be open by default.

  - Item name 3

    Text.

  {% endlist %}
  
- Accordion

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

  **Result:**

  {% list tabs accordion %}

  - Name of item 1

    Content for item 1.

  - Item name 2 {selected}

    The item will be open by default.
  
  - Item name 3

    Content for item 3.

  {% endlist %}


- Dropdown

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

  **Result:**

  {% list tabs dropdown %}

  - Name of item 1

    Content for item 1.

  - Item name 2 {selected}

    The item will be open by default.

  - Item name 3

    Content for item 3.

  {% endlist %}


{% endlist %}

## Links to active elements {#link}

The selected element is saved in the URL as the `?tab=name_value` parameter, allowing you to share a direct link to it.
