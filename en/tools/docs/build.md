# Build

The [package](https://www.npmjs.com/package/@diplodoc/cli) provides the `yfm` CLI command.

## HTML {#html}

Default output format of the builder is html

To start rendering, run the command specifying the required [startup keys](settings.md):

* `--input, -i`: The path to the project folder.
* `--output, -o`: The path to the folder for output data (static HTMLs).

```shell script
yfm -i ./input-folder -o ./output-folder
```

## YFM {#yfm}

You can choose to build project in YFM.

To do this, when executing the `yfm` command, specify the startup key `--output-format=md`.

Building in YFM allows you to use:

* [Inserts](../../project/toc.md#includes) and [section visibility conditions](../../project/toc.md#when) in tables of contents files.
* [Content visibility conditions](../../syntax/vars.md#conditions) on document pages.
* [Variable substitutions](../../syntax/vars.md#subtitudes) if the `apply-presets` parameter is specified.

Use this type of build to support multiple document versions for different users. For example, if there are sections with internal information in the documentation, you can keep two repositories: private and public, and synchronize private with public using conditions.

## Build stats {#build-stats}

When started with [`--build-stats`](settings.md) (or `buildStats: true` in the [configuration file](../../project/config.md)), a `yfm-build-stats.json` file is written next to the output with metrics for the current build. The file is intended for CI dashboards, regression tracking and diagnostics — runtime doesn't need it.

Enabled by default for `--output-format=md` builds; disabled for other formats. Pass `--no-build-stats` (or set `buildStats: false` in the configuration file) to opt out.

What goes in:

* `cli` — package version, Node version, platform, architecture, OS release.
* `build` — `startedAt`, `finishedAt`, `durationMs`, a coarse phase split `phasesMs.{prepare, entries, finalize}` derived from `Entry`-hook timestamps, plus `outputFormat`, `langs`, `inputDir`, `outputDir`, `features` (enabled boolean flags), `memoryUsageMb` (`heapUsed` snapshot at finish, in MB) and `worker.maxOldSpace`.
* `counters` — `tocs`, `entriesPlanned` / `entriesProcessed`, breakdowns `entriesByExtension` and `entriesByLang`, `headings` and `contentBytes` (for markdown entries), `graph.{entries, sources, resources, missed, edges}` — a snapshot of the dependency graph (pages, included files, assets, missing paths and total edge count), plus `warnings` / `errors` (totals) and `warningsByCode` / `errorsByCode` — per-YFM-code breakdown (`YFM013`, `YFM016`, etc.); messages without a recognizable code fall into the `(uncoded)` bucket.
* `output` — `files`, `totalBytes`, `bytesByExtension`.
* `schemaVersion` — format version. Additive changes keep the schema backward compatible; breaking changes will bump this number.

Example output:

```json
{
  "schemaVersion": 1,
  "cli": { "version": "5.29.0", "node": "v22.22.0", "platform": "darwin", "arch": "arm64" },
  "build": {
    "durationMs": 1474,
    "phasesMs": { "prepare": 1242, "entries": 148, "finalize": 84 },
    "outputFormat": "html",
    "langs": ["ru", "en"],
    "features": ["addAlternateMeta", "allowHtml", "buildStats", "sanitizeHtml"],
    "memoryUsageMb": 256
  },
  "counters": {
    "tocs": 3,
    "entriesPlanned": 133,
    "entriesProcessed": 133,
    "entriesByExtension": { ".md": 122, ".yaml": 11 },
    "entriesByLang": { "ru": 91, "en": 42 },
    "headings": 345,
    "contentBytes": 1693771,
    "graph": { "entries": 130, "sources": 12, "resources": 74, "missed": 0, "edges": 129 },
    "warnings": 3,
    "errors": 1,
    "warningsByCode": { "YFM013": 2, "(uncoded)": 1 },
    "errorsByCode": { "YFM016": 1 }
  },
  "output": {
    "files": 421,
    "totalBytes": 45350699,
    "bytesByExtension": { ".html": 2865454, ".js": 9721257, ".png": 24588860 }
  }
}
```

## Build content map {#build-content}

When started with [`--build-content`](settings.md) (or `buildContent: true` in the [configuration file](../../project/config.md)), a `yfm-build-content.json` file is written next to the output with a content fingerprint for every output page and asset. The file is intended for offline tools that compare two builds and need to know exactly which pages changed — search reindexing, change notifications and similar consumers. It is not needed at runtime.

Enabled by default for `--output-format=md` builds; disabled for other formats. Pass `--no-build-content` (or set `buildContent: false` in the configuration file) to opt out.

The build itself doesn't know about other revisions and doesn't perform incremental builds: the diff is a post-process over two manifest files.

What goes in:

* `schemaVersion` — format version. Additive changes keep the schema backward compatible; breaking changes will bump this number.
* `contentHashes` — map keyed by **source-path** (stable across builds; output-paths can shift due to `hashIncludes`). For each file: `hash` (sha256 of a content-stable view of the file in output, prefixed with `sha256-`) and `size` (byte size in output). The content-stable view strips VCS-injected fields (`updatedAt`, `contributors`, `author`) and the CLI-injected `metadata.generator` from `.md` frontmatter and `.yaml` `meta:` blocks before hashing, so the hash reflects what readers see rather than every commit or CLI release. Binary assets are hashed as raw bytes.
* `pageAssets` — for every entry, the sorted list of its direct `resource`-type dependencies (images, videos, SVGs, etc.), normalized to source-paths. Required because asset references aren't fingerprinted in the entry's body — a change to `pic.png` doesn't change the entry's hash, but it changes `contentHashes["pic.png"]`, and `pageAssets` lets the consumer connect the two.

How include changes show up in the diff:

* `mergeIncludes: true` — include content is embedded inline, so its bytes flow into the entry's hash. The include file isn't written to output and isn't present in `contentHashes`.
* `mergeIncludes: false`, `hashIncludes: true` (the default) — the entry references the include via a signed filename `inc-{12hex}.md`. A change to the include changes its hash and renames it, which changes the reference in the entry, which changes the entry's hash.

Diff algorithm (consumer side):

```
changed_pages = {
  p ∈ entries(curr) |
       prev.contentHashes[p]?.hash ≠ curr.contentHashes[p]?.hash
    OR ∃ a ∈ curr.pageAssets[p]:
         prev.contentHashes[a]?.hash ≠ curr.contentHashes[a]?.hash
}

added_pages   = keys(curr.contentHashes) \ keys(prev.contentHashes)
removed_pages = keys(prev.contentHashes) \ keys(curr.contentHashes)
```

Example output:

```json
{
  "schemaVersion": 1,
  "contentHashes": {
    "en/foo.md": { "hash": "sha256-...", "size": 1234 },
    "en/foo/inc.md": { "hash": "sha256-...", "size": 567 },
    "en/img/pic.png": { "hash": "sha256-...", "size": 8901 }
  },
  "pageAssets": {
    "en/foo.md": ["en/img/pic.png"]
  }
}
```

### Known limitations

A few cases where keys in `contentHashes` can drift or be noisy independently of user-doc content changes. None block the primary use cases (search reindex, change notifications), but consumers should be aware of them:

* `_bundle/*` — the `output-html` pipeline copies CLI-bundled JS/CSS chunks under `_bundle/`, and the hash baked into those filenames shifts on every `@diplodoc/cli` upgrade. Consumers comparing builds should filter out keys starting with `_bundle/`.
* `_search/*` — when local search is enabled, `LocalSearchProvider` writes resources at `_search/<lang>/{timeOrigin}-resources.js`, where `{timeOrigin}` is the build start time. Every build produces a new filename and a new key. Consumers should filter `_search/` or accept the churn.
* `mergeSvg: true` (default) — an SVG referenced as `![](logo.svg)` is inlined into the entry's body *and* kept as a standalone file in output. A change to the SVG flips three signals at once: the entry's hash, the standalone `.svg`'s hash, and the entry through `pageAssets`. To avoid the double-counting, reference SVGs with `{inline=false}`.
