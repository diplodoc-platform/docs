# Search options in Diplodoc static documentation

In a static documentation build based on Diplodoc, you can enable built-in search in one of three ways:

- **Local search (Lunr.js)**  
  Search is performed in the user's browser — the index is loaded together with the documentation. This option does not require an external server, works in offline environments, and is suitable for small/medium-sized projects. Configured via a configuration section with the `local` provider.  
  For details: [Local search Lunr.js](./lunr.md)

- **Cloud search (Algolia)**
  For large or public documentation, cloud search is available via the [Algolia](https://www.algolia.com/) service. Indexing and search are performed in an external service. It is enabled using the `search` section with the `algolia` provider and the corresponding parameters.
  For details: [Cloud search Algolia](./algolia.md)

- **External HTTP search**: connect a service you host, including an OpenSearch gateway, through a common GET/JSON contract. The browser sends queries directly to the configured endpoint. [Configuration and HTTP contract](./external-search.md).

By default, search is not enabled. To use one of the implementations, add and configure the `search` section in the [project settings file .yfm](../settings.md#search).

## Search JSON export

To prepare page content in a common format for an external search system, enable [JSON export](./search-index.md) during the build. Export works independently of search on the website.
