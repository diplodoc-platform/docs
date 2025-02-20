# Cuts and tabs

With YFM extensions, you can use interactive markup elements: cuts and tabs.

{% note info %}

The content of cuts and tabs can include any YFM markup.

{% endnote %}

## Cuts {#cuts}

Use cuts to hide content. For example, additional information or long blocks of code.

```markdown
{% cut "Cut header" %}

Content displayed when clicked.

{% endcut %}
```

**Result**

{% cut "Cut header" %}

Content displayed when clicked.

{% endcut %}

## Tabs {#tabs}

Use tabs for mutually exclusive sections. For example, to separate instructions for different operating systems.

To ensure tabs are displayed correctly, separate each tab list and the text within the tabs with empty lines:

* Use `{% list tabs %}` to start a tab list and `{% endlist %}` to end it.
* Place the text for one tab followed by the name of the next tab on a new line.

### Example of Grouped Tabs

```markdown
{% list tabs group=instructions %}

- Name of tab1

  First step of tab1.
  * You can use lists.
  * And **other** markup.

- Name of tab2

  First step of tab2.

{% endlist %}

Description...

{% list tabs group=instructions %}

- Name of tab1

  Second step of tab1.

- Name of tab2

  Second step of tab2.
  
  {% note info %}

  Try reloading the page to see that Tab 2 is active.

  {% endnote %}

{% endlist %}
```

**Result**

{% list tabs group=instructions %}

- Name of tab1

  First step of tab1.
  * You can use lists.
  * And **other** markup.

- Name of tab2

  First step of tab2.

{% endlist %}

Description...

{% list tabs group=instructions %}

- Name of tab1

  Second step of tab1.

- Name of tab2

  Second step of Tab 2.

  {% note info %}

  Try reloading the page to see that Tab 2 is active.

  {% endnote %}



{% endlist %}

{% endcut %}

