# Syntax highlighting

The [highlight.js](https://www.npmjs.com/package/highlight.js) package is used to highlight code. For the list of available languages, see [GitHub](https://github.com/highlightjs/highlight.js/tree/master/src/languages).

To install the package, run this command:

```shell
npm i highlight.js
```

## Supported Languages

Key used to enable syntax highlighting inside the code block.

* apache
* bash
* coffeescript
* cpp
* cs
* css
* diff
* go
* http
* ini
* java
* javascript
* json
* kotlin
* less
* lua
* makefile
* xml
* markdown
* nginx
* objectivec
* perl
* php
* plaintext
* properties
* python
* ruby
* rust
* scss
* shell
* sql
* swift
* typescript
* yaml

## Adding other languages {#add}

You can pass an additional set of languages that will be registered for use.

A set of languages is passed as an object, with:

* The name of the language as the key.
* A function that defines the language as the value.

```javascript
const transform = require('@diplodoc/transform');
const customLang = require('./custom-lang');

const highlightLangs = { 'custom-lang': customLang };

const {result: {html, meta}, logs} = transform(content, {highlightLangs});
```
