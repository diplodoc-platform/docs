# Creating PDF from documentation

Diplodoc can generate documentation in PDF format.

## PDF document structure { #structure }

A PDF document consists of three parts:

1. **Title and closing pages** {#start-pages}

    They are displayed at the beginning and end of the documentation and are not numbered.
    
    Title pages are specified in the `startPages` block in `toc.yaml`:

    ```yaml
    pdf:
      startPages:
        - path-to-page-1.md
        - path-to-page-2.md
        - path-to-page-n.md
    ```

    Closing pages are specified in the `endPages` block in `toc.yaml`:

    ```yaml
    pdf:
      endPages:
        - path-to-page-1.md
        - path-to-page-2.md
        - path-to-page-n.md
    ```

    {% note warning %}

    Pages from `pdf.startPages` and `pdf.endPages` do not support [localization via `yfm translate`](../tools/docs/translate.md).

    {% endnote %}

    When building documentation, title and closing pages are not transformed into files. To check their layout in a browser, use the `--pdf-debug` flag during the build: it will create HTML versions of the pages from `startPages` and `endPages`.

1. **Table of contents**

    Diplodoc automatically generates a table of contents based on `toc.yaml`. Each item in the list is a link to a page.

    Section titles that group a set of articles are displayed as plain text.
    Files with the [`hidden: true` attribute](../project/toc.md#hidden) in `toc.yaml` are not included in the PDF. To include them, set the [`hiddenPolicy: false` parameter](../settings.md#pdf).

1. **Main content**

    All Diplodoc features are supported in PDF:

    - Page Constructor blocks;
    - cross-references;
    - images and other media files.

    Each subsequent article of the PDF document starts on a new page. Articles in the PDF are arranged in the same order as in the table of contents.

## Build { #build }

### Setup

1. [Install the `@diplodoc/pdf-generator` package](../settings.md#pdf).

1. In the `toc.yaml` file, add the `startPages` section to generate [title pages](#start-pages).

1. Enable PDF support in the `.yfm` configuration file:

    ```yaml
    pdf:
      enabled: true
    ```

### Generation

1. Build the documentation project:

    ```bash
    yfm build -i . -o ./docs-output --pdf
    ```

    - ``-i .` — path to the folder with sources (in the example, the current folder);
    - ``-o ./docs-output` — path to the folder for build results;
    - ``--pdf` — flag that enables data preparation for PDF generation; if PDF support is enabled in `.yfm`, the flag does not need to be passed.

1. Run the PDF generator:

    ```bash
    npx -- @diplodoc/pdf-generator@latest -i ./docs-output
    ```

{% note info %}

For each `toc.yaml` file, Diplodoc creates a separate `single-page.pdf`. 

{% endnote %}

## Styling { #styles }

You can change the appearance of the PDF document using [CSS styles](../style/css-js.md).

{% note alert %}

Diplodoc removes styles added inside Markdown files during PDF generation — this is done for security purposes.

{% endnote %}

## Content filtering { #filtering }

To show or hide elements only in the PDF version, use [presets](../project/presets.md).

1. Add the required variable to `presets.yaml`:

    ```yaml
    pdf:
      version: pdf
    ```

2. Use the condition in the text:

    ```markdown
    {% if version == "pdf" %}

    Этот текст появится только в PDF-версии.

    {% endif %}
    ```
