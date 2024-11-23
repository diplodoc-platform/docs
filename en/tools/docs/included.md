# Dependency Merging

## Description

The "included: true" flag is a configuration parameter that is designed to speed up document processing. It merges all dependent .md files into a single final file, improving performance and simplifying document management.

## Features

- Faster processing: Significantly reduces the time it takes to assemble documents by reducing the number of files to process.
- Consistency: All related documents are merged into one, making them easier to distribute and read.
- Optimization: Avoids redundant I/O operations associated with downloading multiple individual files.

## Usage

To enable this feature, add the following line to your project's configuration file:

```yaml
included: true
```

Once enabled, the system will automatically merge all .md files that are marked as dependent into one:

1. Project root file: This file typically contains the main content and references to other files that need to be merged.
2. Dependent files: Files referenced by the root file will be included in the final document.

## Benefits

- Improved performance: Reduces the time it takes to download and process each individual file.
- Simplified deployment and publishing: A glued together single file is easier to distribute and maintain.
- Compatibility: Works with most standard Markdown syntaxes and tools, making integration painless.

## Limitations

- File size: With a significant number of dependencies, the resulting file size can become too large for convenient use.

## Example

### Input

```md
start main

{% include [Text](included/file-1-deep.md) %}

end main
```

#### included/file-1-deep.md

```md
start file 1

{% include [Text](file-2-deep.md) %}

end file 1
```

#### included/file-2-deep.md

```md
start file 2

{% include [Text](file-3.md) %}

end file 2
```

#### included/file-3.md

```md
start file 3

end file 3
```

### Result

```md
start main

{% include [Text](included/file-1-deep.md) %}

end main
{% included (included/file-1-deep.md:file-2-deep.md:file-3.md) %}
start file 3

end file 3
{% endincluded %}
{% included (included/file-1-deep.md:file-2-deep.md) %}
start file 2

{% include [Text](file-3.md) %}

end file 2
{% endincluded %}
{% included (included/file-1-deep.md) %}
start file 1

{% include [Text](file-2-deep.md) %}

end file 1
{% endincluded %}
```

```html
<p>start main</p>
<p>start file 1</p>
<p>start file 2</p>
<p>start file 3</p>
<p>end file 3</p>
<p>end file 2</p>
<p>end file 1</p>
<p>end main</p>
```