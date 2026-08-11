# Content reuse

You can move repeated content to a separate file and add it to the desired places in the document using the `{% include %}` construct.

Reuse will help reduce time spent on editing and searching for source text: information is stored in only one place, and changes are automatically applied to all files.

## Reuse procedure {#steps}

1. Create a directory for storing repeated content. For example, `_includes`.

   {% note warning %}

   Files for reuse must be stored in a directory whose name starts with the `_` character, otherwise they will be deleted during the build.

   {% endnote %}

1. In the `_includes` directory, create a separate md file with the repeated text.

1. In the document sections where you need to insert the text, add a link to the file in the following format:

   ```markdown
   {% include [Описание](../_includes/file.md) %}
   ```

    * `[Description]` — file description. Information for document authors, does not affect the build.
    * `(_includes/file.md)` — path to the file.

    If the header of the file for reuse does not need to be added to the section text, add the `notitle` keyword:

    ```markdown
    {% include notitle [Описание](../_includes/file.md) %}
    ```

During the document build, the file text will be added to the sections at the include locations. If the file contains relative links, they will be rebuilt.

## Reusing part of an article {#include-headers}

You can reuse a separate section of an article by specifying its anchor link in `{% include %}`. The final file will include the section and all subsections of the article.

### Example

The file `file.md` looks like this:

```markdown

## Часть 1
Контент первой части.

## Часть 2 {#part}
Контент второй части.

### Подраздел части 2
Контент подраздела.

## Часть 3
Контент третьей части.

```

Using `{% include [Description](file.md#part) %}` will add the section "Part 2" and its subsection to the article:

```markdown
## Часть 2 {#part}
Контент второй части.

### Подраздел части 2
Контент подраздела.
```

{% note warning %}

Using the `include` construct, you cannot include an article (or parts of an article) into itself.

{% endnote %}
