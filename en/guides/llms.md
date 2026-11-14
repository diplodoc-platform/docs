# Generating llms.txt

##llms.txt## is a special Markdown text file placed in the site root and used by AI systems for improved page navigation. Its main purpose is to help correctly understand the site's structure and meaning, highlight key information, and interpret it correctly when generating responses.

##llms-full.txt## is a special Markdown text file placed in the site root that contains the full text content of all site pages for quick content retrieval by AI systems.

Diplodoc supports generating ##llms.txt## and ##llms-full.txt## files for documentation: you need to add the [`llms: enabled: true`](../settings.md#llms) parameter to `.yfm` or run the build with the `--llms` parameter.

Structure of the generated ##llms.txt## file:

```markdown
# Project title

> Description from llms.description

Additional information from llms.details.

## Documentation

- [Article 1 title](article-1-link)
- [Article 2 title](article-2-link): description from article 2 metadata
- [Article 3 title](article-3-link): description from article 3 metadata
...

---

For more comprehensive documentation, see [llms-full.txt](llms-full.txt)
```

Features:

- for each ##toc.yaml##, a separate pair of ##llms.txt## / ##llms-full.txt## files is generated;
- `llms.description` from `toc.yaml` is added as the project description; if omitted, the value from `.yfm` is used;
- `llms.details` adds Markdown paragraphs and lists after the description and before `## Documentation`; these details are not added to ##llms-full.txt##;
- the description of each article's content for ##llms.txt## is taken from the [##description## field in the page metadata](../project/meta.md#description);
- in ##llms-full.txt##, to reduce file size, `<style>` and `<script>` tags are stripped along with all their content, and svg images are not inlined.

The link text for an article in ##llms.txt## is selected from the first non-empty value in the following order:

1. The `title` field in the [article metadata](../project/meta.md) (`meta.title`). In a Markdown file, set it at the beginning of the file between `---` lines.
2. The first level-one heading (H1) in the article. It is determined after variable substitution and [include](../syntax/includes.md) expansion, respecting content visibility for human readers. For a [leading page](../project/leading-page.md), the page's own `title` field is used.
3. The `name` field of the corresponding item in the [`toc.yaml` table of contents](../project/toc.md).

Values containing only whitespace are skipped. If none of these values is set, the article's metadata `description` is used, followed by the path from the TOC item's `href`.

## Per-TOC settings {#toc-metadata}

Set project-wide defaults for all tables of contents in `.yfm`:

```yaml
llms:
  enabled: true
  description: Product documentation.
  details: |
    Start with the installation guide.

    - Examples assume the latest product version.
  url: https://example.com/llms.txt
```

Override `description`, `details`, and `url` at the root of each [`toc.yaml`](../project/toc.md#structure). For example, in `en/toc.yaml`:

```yaml
title: English documentation
llms:
  description: Guides and API reference in English.
  details: |
    Read the guide before using the API reference.
  url: https://example.com/en/llms.txt
items:
  - name: Getting started
    href: index.md
```

`description` is the short summary at the beginning of ##llms.txt##. `details` is additional Markdown content. These are free-form paragraphs and lists before the link sections, rather than a separate `## Optional` section.

Each field is resolved independently:

- An omitted field in `toc.yaml` uses the corresponding value from `.yfm`. For example, you can set only the English description and keep the project-wide `details` and `url`.
- An empty string in `description: ''` or `details: ''` removes that text, even when `.yfm` provides a default.
- An empty string in `url: ''` clears the project-wide URL. When generation is enabled, pages link to the ##llms.txt## for their own TOC. When generation is disabled, no link is added.

Use an absolute URL or an empty string for `url`. All three fields accept strings only. Generation enablement (`enabled`) and the size limit (`llmsFullMaxSize`) can only be set in `.yfm` or build command options.

A separate nested TOC uses its own settings and `.yfm` defaults without inheriting its parent TOC's settings. A TOC connected through an [include](../project/toc-includes.md) contributes entries to the containing TOC without overriding its LLMS settings.

The nearest TOC determines a page's `llms.url`. The link is added to the article's Markdown companion and to the static HTML build as `rel="describedby"`. The `description` and `details` fields in `toc.yaml` are also extracted for [translation](../tools/docs/translate.md) as Markdown; the URL is not translated.

When building with `--watch`, changes to these fields in `toc.yaml` take effect without restarting. Summary or details changes update ##llms.txt##; URL changes update links on affected pages. Restart the build after changing `.yfm`.

## Limiting the size of llms-full.txt {#llms-full-max-size}

For projects with many articles, the ##llms-full.txt## file may become too large for AI systems to read. To set the maximum allowed size of the generated file, you can specify a limit in the [`llms: llmsFullMaxSize`](../settings.md#llms) parameter in `.yfm`.

The parameter is processed as follows: if adding the next article to ##llms-full.txt## causes the final file size to exceed the specified limit, filling of ##llms-full.txt## stops and build code ##YFM022## is returned (level **INFO**, can be [overridden via yfmlint](../project/lint.md)).

## Connecting an external llms.txt {#external}

If the documentation is part of a site that already has its own ##llms.txt## file, you can specify a link to it in the documentation articles using the `llms: url` parameter:

```yaml
llms:
  url: https://example.com/llms.txt
```

Important: to specify an external file, it is **not necessary** to enable ##llms.txt## generation in the documentation.

You can [override the link per TOC](#toc-metadata) with `llms.url` in `toc.yaml`. This override also works when generation is disabled.
