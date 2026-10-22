# Linter configuration file

In the project root, you can place a linter configuration file `.yfmlint` to manage documentation build checks.

Default configuration values:

```yaml
log-levels:
  MD001: 'disabled' # Heading levels should only increment by one level at a time
  MD002: 'disabled' # First heading should be a top-level heading~~
  MD003: 'disabled' # Heading style
  MD004: 'disabled' # Unordered list style
  MD005: 'disabled' # Inconsistent indentation for list items at the same level
  MD006: 'disabled' # Consider starting bulleted lists at the beginning of the line~~
  MD007: 'disabled' # Unordered list indentation
  MD009: 'disabled' # Trailing spaces
  MD010: 'disabled' # Hard tabs
  MD011: 'disabled' # Reversed link syntax
  MD012: 'disabled' # Multiple consecutive blank lines
  MD013: 'disabled' # Line length
  MD014: 'disabled' # Dollar signs used before commands without showing output
  MD018: 'error'    # No space after hash on atx style heading
  MD019: 'disabled' # Multiple spaces after hash on atx style heading
  MD020: 'disabled' # No space inside hashes on closed atx style heading
  MD021: 'disabled' # Multiple spaces inside hashes on closed atx style heading
  MD022: 'disabled' # Headings should be surrounded by blank lines
  MD023: 'disabled' # Headings must start at the beginning of the line
  MD024: 'disabled' # Multiple headings with the same content
  MD025: 'disabled' # Multiple top-level headings in the same document
  MD026: 'disabled' # Trailing punctuation in heading
  MD027: 'disabled' # Multiple spaces after blockquote symbol
  MD028: 'disabled' # Blank line inside blockquote
  MD029: 'disabled' # Ordered list item prefix
  MD030: 'disabled' # Spaces after list markers
  MD031: 'disabled' # Fenced code blocks should be surrounded by blank lines
  MD032: 'disabled' # Lists should be surrounded by blank lines
  MD033: 'disabled' # Inline HTML
  MD034: 'disabled' # Bare URL used
  MD035: 'disabled' # Horizontal rule style
  MD036: 'disabled' # Emphasis used instead of a heading
  MD037: 'disabled' # Spaces inside emphasis markers
  MD038: 'disabled' # Spaces inside code span elements
  MD039: 'disabled' # Spaces inside link text
  MD040: 'disabled' # Fenced code blocks should have a language specified
  MD041: 'disabled' # First line in a file should be a top-level heading
  MD042: 'disabled' # No empty links
  MD043: 'disabled' # Required heading structure
  MD044: 'disabled' # Proper names should have the correct capitalization
  MD045: 'disabled' # Images should have alternate text (alt text)
  MD046: 'disabled' # Code block style
  MD047: 'disabled' # Files should end with a single newline character
  MD048: 'disabled' # Code fence style
  
  YFM001: 'warn'    # Inline code length
  YFM002: 'warn'    # No header found in the file for the link text
  YFM003: 'error'   # Link is unreachable
  YFM004: 'error'   # Table not closed
  YFM005: 'warn'    # Tab list, cut, note not opened or closed
  YFM006: 'warn'    # Term definition duplicated
  YFM007: 'warn'    # Term used without definition
  YFM008: 'warn'    # Term inside definition not allowed
  YFM009: 'error'   # Term definition used not at the end of file
  YFM010: 'warn'    # Autotitle anchor is missed
  YFM011: 'warn'    # Max svg size
  YFM012: 'error'   # Max output html size
  YFM013: 'error'   # Max single asset size
  YFM014: 'warn'    # Anchor cannot be used as file path
  YFM015: 'warn'    # Anchor not found in file
  YFM016: 'error'   # The file is included in itself
  YFM017: 'error'   # Invalid front matter format: duplicated mapping key
  YFM018: 'info'    # Term definition from include
  YFM020: 'warn'    # Invalid yfm directive
  YFM021: 'warn'    # Empty automatic heading anchor
  YFM022: 'info'    # llms-full.txt max size reached
  YFM025: 'warn'    # Local link anchor is missing in the target document


# Inline code length
YFM001:
  maximum: 100
```

