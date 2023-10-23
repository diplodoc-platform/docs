# Linter configuration file

A project may contain a linter configuration file. By default, a `.yfmlint` file is used in the root of the project.

The default config looks like this:

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

# Inline code length
YFM001:
  maximum: 100
```

Rules with the prefix `MD` are provided by the library [markdownlint](https://github.com/DavidAnson/markdownlint).
A detailed description of all the rules with `MD` prefix can be found [here](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md).
A detailed description of all the rules with `YFM` prefix can be found [here](https://github.com/yandex-cloud/yfm-transform/blob/master/lib/yfmlint/README.md).

In the `.yfmlint` config in the `log-levels` section, you can override the logging level separately for each rule: `error`, `warn`, `disabled`.

In the root section of the config, you can configure the values passed to the rules. For example:

```yaml
# Inline code length
YFM001:
  maximum: 100
  
# Line length
MD013:
  line_length: 100 # default: 80 characters
  code_blocks: false # exclude this rule for code_blocks
  tables: fales # exclude this rule for tables
  headings: false # exclude this rule for headings

# Inline HTML
MD033:
  allowed_elements: [ "span", "br", "p" ]


# Section for defining log levels
log-levels:
```

Default values for rules with the prefix `MD` are specified [here.](https://github.com/DavidAnson/markdownlint/blob/main/schema/.markdownlint.yaml)
Default values for rules with the prefix `YFM` are specified [here.](https://github.com/yandex-cloud/yfm-transform/blob/master/lib/yfmlint/yfmlint.js)

Rules can be enabled, disabled, and configured for an entire file or a paragraph of a file.
Look at the examples [here.](https://github.com/DavidAnson/markdownlint/blob/a852407c887ec60949aa5365ed964bab833f962f/README.md#configuration) 
