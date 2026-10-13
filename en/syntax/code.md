# Code fragments

A code fragment can be added to the text or placed in a separate block.

## In text {#inline}

To add a code fragment to the text, use the ` character.

```markdown
`Фрагмент кода` в тексте.
```

**Result:**

`Code fragment` in text.

{% include [not_var](../_includes/not_var-info.md) %}

The prefix `not_var` works **only** for code fragments consisting of characters `.-|(),_`, `a-z`, `A-Z`, `0-9` and spaces.

{% note tip "Tip" %}

It is recommended to use no more than 100 characters, as text in such a fragment is not wrapped. For a larger number of characters, format the code as a separate block.

{% endnote %}

## As a separate block {#block}

To format a code fragment as a separate block, separate it from the rest of the text on both sides with ``` characters.

For syntax highlighting, specify the language in which the code is written in the opening line. For example:

````markdown
```sql
  price= '2000'
  size= '24'  
  color= 'primary'
  variant= 'detailed' 
```
````

{% cut "Examples of supported languages" %}

- apache;
- bash;
- coffeescript;
- cpp;
- cs;
- css;
- diff;
- go;
- http;
- ini;
- java;
- javascript;
- json;
- kotlin;
- less;
- lua;
- makefile;
- xml;
- markdown;
- nginx;
- objectivec;
- perl;
- php;
- plaintext;
- properties;
- python;
- ruby;
- rust;
- scss;
- shell;
- sql;
- swift;
- typescript;
- **yaml**.

{% endcut %}

See the [highlight.js documentation](https://highlightjs.readthedocs.io/en/latest/supported-languages.html) for the full list of languages and aliases. Available languages depend on the version and language set of the installed highlighting library; third-party languages must be loaded separately.

### Displaying line numbers {#line-numbers}

If you need to enable line numbers in a code block, use the keyword `showLineNumbers`.

Usage example:

````markdown
```sql showLineNumbers
  price = '2000'
  size = '24'  
  color = 'primary'
  variant = 'detailed' 
```
````

**Result:**

```sql showLineNumbers
  price = '2000'
  size = '24'
  color = 'primary'
  variant = 'detailed'
```

### Line wrapping by default {#softwrap}

To enable soft wrap by default in a code block, use the keyword `wrap`.

Usage example:

````markdown
``` wrap
Очень длинная строка в блоке кода, которая точно не поместится в длину, если её искусственно не свернуть
```
````

**Result:**

``` wrap
Очень длинная строка в блоке кода, которая точно не поместится в длину, если её искусственно не свернуть
```

### Command line prefix {#prompt}

Use the parameter `prompt="<value>"` to exclude the command line prefix (`$`, `#`, `>>>`, `mysql>`, etc.) from selection and copying via the widget.

**Usage example:**

````markdown
```bash prompt="$"
$ npm install
$ npm run build
```
````

**Result:**

```bash prompt="$"
$ npm install
$ npm run build
```

{% note tip "Tip" %}

This feature is especially useful for **snippets**. If a code block contains only commands, without their output, the user can copy the entire content with one button and paste it into the terminal — without selecting lines individually.

{% endnote %}

## Including code from a file {#include-code}

Use the `{% code %}` directive to include a local file as a code block:

````markdown
{% code "./examples/main.ts" lang="typescript" %}
````

A path without a leading `/` is relative to the current Markdown file. A path with a leading `/` is relative to the documentation project root.

The `lang` parameter sets the code block language for syntax highlighting. It supports the same languages and aliases as [regular code blocks](#block): for example, `typescript` or `ts`, `javascript` or `js`, `python` or `py`, `bash` or `sh`, `sql`, `json`, `yaml`, `xml` or `html`. If the parameter is omitted or the highlighting library does not recognize the language, the code is displayed without highlighting. The language is not detected automatically from the file extension.

See the [highlight.js documentation](https://highlightjs.readthedocs.io/en/latest/supported-languages.html) for the full list of `lang` values and aliases.

To enable [line numbers](#line-numbers), append `showLineNumbers` after the language inside the `lang` value:

````markdown
{% code "./examples/main.ts" lang="typescript showLineNumbers" %}
````

Numbering starts at 1 for the displayed fragment, even when `lines` selects it from the middle of a file. The `lines` parameter selects a fragment and does not control the display of line numbers.

By default, the common indentation is removed from all non-empty lines. Add `keep-indents` to preserve the original indentation:

````markdown
{% code "./examples/main.ts" keep-indents %}
````

Use the `lines` parameter to include part of a file by providing two substring markers separated by `-`. The lines containing the markers are excluded.

For example, `examples/main.ts` contains:

```typescript
const before = 1;
// [A]
console.log('Hello');
// [B]
const after = 2;
```

To include the code between the `[A]` and `[B]` markers, specify them in the `lines` parameter:

````markdown
{% code "./examples/main.ts" lang="typescript" lines="[A]-[B]" %}
````

**Result:**

```typescript
console.log('Hello');
```

The `lines` values are substring markers. For example, `lines="2-3"` specifies the markers `2` and `3`, rather than source file line numbers.

If the start or end marker is missing, the [CLI](../tools/docs/build.md) emits a [code directive warning](../project/lint.md#code-directive-warnings) and uses the beginning or end of the file, respectively. If the end marker occurs before the start marker, the builder emits a warning and creates an empty code block.

For a directive with `lines="[A]-[B]"` in `index.md`, the warnings look like this:

```text
index.md: Code directive: start marker "[A]" was not found; using the beginning of the file while including "./examples/main.ts".
index.md: Code directive: end marker "[B]" was not found; using the end of the file while including "./examples/main.ts".
index.md: Code directive: end marker "[B]" occurs before start marker "[A]"; the fragment is empty while including "./examples/main.ts".
```

The message identifies the Markdown file containing the directive, the reason for the warning, and the included file path. Each warning is emitted only when its corresponding condition occurs.

These warnings do not have a dedicated `MD` or `YFM` code: their messages use the `Code directive:` prefix.
