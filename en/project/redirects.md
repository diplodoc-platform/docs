# Redirects

Diplodoc allows you to configure redirects within a project:
* in static documentation — [via page headers](#metatags);
* in the cloud version — [via the ##redirects.yaml## file](#file).

## Redirects in static documentation {#metatags}

{% note warning %}

The proposed solution is temporary. In the future, redirects via ##redirects.yaml## will be supported for static documentation, similar to the cloud version.

{% endnote %}

To configure a redirect, add meta tags to the beginning of the source page:

```yaml
---
metadata:
  - name: redirect
    http-equiv: refresh
    content: '0; url=<path_to_target_page>'
---
```

Field descriptions:

- `name: redirect` — the name of the meta tag to indicate a redirect.
- `http-equiv: refresh` — page refresh by the browser.
- `content: '0; url=<path_to_target_page>'` — an attribute with parameters:
    - `0` — delay in seconds before the redirect. `0` means an immediate redirect.
    - `url=<path_to_target_page>` — the URL of the redirect target page.

In the `url` field, you can specify:

- An absolute path — the full URL of the page to which the redirect should be made.
- A relative path — the path from the source page or the root of the current project. For example, `../folder/page` or `/root-folder/page`.
    
To prevent the source page from appearing in the table of contents, hide it in the `toc.yaml` file:

```yaml
- href: <path_to_source_page>.md
  hidden: true
```

### Limitations {#metatags-limitations}

- Anchor links are not preserved.
- The source file cannot be deleted from the project.

### Example of an external redirect {#metatags-example-ext}

Redirect from `https://diplodoc.com/docs/ru/page-constructor/old-spec/` to `https://preview.gravity-ui.com/page-constructor/`.

1.  File `/ru/page-constructor/old-spec/index.md`:

    ```yaml
    ---
    metadata:
      - name: redirect
        http-equiv: refresh
        content: '0; url=https://preview.gravity-ui.com/page-constructor/'
    ---
    ```

2.  File `/ru/toc.yaml`:

    ```yaml
    - href: page-constructor/old-spec/index.md
      hidden: true
    ```

#### Example of an internal project {#metatags-example-int}

Redirect from the page `ru/settings/old-page.html` to the page `ru/settings/new-folder/new-page.html`.

1.  File `ru/settings/old-page.md`:

    ```yaml
    ---
    metadata:
      - name: redirect
        http-equiv: refresh
        content: '0; url=./new-folder/new-page.html'
    ---
    ```

2.  File `ru/toc.yaml`:

    ```yaml
    - href: settings/old-page.md
      hidden: true
    ```


##  Redirects in the cloud version {#file}

Redirects in the cloud version can be described in the `redirects.yaml` file, which must be located at the same level as the [configuration file `.yfm`](../settings.md).

### File structure {#file-structure}

The `redirects.yaml` file consists of:
* language sections that contain redirects for individual documentation languages;
* the `common` section with redirects for all documentation languages.

Redirects cannot be specified outside a section.

{% note warning %}

Redirects are checked in the following order:

1. The section of redirects for individual documentation languages.
1. The `common` section.

Within sections, redirects are checked in the order they appear: from top to bottom.

{% endnote %}

### Configuration specifics  {#file-details}

* Redirects are configured only within the documentation project.
* Anchor links are not supported.
* In the `common` section, paths are specified relative to the project root. In language sections, paths are specified relative to the language folders without including them directly in the path. For directories, a `/` symbol is added at the end. Specifying the `.md` extension is not required. [Example file](#file-example).
* Regular expressions can be used.

  {% cut "Code example" %}

  ```yaml
  - from: /concepts/referral-(.*)
    to: /index
  ```

  {% endcut %}

### Example ##redirects.yaml## {#file-example}

```yaml
# Секция редиректов для отдельных языков документации
ru:
    - from: /entry1
      to: /folder1/entry1
en:
    - from: /entry2
      to: /folder2/entry2
# Секция common
common:
    - from: /entry3
      to: /folder3/entry3
```

### Examples for files {#file-examples-single}

#|
|| **Redirect** | **Example** ||
|| The file was renamed | 

```yaml
- from: /pricing
  to: /pricing-info
``` 

```yaml
- from: /details/(.*)-mini
  to: /details/$1-mini2
```

||
|| The file was moved to a directory |

```yaml
- from: feedback
  to: /troubleshooting/feedback
```
||
|| The file was moved to a parent directory and renamed |

```yaml
- from: /devices/third-party/troubleshooting/reset
  to: /devices/index
```

||
|| The file was moved to a subdirectory and renamed |

```yaml
- from: /phones/assistance
  to: /phones/help/index
```

||
|| The file was moved from a directory to the root |

```yaml
- from: /devices/index
  to: /index
```

||
|| All files were moved from a directory to the root|

```yaml
- from: /old/concepts/([^/]+)
  to: /index
```

||
|#

### Examples for directories {#file-examples-dir}

#|
|| **Redirect** | **Example** ||
|| The directory was renamed |

```yaml
- from: /devices/settings/
  to: /phones/settings/
```
||
|| All subdirectories were renamed |

```yaml
- from: /(.*)/folder/
  to: /$1/renamed-folder/
```
||
|#

