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
* `build` — `startedAt`, `finishedAt`, `durationMs`, a coarse phase split `phasesMs.{prepare, entries, finalize}` derived from `Entry`-hook timestamps, plus `outputFormat`, `langs`, `inputDir`, `outputDir`, `configHash` (sha256 over a stably-serialized config), `features` (enabled boolean flags) and `worker.maxOldSpace`.
* `counters` — `tocs`, `entriesPlanned` / `entriesProcessed`, breakdowns `entriesByExtension` and `entriesByLang`, `headings` and `contentBytes` (for markdown entries), plus `graph.{entries, sources, resources, missed, edges}` — a snapshot of the dependency graph: pages, included files, assets, missing paths and total edge count.
* `output` — `files`, `totalBytes`, `bytesByExtension`, `largestFile`.
* `schemaVersion` — format version. Additive changes keep the schema backward compatible; breaking changes will bump this number.

Example output:

```json
{
  "schemaVersion": 1,
  "cli": { "version": "5.29.0", "node": "v22.22.0", "platform": "darwin", "arch": "arm64" },
  "build": {
    "durationMs": 990,
    "phasesMs": { "prepare": 951, "entries": 16, "finalize": 23 },
    "outputFormat": "html",
    "langs": ["en", "ru"],
    "configHash": "6a5891269cbab2b5",
    "features": ["addAlternateMeta", "allowHtml", "buildStats", "sanitizeHtml"]
  },
  "counters": {
    "tocs": 3,
    "entriesPlanned": 130,
    "entriesProcessed": 130,
    "entriesByExtension": { ".md": 119, ".yaml": 11 },
    "entriesByLang": { "ru": 88, "en": 42 },
    "headings": 338,
    "contentBytes": 1596875,
    "graph": { "entries": 128, "sources": 11, "resources": 69, "missed": 0, "edges": 118 },
    "warnings": 0,
    "errors": 0
  },
  "output": {
    "files": 403,
    "totalBytes": 42513143,
    "largestFile": { "path": "ru/_images/highload.png", "bytes": 5436055 }
  }
}
```

Typical use cases:

* track `durationMs` and `phasesMs` across builds to catch slowdowns;
* monitor `output.totalBytes` and `output.largestFile` to spot accidentally committed heavy assets;
* fail CI on `counters.graph.missed > 0` or `counters.errors > 0` as a broken-build signal;
* keep `build.configHash` alongside published artifacts so you know which exact config produced them.
