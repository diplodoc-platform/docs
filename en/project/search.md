# Search options in Diplodoc static documentation

In a static documentation build based on Diplodoc, you can enable built-in search in one of two ways:

- **Local search (Lunr.js)**  
  Search is performed in the user's browser — the index is loaded together with the documentation. This option does not require an external server, works in offline environments, and is suitable for small/medium-sized projects. Configured via a configuration section with the `local` provider.  
  For details: [Local search Lunr.js](./lunr.md)

- **Cloud search (Algolia)**
  For large or public documentation, cloud search is available via the [Algolia](https://www.algolia.com/) service. Indexing and search are performed in an external service. It is enabled using the `search` section with the `algolia` provider and the corresponding parameters.
  For details: [Cloud search Algolia](./algolia.md)

By default, search is not enabled. To use one of the implementations, add and configure the `search` section in the [project settings file .yfm](../settings.md#search).
