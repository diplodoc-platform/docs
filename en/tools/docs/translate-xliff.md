---
keywords: ['translate', 'xliff', 'cat', 'extract', 'compose', 'trados', 'smartcat', 'crowdin']
---
# XLIFF exchange with CAT tools

When translation is done by people - in-house translators or an agency - they usually work in a Computer Assisted Translation (CAT) tool: Trados, Phrase, Smartcat, Crowdin, and the like. The standard exchange format for such tools is [XLIFF](https://en.wikipedia.org/wiki/XLIFF).

The `extract` and `compose` subcommands of the `{{PROGRAM}} translate` command implement the full cycle of such translation:

1. `extract` exports the translatable project text into `*.xliff` files.
2. The files are translated in a CAT tool.
3. `compose` assembles the translated `*.xliff` back into documentation files.

## How it works {#how-it-works}

`extract` splits each documentation file into two parts:

* `<file>.xliff` - translatable segments: sentences, headings, table cells;
* `<file>.skl` - the skeleton: the source file with markers in place of the segments.

Markup, code, and Liquid constructs stay in the skeleton and never reach the CAT tool - see [How translation works](translate.md#pipeline) for details.

Both files are saved under the target language path. For example, when translating from `ru` into `en`, the file `ru/guide/index.md` produces `en/guide/index.md.xliff` and `en/guide/index.md.skl`.

`compose` performs the reverse operation: it finds `.xliff` + `.skl` pairs in a directory and assembles a translated file from each - `en/guide/index.md`. Files without a pair are skipped with a warning.

## Full cycle example {#example}

```bash
# Export segments: en/**/*.xliff and en/**/*.skl appear in ./xliff
{{PROGRAM}} translate extract -i ./docs -o ./xliff --source ru --target en

# ...translate *.xliff in a CAT tool...

# Assemble translated files into ./docs/en
{{PROGRAM}} translate compose -i ./xliff -o ./docs
```

Only the `*.xliff` files are handed over to the CAT tool, but during assembly the translated `*.xliff` must sit next to their `*.skl` - don't delete the skeletons between steps.

After `compose`, the translated version is built with a regular `{{PROGRAM}} build`.

## XLIFF format {#format}

`extract` produces XLIFF version 1.2. Each segment is a `<trans-unit>` element with the source text in `<source>`. The translation must go into the `<target>` element - CAT tools add it themselves:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xliff xmlns="urn:oasis:names:tc:xliff:document:1.2" version="1.2">
  <file original="file.ext" source-language="ru-RU" target-language="en-US" datatype="markdown">
    <header>
      <skeleton>
        <external-file href="file.skl"></external-file>
      </skeleton>
    </header>
    <body>
      <trans-unit id="1">
        <source xml:space="preserve" xml:lang="ru-RU">Document title</source>
      </trans-unit>
    </body>
  </file>
</xliff>
```

Inline markup inside a segment - emphasis, links, code - is encoded with the auxiliary `<g>` and `<x/>` tags. They must be preserved during translation: `compose` uses them to restore the original markup.

## extract parameters {#extract}

#|
|| **Parameter** | **Description** ||
|| `--source`, `-sl` |
Source language in ISO 639-1 format: `ru` or `ru-RU`. Required
||
|| `--target`, `-tl` |
Target language: `en` or `en-US`. Can be passed multiple times - the export is performed for each language
||
|| `--filter` |
Export only files reachable from `toc.yaml`. By default, all project files are exported
||
|| `--schema` |
Paths to files with custom [translation schemas](translate.md#json-schemas) for YAML and JSON. Several paths can be specified
||
|| `--no-ref-resolve` |
Do not resolve `$ref` in OpenAPI specifications during export
||
|#

The common parameters `--input`, `--output`, `--files`, `--include`, and `--exclude` are also supported - see [Localization](translate.md#options).

## compose parameters {#compose}

#|
|| **Parameter** | **Description** ||
|| `--input`, `-i` |
Directory with `*.xliff` + `*.skl` pairs. Defaults to the directory the command is run from
||
|| `--output`, `-o` |
Path to the project **root** where the assembled files should be saved. Defaults to `input`
||
|| `--use-source` |
Assemble files from the source text (`<source>`) instead of the translation. Useful for debugging the export
||
|#

The `--include` and `--exclude` parameters filter file pairs the same way as during translation - see [Localization](translate.md#options).