Rules with the `MD` prefix are provided by the [markdownlint](https://github.com/DavidAnson/markdownlint) library.
A detailed description of all rules with the `MD` prefix can be found [at the link](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md).
A detailed description of all rules with the `YFM` prefix can be found [at the link](https://github.com/diplodoc-platform/yfmlint/blob/master/README.md).

YFM021 reports headings whose automatic anchor is empty. It relies on the anchors plugin from `@diplodoc/transform`; Diplodoc CLI and the VS Code extension include this plugin by default.

You can override the logging level in the `.yfmlint` file in the `log-levels` section separately for each rule: `error`, `warn`, `disabled`.

{% note warning %}

You cannot override the errors `YFM014`, `YFM015`, `YFM016`, and `YFM017`.

{% endnote %}

In the root section, you can configure the values passed to the rules. For example:

```yaml
# Inline code length
YFM001:
  level: warn
  maximum: 100

# Supported yfm directives
YFM020:
  level: warn
  customDirectives:
    - diagram       # skip warning on {% diagram %} directive

# Line length
MD013:
  line_length: 100 # default: 80 characters
  code_blocks: false # exclude this rule for code_blocks
  tables: false # exclude this rule for tables
  headings: false # exclude this rule for headings

# Inline HTML
MD033:
  allowed_elements: [ "span", "br", "p" ]


# Section for defining log levels
log-levels:
```

The default values for rules with the `MD` prefix are specified [at the link](https://github.com/DavidAnson/markdownlint/blob/main/schema/.markdownlint.yaml).
The default values for rules with the `YFM` prefix are specified [at the link](https://github.com/diplodoc-platform/yfmlint/blob/master/src/config.ts).

Rules can be enabled, disabled, or configured for an entire file or a paragraph within a file.
Examples can be viewed [at the link](https://github.com/DavidAnson/markdownlint/blob/a852407c887ec60949aa5365ed964bab833f962f/README.md#configuration).

> See also: [Ajv schema of .yfmlint linter configuration files](https://raw.githubusercontent.com/diplodoc-platform/ajv/refs/heads/master/src/json/yfmlint-schema.json)

## Code directive warnings {#code-directive-warnings}

When [including code from a file](../syntax/code.md#include-code), [Diplodoc CLI](../tools/docs/build.md), the documentation builder, emits warnings with the `Code directive:` prefix if a fragment marker is missing or the end marker occurs before the start marker. This prefix is also used for warnings about ignored unknown attributes, extra arguments, or duplicate directive attributes.

The message level is `warn`. These messages do not have a dedicated `MD` or `YFM` code. The builder emits this diagnostic while processing the directive, so it cannot be configured through `log-levels` in `.yfmlint`; it is emitted even when linting is disabled. See the [directive description](../syntax/code.md#include-code) for the exact messages and builder behavior.

## Where checks run {#check-implementation}

[Diplodoc CLI](../tools/docs/build.md) performs project checks and prepares information about pages, includes, and resources. [@diplodoc/transform](https://github.com/diplodoc-platform/transform) processes markup, and [@diplodoc/yfmlint](https://github.com/diplodoc-platform/yfmlint) produces diagnostics using lint rules.

### Builder diagnostics

| Codes | Check | Builder responsibility |
| --- | --- | --- |
| `YFM012` | Page HTML size | Checks the output size against the configured limit |
| `YFM013` | Resource size | Checks project file sizes against the configured limit |
| `YFM014`, `YFM015` | File path and anchor in `include` | Checks the included file path and fragment anchor; skips an invalid include |
| `YFM016` | A file including itself | Checks dependencies when loading source files |
| `YFM017` | A duplicate metadata key | Checks page metadata when loading source files |
| `YFM022` | The `llms-full.txt` limit | Stops adding articles before exceeding the limit |
| `YAML001` | Local links in YAML pages | Checks that files exist; `log-levels.YAML001` sets the level, and `disabled` turns the check off |

Sources: [source-file processing](https://github.com/diplodoc-platform/cli/tree/master/src/core/markdown/loader), [HTML output checks](https://github.com/diplodoc-platform/cli/tree/master/src/commands/build/features/output-html), [full-text generation](https://github.com/diplodoc-platform/cli/blob/master/src/commands/build/features/llms/index.ts).

### Checks shared between packages

For these rules, the builder prepares data used by plugins and the linter.

| Codes | Check | Builder responsibility |
| --- | --- | --- |
| `YFM003` | Link availability | Checks local files and whether pages are listed in the table of contents |
| `YFM010` | Automatic link titles | Collects target-page titles |
| `YFM011` | Inline SVG size | Supplies file content and the size limit |
| `YFM009`, `YFM018` | Term definitions in included files | Loads includes and preserves information about where definitions come from |
| `YFM025` | Local link anchors | Collects target-page anchors for link validation |

Source: [data preparation for checks](https://github.com/diplodoc-platform/cli/blob/master/src/commands/build/run.ts).

## YFM025 — missing local link anchor

When building HTML, [Diplodoc CLI](../tools/docs/build.md), the documentation builder, checks that the anchor after `#` in a local link exists on the target page. It checks links to the current page (`#section`) and other project pages (`guide.md#section`), using both automatically generated and explicit anchors, including anchors from included files.

For example, `[Section](guide.md#installation)` produces `YFM025 / missing-local-anchor` if `guide.md` is reachable but has no `installation` anchor. Correct the link fragment or add the anchor to the target page. If the target page itself is unreachable, the builder reports `YFM003`.

The default level is `warn`, independently of the `YFM002` setting. To change it, add the following to `.yfmlint`:

```yaml
log-levels:
  YFM025: error # warn to report a warning, disabled to disable the check
```
