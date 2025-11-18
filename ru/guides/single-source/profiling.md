# Профилирование

Текст размечается с помощью [условных операторов](https://diplodoc.com/docs/ru/syntax/vars#conditions) или [переменных](https://diplodoc.com/docs/ru/syntax/vars). При сборке в каждый выходной документ подставляются только нужные фрагменты текста.

## Организация проекта

1. В корне проекта создайте папку `common` с исходными файлами.   
    
1. В корне проекта создайте папки для каждой версии документа. Например, `android` и `ios` для разных платформ.

1. В папках для версий документов настройте [конфигурационные файлы](#configs). 

1. В корне проекта добавьте общий [файл `a.yaml`](#a-yaml) — он запускает сборку всех версий документа при изменении в исходных файлах.

Пример организации структуры:

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
│   ├── a.yaml
│   └── ya.make
├── document_name_2
│   ├── .yfm
│   ├── a.yaml
│   └── ya.make
├── document_name_3
|   ├── .yfm
|   ├── a.yaml
|   └── ya.make
└a.yaml  # общий файл a.yaml
```

## Шаг 1. Добавьте пресеты переменных {#prepare-conditions}

Cоздайте [файл `presets.yaml`](https://diplodoc.com/docs/ru/presets.md). Общий файл располагается в корневой директории проекта и содержит все переменные для каждого условия профилирования.

Значения переменных, которые установлены по умолчанию, поместите в пресет `default`. Он является обязательным.

Уникальные значения поместите в отдельные пресеты для каждого условия профилирования.

{% cut "Пример файла `presets.yaml` для разных платформ" %}

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

Обычно условия профилирования называют `product`, `platform`, `audience`, но можно использовать и любые другие имена, которые приняты в вашем проекте.

#### Узнайте больше

- [Как работать с переменными](https://diplodoc.com/docs/ru/syntax/vars)


## Шаг 2. Разметьте текст документа {#set-conditions-text}

Текст размечается с помощью [условных операторов](https://diplodoc.com/docs/ru/syntax/vars#conditions) или [переменных](https://diplodoc.com/docs/ru/syntax/vars).

{% note warning %}

Если текст размечен с помощью переменных, то в файле `presets.yaml` должны быть пресеты для каждого варианта профилирования. При сборке значения переменных берутся из пресета `default` и пресета, который указан в [конфигурационном файле `.yfm`](https://diplodoc.com/docs/ru/settings#config) в параметре `varsPreset`.

{% endnote %}

Условия для профилирования могут быть составными. Несколько условий объединяются с помощью операторов `or` или `and`.

{% cut "Примеры разметки условными операторами" %}


**Три фрагмента, которые отличаются для каждой платформы:**

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

**Фрагмент можно отнести к нескольким платформам:**

```
{% if platform == "ios" or platform == "android" %}
Скачайте приложение.
{% endif %}
```

**Фрагмент должен отображаться для определенной платформы и только в выбранном регионе:**

```
{% if platform == "browser" and locale == "ru" %}
Откройте страницу example.ru.
{% endif %}
```

{% endcut %}


## Шаг 3. Разметьте оглавление документа {#set-conditions-toc}

[Оглавление документа `toc.yaml`](https://diplodoc.com/docs/ru/project/toc) размечается при помощи условного оператора `when`:

```
when: условие == "значение"
```

{% cut "Примеры" %}

**Две страницы, которые отображаются для разных платформ:**

   ```yaml
   - name: Обзор iOS
     href: iOS-overview.md
     when: platform == "ios"
   - name: Обзор Android
     href: android-overview.md
     when: platform == "android"
   ```

**Одна страница отображается для нескольких платформ:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" or platform == "android"
```

**Страница должна отображаться для определенной платформы и только в выбранном регионе:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" and locale == "ru"
```

{% endcut %}

[//]: # (TODO: вычитать раздел 4) 

## Шаг 4. Настройте конфигурационные файлы {#configs}

Конфигурационные файлы необходимы для правильной сборки и публикации проекта.

{% note info %}

Если для проекта необходима автоматическая выкладка в прод, ее можно будет настроить только для одного из документов проекта, для остальных нужно будет делать ручную выкладку. Подробнее об этом можно почитать в [разделе Выкладка через Арканум](https://docs.yandex-team.ru/docstools/deploy/release#vykladka-cherez-arkanum).

{% endnote %}


### Файл `.yfm` {#yfm}

[В конфигурационный файл `.yfm`](https://diplodoc.com/docs/ru/settings#config) добавьте следующие параметры сборки:

```yaml
apply-presets: true
varsPreset: "имя-пресета"
```

В поле `varsPreset` укажите имя пресета из [шага 1](#prepare-conditions).


### Файл `ya.make` {#yamake}

В [конфигурационный файл `ya.make`](https://docs.yandex-team.ru/docstools/settings/yamake) для каждого документа, который собирается из единого источника, добавьте макрос `DOCS_DIR` и укажите путь от корня Аркадии до папки с документом-источником:

Пример:

```
DOCS_DIR (docs/yateam/ei/common)
```

[//]: # (Для файла `ya.make`, который находится в папке с документом-источником, указывать макрос `DOCS_DIR` не нужно.)


### Файл `a.yaml` {#a-yaml}

[Конфигурационный файл `a.yaml`](https://docs.yandex-team.ru/docstools/settings/ayaml) содержит настройки деплоя. Деплой настраивается отдельно для каждого документа.

1. В корневую папку документации добавьте общий файл `a.yaml`.

    ```yaml
    title: title
    service: service
    ci:
    on-demand-auto:
        - tags:
            - docs-build
            - docs-release
    ```

    
    {% note warning %}

    Общий файл `a.yaml` обязательный. Он разрешает автоматически запускать деплой для всех документов при изменении исходных файлов.

    {% endnote %}

1. Добавьте файл `a.yaml` в корень каждого документа, собираемого из единого источника. Заполните поля `title`, `ci.secret`, `ci.runtime`. В блоках `actions` и `releases` укажите путь до директории с общим файлом `a.yaml`.

    ```yaml
    title: title
    service: service

    ci:
    includes:
        docs: ci/registry/common/docs/docs.a.yaml

    extends: "docs#/any/default-config"

    secret: sec-***********
    runtime:
        sandbox:
        owner: ******
        notifications:
            - statuses: FAILURE
            transport: email
            recipients: ********

    actions:
        precommit:
        triggers: !override
            - on: pr
            on-demand: true
            filters:
                - sub-paths: ['**']
                - abs-paths: ['<путь от корня Аркадии до директории с общим a.yaml>/**']

    releases:
        docs:
        filters: !override
            - sub-paths: ['**']
            - abs-paths: ['build/platform/yfm', '<путь от корня Аркадии до директории с общим a.yaml>/**']
    ```
