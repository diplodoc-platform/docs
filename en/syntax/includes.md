# Content reuse

You can move repeating content into a separate file and include it where needed in the document using the `{% include %}` construct.

Reuse helps reduce the time spent on editing and searching for source text: the information is stored in one place only, and changes are automatically applied to all files.

## Reuse Workflow {#steps}

1. Create a directory to store reusable content. For example, `_includes`.

   {% note warning %}

   Files for reuse must be stored in a directory whose name starts with the `_` character, otherwise they will be removed during the build.

   {% endnote %}

1. In the `_includes` directory, create a separate md file with the reusable text.

1. In the sections of the document where you need to insert the text, add a reference to the file in the following format:

   ```markdown
   {% include [Description](../_includes/file.md) %}
   ```

    * `[Description]` — description of the file. Information for document authors; it does not affect the build.
    * `(_includes/file.md)` — path to the file.

    If you do not need to add the title of the reusable file to the section text, add the `notitle` keyword:

    ```markdown
    {% include notitle [Description](../_includes/file.md) %}
    ```

During the document build, the file content will be inserted into the sections at the include locations. If the file contains relative links, they will be rewritten.

## Reusing a Part of an Article {#include-headers}

You can reuse a specific section of an article by specifying its anchor link in `{% include %}`. The resulting file will include the section and all its subsections.

### Example

The file `file.md` looks like this:

```markdown

## Part 1
Content of the first part.

## Part 2 {#part}
Content of the second part.

### Subsection of Part 2
Content of the subsection.

## Part 3
Content of the third part.

```

Using `{% include [Description](file.md#part) %}` will add the "Part 2" section and its subsection to the article:

```markdown
## Part 2 {#part}
Content of the second part.

### Subsection of Part 2
Content of the subsection.
```

{% note warning %}

You cannot use the `include` construct to add an article (or parts of an article) into itself.

{% endnote %}
