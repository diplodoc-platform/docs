# Profiling

The text is marked up using [conditional operators](../../syntax/vars.md#conditions) or [variables](../../syntax/vars.md). During the build, only the required text fragments are inserted into each output document.

## Project structure

1. In the project root, create a folder `common` with the source files.   
    
1. In the project root, create folders for each document version. For example, `android` and `ios` for different platforms.

1. In the document version folders, configure [configuration files](#configs). 

Example of the structure organization:

```
project_name
├── common  # папка с файлами проекта
│   ├── ru # языковая папка
│   │   ├── index.md
│   |   ├── presets.yaml
│   |   └── toc.yaml
|   └── en  # языковая папка
│       ├── index.md
│       ├── presets.yaml
│       └── toc.yaml
├── document_name_1  # Папка собираемого документа, например android, windows или tld-com
│   ├── .yfm
├── document_name_2
│   ├── .yfm
├── document_name_3
|   ├── .yfm
```

## Step 1. Add variable presets {#prepare-conditions}

Create a [`presets.yaml` file](../../project/presets.md). The common file is located in the project root directory and contains all variables for each profiling condition.

Place the variable values that are set by default in the `default` preset. It is mandatory.

Place unique values in separate presets for each profiling condition.

{% cut "Example of a `presets.yaml` file for different platforms" %}

``` yaml
default: # набор значений по умолчанию
  locale: ru
  platform: browser

ios: # набор значений для ios
  platform: ios

android: # набор значений для android
  platform: android
  ```

{% endcut %}

Profiling conditions are usually called `product`, `platform`, `audience`, but you can use any other names adopted in your project.

#### Learn more

- [How to work with variables](../../syntax/vars.md)


## Step 2. Mark up the document text {#set-conditions-text}

The text is marked up using [conditional operators](../../syntax/vars.md#conditions) or [variables](../../syntax/vars.md).

{% note warning %}

If the text is marked up using variables, then the `presets.yaml` file must contain presets for each profiling variant. During the build, variable values are taken from the `default` preset and the preset specified in the [configuration file `.yfm`](../../settings.md) in the `varsPreset` parameter.

{% endnote %}

Profiling conditions can be composite. Multiple conditions are combined using the `or` or `and` operators.

{% cut "Examples of markup with conditional operators" %}


**Three fragments that differ for each platform:**

```
{% if platform == "ios" %}
Скачайте приложение в [App Store](https://www.apple.com/ios/app-store/).
{% endif %}

{% if platform == "android" %}
Скачайте приложение в [Google Play](https://play.google.com).
{% endif %}

{% if platform == "browser" %}
Откройте страницу в браузере.
{% endif %}
```

**A fragment can belong to multiple platforms:**

```
{% if platform == "ios" or platform == "android" %}
Скачайте приложение.
{% endif %}
```

**A fragment should be displayed for a specific platform and only in the selected region:**

```
{% if platform == "browser" and locale == "ru" %}
Откройте страницу example.ru.
{% endif %}
```

{% endcut %}


## Step 3. Mark up the document table of contents {#set-conditions-toc}

[The document table of contents `toc.yaml`](../../project/toc.md) is marked up using the `when` conditional operator:

```
when: условие == "значение"
```

{% cut "Examples" %}

**Two pages that are displayed for different platforms:**

   ```yaml
   - name: Обзор iOS
     href: iOS-overview.md
     when: platform == "ios"
   - name: Обзор Android
     href: android-overview.md
     when: platform == "android"
   ```

**One page is displayed for multiple platforms:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" or platform == "android"
```

**A page should be displayed for a specific platform and only in the selected region:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" and locale == "ru"
```

{% endcut %}

[//]: # (TODO: proofread section 4) 

## Step 4. Configure the configuration files {#configs}

Configuration files are required for proper project build and publishing.

### File `.yfm` {#yfm}

In the [configuration file `.yfm`](../../settings.md), add the following build parameters:

```yaml
apply-presets: true
varsPreset: "имя-пресета"
```

In the `varsPreset` field, specify the preset name from [step 1](#prepare-conditions).
