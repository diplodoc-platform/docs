---
title: Local search based on lunr.js
keywords:
    - search
    - lunr
    - solr
    - search
---

# Local search based on lunr.js

### Configuration

```yaml
search:
  provider: local
  tolerance: 2
  confidense: phrased
```

#### confidense

Toggles the mode of additional search result ranking.

`confidense: phrased` - default value. Additionally ranks results by the length of the found phrase.

`confidense: sparsed` - Uses the standard ranking from LunrJS. That is, it simply counts the number of words found in the document, without considering the distance between them.

#### tolerance

Toggles the search query range.

`tolerance: 0` - Searches for exact word matches.

`tolerance: 1` - If there are not enough results with `tolerance=0`, searches for "tails", i.e. `word*`.

`tolerance: 2` - (default) If there are not enough results with `tolerance=1`, searches for "caps", i.e. `*word*`.

### Architecture

LunrJS builds the search index when the documentation is built and searches it synchronously.
This imposes a number of limitations on the system:

#### Size

The search index can be quite large. On average, it takes up three times more space than the volume of textual information in the indexed documents.

Moreover, the index is re-initialized on every new documentation tab (at the moment of focus on the search element).

This can negatively affect the amount of memory used by the browser and the speed of search result initialization.

If the search index exceeds 100Mb, you should consider integrating with another search engine.

You can check the index size in the built documentation directory under `_search/<lang>/index.js`.

#### Synchrony

Because LunrJS has a synchronous implementation, most of its logic is moved to a WebWorker.

WebWorker has [a number of limitations](https://stackoverflow.com/questions/21408510/chrome-cant-load-web-worker) regarding file system access if you open the documentation fully locally (`file:///some-documentation`).

The implementation in Diplodoc tries to work around these limitations, but does not guarantee that everything will work under future browser policies.

### Issues

Report issues with local search to the [issues](https://github.com/diplodoc-platform/search-extension/issues) of the corresponding project.
