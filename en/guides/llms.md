# Generating llms.txt

##llms.txt## is a special Markdown text file placed in the site root and used by AI systems for improved page navigation. Its main purpose is to help correctly understand the site's structure and meaning, highlight key information, and interpret it correctly when generating responses.

##llms-full.txt## is a special Markdown text file placed in the site root that contains the full text content of all site pages for quick content retrieval by AI systems.

Diplodoc supports generating ##llms.txt## and ##llms-full.txt## files for documentation: you need to add the [`llms: enabled: true`](../settings.md#llms) parameter to `.yfm` or run the build with the `--llms` parameter.

Structure of the generated ##llms.txt## file:

```markdown
# Название проекта

> Содержимое поля `llms: description` из файла .yfm

## Documentation

- [Заголовок статьи 1](ссылка-на-статью-1)
- [Заголовок статьи 2](ссылка-на-статью-2): содержимое поля description из метаданных статьи 2
- [Заголовок статьи 3](ссылка-на-статью-3): содержимое поля description из метаданных статьи 3
...

---

For more comprehensive documentation, see [llms-full.txt](llms-full.txt)
```

Features:

- for each ##toc.yaml##, a separate pair of ##llms.txt## / ##llms-full.txt## files is generated;
- the `llms: description` field from `.yfm` is added as the project description;
- the description of each article's content for ##llms.txt## is taken from the [##description## field in the page metadata](../project/meta.md#description);
- in ##llms-full.txt##, to reduce file size, `<style>` and `<script>` tags are stripped along with all their content, and svg images are not inlined.

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
