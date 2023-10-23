# Reusing content

You can put recurring content in a separate file and add it to the necessary places in the document using the construction `{% include %}`.

Reusing content helps reduce the time spent on editing and searching the source text: information is stored in one place, and changes are automatically applied to all files.

## Instructions for reusing content {#steps}

1. Create a folder to store recurring content. For example, `_includes`.

   {% note warning %}

   Images should be stored in a folder whose name starts with `_`. Otherwise, they will be deleted during the build.

   {% endnote %}

1. In the `_includes` folder, create a separate MD file with the recurring text.

1. In sections of a document where you need to insert this text, add a link to the file in the following format:

   ```markdown
   {% include [Description](../_includes/file.md) %}
   ```
    * `[Description]`: File description. Information about document authors does not affect the build.
    * `(_includes/file.md)`: File path.

    If you don't need to add the header of the reusable file to the section, add the `notitle` keyword:

    ```markdown
    {% include notitle [Description](../_includes/file.md) %}
    ```

When building the document, the text of the file is added to the sections in place of the includes. If there are relative links in the file, they are re-assembled.

