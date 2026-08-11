# Source Docs

You can include documentation in the [Source Docs](https://github.com/SourceDocs/SourceDocs) format in the main document.

{% note alert %}

The sourcedocs includer is being deprecated in favor of the [generic includer](generic.md).

{% endnote %}

#### Usage example

The documentation project is located in the `doc_root` folder.

Let's put the result of running Source Docs into the `doc_root/docs` folder.

Include it in the documentation inside `doc_root/toc.yaml` by specifying `includer` sourcedocs.

Add a link to the generated index page in the main document in `doc_root/index.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: docs
      includer: sourcedocs
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs
    href: docs/
```