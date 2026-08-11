# Single source

Single source is a way of organizing a project that allows you to produce several similar versions of a document from the same source text. For example, help for different platforms, languages, or audiences.

This simplifies project updates and reduces the number of errors. Repeated text is kept in one place, so when updating, you don't need to search for and edit every occurrence.

### Examples 

A user of the [Yandex Mail](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/letter-from-mobile?tabs=defaultTabsGroup-002l0bah_android) mobile app can find instructions in the help adapted [for a smartphone](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/letter-from-mobile?tabs=defaultTabsGroup-002l0bah_android). At the same time, a user of the [web version](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/write-letter) sees instructions that account for the specifics of working with the service in a browser. Both versions of the help are created from the same source text.

After installing [Yandex Music](https://yandex.ru/support/music/ru/new-template/gettingstart), a user can refer to the help to understand how the service works. The help contains clear instructions adapted to a [specific platform](https://yandex.ru/support/music/ru/new-template/appmusic).

## Methods of working with a single source {#methods}

[**Profiling**](./profiling.md) is used to generate several similar documents from a single source document. The text is marked up using [conditional operators](../../syntax/vars.md#conditions) or [variables](../../syntax/vars.md). During the build, only the required text fragments are inserted into each output document.

  This method is used when there is more shared content than unique content.

  {% cut "Example" %}

  In the [Yandex Mail help](https://yandex.ru/support/yandex-360/customers/mail/ru/), a single source text contains instructions for working with the service. Using profiling, two versions of the help are generated from this text: 
  * for the mobile app, fragments describing actions specific to a smartphone are included (for example, actions for [writing a letter](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/letter-from-mobile?tabs=defaultTabsGroup-nrz4zeaf_android));
  * for the web version, fragments describing actions specific to a browser are included (for example, [adding files](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/attachments)).

  {% endcut %}

**Content reuse** allows you to insert repeated text fragments within one or more documents. 

  This method is used when there is more unique content than shared content.

  Reuse is provided by:

  * [Includes](../../syntax/includes.md) — separate files with text, links to which are inserted in the required place in the text. During assembly, the text from the file is inserted in full.

    {% cut "Example" %}

      In the [Yandex Music help](https://yandex.ru/support/music/ru/), some sections contain repeated information. Such blocks are formatted as includes and inserted into the required places in the text. For example, [Additional benefits in Yandex services](https://yandex.ru/support/music/ru/new-template/gettingstart) and [What is included in the Plus subscription](https://yandex.ru/support/music/ru/access-and-account/why-is-paid). 

    {% endcut %}

  * [Variable presets](../../project/presets.md) — a set of variables and their values. When building a document, the variable value is substituted into the text depending on the build conditions.

    {% cut "Example" %}

      In [Yandex Mail help](https://yandex.ru/support/yandex-360/customers/mail/ru/), the variable `действие_с_письмом` can have different values: 
      * for [the mobile app](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/letter-from-mobile?tabs=defaultTabsGroup-08mm4747_android) — “Tap the icon in the lower-right corner of the screen”; 
      * for [the web version](https://yandex.ru/support/yandex-360/customers/mail/ru/web/letter/create/write-letter) — “To create a new message, click “Write” in the upper-left corner of the screen.”

    {% endcut %}

  * [Table of contents includes](../../project/toc-includes.md) — table of contents blocks that are inserted into the main table of contents.

    {% cut "Example" %}

      In [Yandex Mail help](https://yandex.ru/support/yandex-360/customers/mail/ru/), the main help contains several large sections, for example, [“Managing contacts”](https://yandex.ru/support/yandex-360/customers/mail/ru/web/abook), [“Setting up your mailbox”](https://yandex.ru/support/yandex-360/customers/mail/ru/box-settings). For each section, its own table of contents block is created, which includes subsections and key topics. Using table of contents includes, these blocks are included in the general table of contents of the help, allowing users to quickly find the sections they need and navigate large amounts of information.

    {% endcut %}

## Features {#peculiaritys}

* It is recommended to place directories with images and includes in folders named `_assets` and `_includes` respectively. The `_` symbol means that the folder will not be displayed in the final build, but can be used as a source.

* Within a project with profiling, you can additionally use includes or variable presets, so the methods can be combined.

* If you need to publish multiple documents from a single source document on different domains, it is recommended to configure configuration files for [profiling](./profiling.md#configs). When reusing, it is possible to publish multiple documents only on one domain with different URLs.

To debug documentation with includes or variable presets, you can use the local YFM build. 
[Example of a local build with reuse](../../project/presets.md#reuse)
