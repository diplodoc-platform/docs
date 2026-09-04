# Building documentation

The project is built by running `yfm build` with the following parameters:

* `--input, -i` — path to the project directory (by default, the current folder);
* `--output, -o` — path to the output directory (required parameter).

```shell script
# full command
yfm build -i ./input-folder -o ./output-folder

# a shortened form without build is also available
yfm -o ./output-folder
```

The standard output format of the builder is HTML.

The full list of build parameters can be [found in the article](settings.md) or displayed in the console by running `yfm build --help`.

Builds of large projects can be sped up by processing pages in parallel, see [Multithreaded build](multithreading.md).

## YFM → YFM {#yfm}

You can perform an intermediate build from YFM to YFM. To do this, specify the launch flag `--output-format=md` when running the command.

When building to YFM, the following are performed:
* [inserts](../../project/toc-includes.md) and [checks of section visibility conditions](../../project/toc.md#when) in table of contents files;
* [checks of content display conditions](../../syntax/vars.md#conditions) on document pages;
* [variable substitutions](../../syntax/vars.md#subtitudes), if the `apply-presets` parameter is specified;
* [inlining of SVG images](../../syntax/media.md#img-inline);
* [substitution of article titles instead of {#T}](../../syntax/links.md#autotitle);
* [inserts of content from files](../../syntax/includes.md).

Use this type of build to maintain multiple documentation variants for different users. If the documentation contains sections with internal information, you can keep two repositories — private and public, and synchronize the private one to the public one using conditions.

## Watch mode {#watch}

You can automate the rebuild of individual articles when they change. To do this, run `yfm build` with the `--watch` parameter: after the project build, the program will enter incremental rebuild mode and will create or update articles after saving changes in the source documentation files.

For convenience, after rebuilding a file open in the browser, the page is automatically reloaded.

## Build statistics {#build-stats}

When run with the [`--build-stats`](settings.md#build-stats-flag) flag (or `buildStats: true` in the [configuration file](../../settings.md)), a file `yfm-build-stats.json` with metrics of the current build is written next to the output. The file is intended for CI dashboards, regression tracking, and diagnostics — it is not needed for runtime.

By default, it is enabled for builds with `--output-format=md`, and disabled for other formats. To disable it, pass `--no-build-stats` or specify `buildStats: false` in the configuration file.

What goes into the file:

* ``cli` — package version, Node version, platform, architecture, OS release.
* ``build` — `startedAt`, `finishedAt`, `durationMs`, rough phase breakdown `phasesMs.{prepare, entries, finalize}` (based on `Entry` hook timing), `outputFormat`, `langs`, `inputDir`, `outputDir`, `features` (enabled boolean flags), `memoryUsageMb` (`heapUsed` at completion, in MB), `worker.maxOldSpace`.
* ``counters` — `tocs`, `entriesPlanned` / `entriesProcessed`, breakdowns `entriesByExtension` and `entriesByLang`, `headings` and `contentBytes` (for md pages), `graph.{entries, sources, resources, missed, edges}` — a snapshot of the dependency graph (pages, included files, assets, missing paths, edge count), as well as `warnings` / `errors` (total counts) and `warningsByCode` / `errorsByCode` — breakdown by error codes (`YFM013`, `YFM016`, etc.; messages without a recognized code fall into the `(uncoded)` bucket).
* ``output` — `files`, `totalBytes`, `bytesByExtension`.
* ``schemaVersion` — version of the file format. When the format is extended, the schema will remain compatible; breaking changes will increase this number.

Example output file:

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

When run with the `--build-content` flag (or `buildContent: true` in the [configuration file](../../settings.md)), a file `yfm-build-content.json` is written next to the output, containing a fingerprint of the content of each page and asset. The file is intended for external tools that compare two builds and precisely determine the list of changed pages — search reindexing, change notifications, etc. It is not needed for the runtime.

Enabled by default for `--output-format=md` builds, disabled for other formats. To disable, pass `--no-build-content` or specify `buildContent: false` in the configuration file.

The build itself knows nothing about other revisions and does not perform incremental builds: the diff is computed as post-processing of two manifest files.

What goes into the file:

* ``schemaVersion` — version of the file format. When the format is extended, the schema will remain compatible; breaking changes will increase this number.
* `contentHashes — a table whose keys are source paths (stable between builds; output paths may change due to hashIncludes). For each file: hash (sha256 of the stable representation of the file in the output, prefixed with sha256-) and size (file size in the output in bytes). The stable representation is the file with VCS fields (updatedAt, contributors, author) and the CLI field metadata.generator stripped from the frontmatter of .md and the meta: block in .yaml before hashing. This way, the hash reflects what readers see, not every commit or CLI release. Binary assets are hashed as-is.
* `pageAssets — for each page — a sorted list of its direct dependencies of type resource (images, videos, SVG, etc.), reduced to source paths. It is needed because asset links do not have a fingerprint in the page body: changing pic.png does not change the page hash, but changes contentHashes["pic.png"], and pageAssets allows the consumer to link the two.

How changes in includes get into the diff:

* `mergeIncludes: true — the include content is inlined into the page, its bytes are part of the page hash. The include file is not written to the output and is absent from contentHashes.
* `mergeIncludes: false, hashIncludes: true (default) — the page references the include under a signed name inc-{12hex}.md. Changing the include changes its hash and renames it, which changes the link in the page, which changes the page hash.

Diff algorithm (on the consumer side):

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

Example output file:

```json
{
  "schemaVersion": 1,
  "contentHashes": {
    "ru/foo.md": { "hash": "sha256-...", "size": 1234 },
    "ru/foo/inc.md": { "hash": "sha256-...", "size": 567 },
    "ru/img/pic.png": { "hash": "sha256-...", "size": 8901 }
  },
  "pageAssets": {
    "ru/foo.md": ["ru/img/pic.png"]
  }
}
```

### Known limitations

Cases where keys in contentHashes may "jitter" or be noisy regardless of actual content changes. They do not interfere with the main scenarios (search reindexing, change notifications), but it is worth knowing about them:

* `_bundle/* — the output-html pipeline copies CLI JS/CSS chunks to _bundle/, and the hash embedded in these file names shifts with every @diplodoc/cli upgrade. Consumers comparing two builds should filter out keys starting with _bundle/.
* `_search/* — if local search is enabled, LocalSearchProvider writes resources to _search//{timeOrigin}-resources.js, where {timeOrigin} is the build start time. Each build produces a new file name and a new key. It is worth filtering out _search/ or accepting this noise.
* `mergeSvg: true` (default) — SVG referenced as `![](logo.svg)` is inlined into the page body *and* remains a separate file in the output. Changing an SVG triggers three signals at once: the page hash, the hash of an individual `.svg`, and the page via `pageAssets`. To avoid double counting, use `![](logo.svg){inline=false}`.
