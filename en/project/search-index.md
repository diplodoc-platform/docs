# Search JSON export

Export documentation content as a JSON file for an external search system. The CLI produces a common page snapshot independently of the search provider.

## Enable export

Add `--search-index` to the [build command](../tools/docs/build.md):

```sh
yfm build -i ./docs -o ./build --search-index
```

The result is written to `./build/_search/documents.json`. Export is disabled by default and requires no additional extensions.

Export supports HTML builds without `--watch`. It is independent of the [search settings](./search.md): you can create a snapshot even when search is disabled on the website.

## JSON format

The file contains a format version, `schemaVersion`, and a `documents` array. Each array entry describes one page:

```json
{
  "schemaVersion": 1,
  "documents": [
    {
      "id": "1f2fcdd0ccaac9f9a15f4a73a0d9c00fb787bac300f9959aeca48795d5bcc816",
      "path": "en/guide.md",
      "url": "en/guide.html",
      "lang": "en",
      "title": "Guide",
      "content": "Hello world & friends.",
      "headings": ["Guide"],
      "keywords": ["help"],
      "tags": ["guide"]
    }
  ]
}
```

All page fields are present in the JSON. `headings`, `keywords` and `tags` are arrays of strings and may be empty; the remaining fields are strings.

| Field | Meaning |
| --- | --- |
| `id` | SHA-256 of the source `path`. The ID survives content changes but changes when the file is renamed. |
| `path` | Source file path relative to the project root, using `/` as the directory separator. |
| `url` | HTML page link relative to the published documentation root, respecting `--skip-html-extension`. |
| `lang` | Page language. |
| `title` | Page title without HTML markup. |
| `content` | Resolved page text without navigation, HTML markup, scripts or styles. |
| `headings` | Page title and section headings without duplicates. |
| `keywords` | Page keywords. |
| `tags` | Public tags, excluding values that start with `_`. |

Check `schemaVersion` before processing the file. The `url` field does not contain a host, so the same snapshot can be used at different publication addresses.

## Content and exclusions

The JSON contains text after variable substitution, condition processing and include resolution. Export reflects the documentation variant selected by the build parameters.

Pages marked [`noIndex: true`](./meta.md#no-index) are excluded, including when the restriction is inherited from a section in the [table of contents](./toc.md#no-index). Hidden pages follow the [`search.hiddenPolicy`](../settings.md#search-hidden-policy) rules.

For a landing page without article HTML, export includes its title and metadata description. Its block content is not included in `content`.

## Rebuilds

Each build with `--search-index` replaces the complete snapshot. Documents are sorted by source path. Deleted and excluded pages are absent from the new file; if no eligible pages remain, `documents` is empty.

Documentation processing errors prevent a fresh snapshot from being written. A subsequent HTML build without `--search-index` removes the previously generated snapshot from the output directory. A file with the same name in the documentation input does not override the exported result.
