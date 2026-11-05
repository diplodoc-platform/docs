# External HTTP search

Connect any search service that implements the Diplodoc HTTP contract. For example, a gateway can translate these requests to OpenSearch and return its results in the format below. The documentation frontend does not depend on the underlying search engine.

## Configuration

Add to the project's `.yfm`:

```yaml
search:
  provider: external
  endpoint: https://search.example.com/docs/search
  options:
    project: reference
    version: v1
```

For suggestions in the site header, enable [extended navigation](./navigation.md) in `toc.yaml`, for example:

```yaml
navigation:
  header:
    rightItems:
      - type: search
```

Build with `yfm build -i ./docs -o ./docs-out`. No search extension or custom JavaScript is required.

The same settings can be supplied from the command line:

```bash
yfm build -i ./docs -o ./docs-out \
  --search-provider external \
  --search-endpoint https://search.example.com/docs/search \
  --search-options '{"project":"reference","version":"v1"}'
```

CLI values override the corresponding `.yfm` settings. `--search-options` replaces the options object. `--no-search` or `search.enabled: false` disables search; `--search` explicitly enables it.

`endpoint` can be:

- An absolute HTTP(S) URL: `https://search.example.com/docs/search`.
- An origin-relative path: `/api/docs/search`.
- A path relative to the published documentation root: `api/search`. If documentation is published at `https://example.com/product/v1/`, this resolves to `https://example.com/product/v1/api/search`, both from an article and from the search results page.

Do not use protocol-relative URLs, URL credentials, fragments, spaces, or backslashes. The endpoint and `options` are public configuration embedded in the generated HTML. Keep credentials for OpenSearch or another backend on the server.

## Request

The browser sends a `GET` request with `Accept: application/json` to `endpoint`:

| Query parameter | Meaning |
| --- | --- |
| `query` | Search text, URL-encoded. May be empty, for example when filtering by tags. |
| `lang` | Current documentation language, such as `en` or `ru`. |
| `count` | Requested maximum number of results on the page. |
| `page` | Page number, starting at `1`. |
| `tags` | Selected tag. Repeated for multiple tags, omitted when none are selected. |

Each property in `options` becomes an additional query parameter. String, number, and boolean values are supported and converted to strings. Existing query parameters in `endpoint` are retained unless overwritten by `options` or contract parameters. `query`, `lang`, `count`, `page`, and `tags` are reserved: the current request always takes precedence.

Example request:

```text
GET /docs/search?project=reference&version=v1&query=quick%20start&lang=en&count=10&page=2&tags=api&tags=guide
```

The service should filter by the requested language, return the requested page, and use OR semantics for multiple tags. Total counts must refer to all matching results, before pagination. If the service does not support tag filters, keep them absent from documentation links.

## Response

Return HTTP `200` with a JSON object:

```json
{
  "items": [
    {
      "title": "Quick start",
      "url": "/product/v1/en/quickstart.html",
      "description": "Create your first documentation project.",
      "section": "Guides"
    }
  ],
  "total": 12,
  "tagCounts": {
    "guide": 12
  }
}
```

`items` is an array. Each item must contain string fields `title`, `url`, and `description`; `section` is an optional string. Return links that work from both articles and the search page, preferably origin-relative paths or absolute URLs. Do not return a raw OpenSearch response.

`total` is a non-negative integer containing the total number of matches. `tagCounts` is optional and maps tags to non-negative integer counts. Return `{"items": [], "total": 0}` when nothing matches.

Public page metadata tags populate the tag filter; technical tags starting with `_` and tags from pages marked `noIndex` are excluded.

The same endpoint serves suggestions: the client requests page `1` with the required `count` and displays its items in the suggestion list. Suggestions and full search use the same response shape. No separate suggest endpoint is required.

Non-success HTTP responses, network failures, and invalid response shapes are treated as search errors. They do not cause a fallback to local search.

## Hosting and indexing

Requests run in the user's browser, not on the build machine. For a cross-origin endpoint, configure CORS to allow the documentation origin and use HTTPS when documentation is served over HTTPS. If your project or hosting uses a restrictive CSP, allow the worker and the endpoint in that policy. The external provider does not restrict connections to other services. The HTTP worker uses the browser's default same-origin credentials policy and does not add an authorization header.

The CLI generates the search results page and packages the HTTP client. It does not call the endpoint during the build, create the external index, upload documents, or manage the search service. The service owner is responsible for indexing and for respecting document visibility, including `noIndex` metadata and access controls.
