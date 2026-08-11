---
title: Search with Algolia
---

# Search with Algolia

[Algolia](https://www.algolia.com/) is an external cloud-based search engine for working with large volumes of data. Integrates with the Diplodoc documentation frontend.

**Source code and additional instructions for the Algolia extension:**
[https://github.com/diplodoc-platform/algolia-extension](https://github.com/diplodoc-platform/algolia-extension)

> A VPN may be required to register an Algolia account.

## Quick start

1. **Register with Algolia**  
   Go to [algolia.com](https://www.algolia.com/) and create an account. After that, obtain the App ID, Write API Key, and Search API Key for your application.  
   _(For details, see the section [“Algolia registration and settings”](#registraciya-i-nastrojki-algolia))_

2. **Install the Diplodoc CLI and the Algolia extension (globally)**  
   ```bash
   npm install -g @diplodoc/cli
   npm install -g @diplodoc/algolia-extension
   ```
   _(For more details on installation options, see the section [“Installation”](#ustanovka))_

3. **Configure search in `.yfm`**  
   In the root `.yfm`, specify:
   ```yaml
   search:
     provider: algolia
     appId: <your app id>
     searchApiKey: <your search key>
     index: true
   ```
   _(For an example with advanced settings, see [“Example of advanced settings”](#primer-rasshirennoj-nastrojki))_

4. **Pass the keys and run the build**  
   For a secure build, pass the Write API Key via the CLI flag:
   ```bash
   yfm build -i ./docs -o ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
   ```

### Algolia registration and settings

1. Register at [algolia.com](https://www.algolia.com/) (a VPN may be required).
2. In the Algolia panel, create an application and obtain:
   - **App ID** ― application identifier
   - **Write API Key** ― secret key for data indexing
   - **Search API Key** ― key for client-side search
3. The index name (`indexName`) can be left unset; by default it is `"docs"`.

### Installation

There are two ways to install the Algolia search extension:

- **Global installation** — suitable for most typical scenarios if you simply want to build documentation with cloud search support.
- **Local installation in the repository** — recommended if you use custom plugins, modify the CLI, or work in a team with a shared package.json.

**Global installation:**
```bash
npm install -g @diplodoc/cli
npm install -g @diplodoc/algolia-extension
```
Running the build with the extension:
```bash
yfm build -i ./docs -o ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
```

**Local installation in the @diplodoc/cli project:**
```bash
npm install @diplodoc/algolia-extension
```
Running the build with the extension:
```bash
npm start -- -i ./docs -o ./docs-out --extensions @diplodoc/algolia-extension --api-key "your-write-key"
```

### Sources for passing parameters

Extension parameters can be set via the CLI, environment variables, and the `.yfm` file:

| Parameter      | CLI flag            | Environment variable       | .yfm                       | Purpose                               |
|---------------|---------------------|------------------------|----------------------------|------------------------------------------|
| `provider`      | `--search-provider`   | ALGOLIA_PROVIDER       | `search.provider`            | Search provider (`algolia`)             |
| `appId`         | `--app-id`            | ALGOLIA_APP_ID         | `search.appId`               | Algolia App ID                           |
| `apiKey`        | `--api-key`           | ALGOLIA_API_KEY        | `search.apiKey`   | Secret key for indexing            |
| `indexName`     | `--index-name`        | ALGOLIA_INDEX_NAME     | `search.indexName`           | Index name (default "docs")        |
| `index`         | `--index`             | -                      | `search.index`               | Whether to upload the index to Algolia            |
| `searchApiKey`  | `--search-api-key`    | ALGOLIA_SEARCH_API_KEY | `search.searchApiKey`        | Client-side search key               |
| `api`           | `--search-api`        | ALGOLIA_API_PATH       | `search.api`                 | Path to the JS search API                     |
| `indexSettings` | -                   | -                      | `search.indexSettings`       | Algolia index settings                |
| `querySettings` | -                   | -                      | `search.querySettings`       | Search query settings             |


{% note warning "Explanation of key types" %}

- **apiKey (Write API Key):**
  Secret key used to upload and update data in Algolia during build or indexing. Keep it secret, do not publish it in repositories or exposed configuration files: use environment variables or CLI flags.

- **searchApiKey (Search API Key):**
  Key for frontend search, included in the final documentation build. Without it, client-side search will not work. This key is safe to publish in the `.yfm` file.

{% endnote %}

### Example of advanced configuration

```yaml
search:
  provider: algolia
  appId: <your app id>
  indexName: docs
  index: true
  searchApiKey: <your search api key>
  indexSettings:
    searchableAttributes:
      - title
      - content
      - headings
      - keywords
    attributesToHighlight:
      - title
      - content
  querySettings:
    hitsPerPage: 10
    attributesToRetrieve:
      - title
      - content
      - url
      - section
```

### Build and indexing

- By default, the extension creates local indexes in the `_search` directory of your output folder. These indexes are available for local search and are not uploaded to the cloud.
- If the config specifies the `index: true` parameter (or the CLI flag `--index` is used), then with each documentation build the index will not only be generated locally but also automatically uploaded (updated) to Algolia after the build.
- If you want to separate these processes — for example, build the documentation first, verify the result, and upload the index only after final verification or separately on a schedule — configure the build without the `index` parameter (or explicitly with `index: false`). Then only local indexes are created during the build. Later, to upload or update the index to the cloud, use a separate command:

```bash
yfm index -i ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
```

#### Frequently asked questions and issues

- Search does not work — check that `searchApiKey` is correctly passed in the config.
- Indexing error — check the correctness and method of passing the `write apiKey`.
- Data does not appear in Algolia — make sure the `index: true` parameter is set in the config or the `--index` flag is used when running.
