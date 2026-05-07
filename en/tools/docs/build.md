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

What goes in:

* `cli` — package version, Node version, platform, architecture, OS release.
* `build` — `startedAt`, `finishedAt`, `durationMs`, a coarse phase split `phasesMs.{prepare, entries, finalize}` derived from `Entry`-hook timestamps, plus `outputFormat`, `langs`, `inputDir`, `outputDir`, `features` (enabled boolean flags), `memoryUsageMb` (`heapUsed` snapshot at finish, in MB) and `worker.maxOldSpace`.
* `counters` — `tocs`, `entriesPlanned` / `entriesProcessed`, breakdowns `entriesByExtension` and `entriesByLang`, `headings` and `contentBytes` (for markdown entries), plus `graph.{entries, sources, resources, missed, edges}` — a snapshot of the dependency graph: pages, included files, assets, missing paths and total edge count.
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
    "warnings": 0,
    "errors": 0
  },
  "output": {
    "files": 421,
    "totalBytes": 45350699,
    "bytesByExtension": { ".html": 2865454, ".js": 9721257, ".png": 24588860 }
  }
}
```

Typical use cases:

* track `durationMs`, `phasesMs` and `memoryUsageMb` across builds to catch slowdowns and memory regressions;
* monitor `output.totalBytes` and `output.bytesByExtension` to spot accidentally committed heavy assets;
* fail CI on `counters.graph.missed > 0` or `counters.errors > 0` as a broken-build signal;
* compare `counters.entriesPlanned` against `counters.entriesProcessed` — a mismatch means some pages failed mid-build.
