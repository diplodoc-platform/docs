# Редиректы

Diplodoc позволяет настраивать редиректы внутри проекта:
* в статической документации — [через заголовки страниц](#metatags);
* в облачной версии — [через файл ##redirects.yaml##](#file).

## Редиректы в статической документации {#metatags}

{% note warning %}

Предложенное решение является временным. В будущем для статической документации будут поддержаны редиректы через ##redirects.yaml## по аналогии с облачной версией.

{% endnote %}

Чтобы настроить редирект, в начало исходной страницы добавьте метатеги:

```yaml
---
metadata:
  - name: redirect
    http-equiv: refresh
    content: '0; url=<путь_к_целевой_странице>'
---
```

Описание полей:

- `name: redirect` — имя метатега для обозначения редиректа.
- `http-equiv: refresh` — обновление страницы браузером.
- `content: '0; url=<путь_к_целевой_странице>'` — атрибут с параметрами:
    - `0` — задержка в секундах перед редиректом. `0` означает немедленный редирект.
    - `url=<путь_к_целевой_странице>` — URL-адрес целевой страницы редиректа.

В поле `url` можно указать:

- Абсолютный путь — полный URL-адрес страницы, на которую нужно сделать редирект.
- Относительный путь — путь от исходной страницы или корня текущего проекта. Например, `../folder/page` или `/root-folder/page`.
    
Чтобы исходная страница не отображалась в оглавлении, скройте ее в файле `toc.yaml`:

```yaml
- href: <путь_к_сходной_странице>.md
  hidden: true
```

### Ограничения {#metatags-limitations}

- Не сохраняют якорные ссылки.
- Исходный файл нельзя удалить из проекта.

### Пример внешнего редиректа {#metatags-example-ext}

Редирект с `https://diplodoc.com/docs/ru/page-constructor/old-spec/` на `https://preview.gravity-ui.com/page-constructor/`.

1.  Файл `/ru/page-constructor/old-spec/index.md`:

    ```yaml
    ---
    metadata:
      - name: redirect
        http-equiv: refresh
        content: '0; url=https://preview.gravity-ui.com/page-constructor/'
    ---
    ```

2.  Файл `/ru/toc.yaml`:

    ```yaml
    - href: page-constructor/old-spec/index.md
      hidden: true
    ```

#### Пример внутреннего проекта {#metatags-example-int}

Редирект со страницы `ru/settings/old-page.html` на страницу `ru/settings/new-folder/new-page.html`.

1.  Файл `ru/settings/old-page.md`:

    ```yaml
    ---
    metadata:
      - name: redirect
        http-equiv: refresh
        content: '0; url=./new-folder/new-page.html'
    ---
    ```

2.  Файл `ru/toc.yaml`:

    ```yaml
    - href: settings/old-page.md
      hidden: true
    ```


##  Редиректы в облачной версии {#file}

Редиректы в облачной версии можно описать в файле `redirects.yaml`, который должен быть расположен на одном уровне с [конфигурационным файлом `.yfm`](../settings.md).

### Структура файла {#file-structure}

Файл `redirects.yaml` состоит из:
* языковых секций, которые содержат редиректы для отдельных языков документации;
* секции `common` с редиректами для всех языков документации.

Указывать редиректы вне секции нельзя.

{% note warning %}

Редиректы проверяются в следующем порядке:

1. Секция редиректов для отдельных языков документации.
1. Секция `common`.

Внутри секций редиректы проверяются в порядке расположения: сверху вниз.

{% endnote %}

### Особенности настройки  {#file-details}

* Редиректы настраиваются только внутри документационного проекта.
* Не поддержана работа с якорными ссылками.
* В секции `common` пути указываются относительно корня проекта. В языковых секциях пути указываются относительно языковых папок без их прямого указания в пути. Для директорий в конце добавляется символ `/`. Указывать расширение `.md` не требуется. [Пример файла](#file-example).
* Можно использовать регулярные выражения.

  {% cut "Пример кода" %}

  ```yaml
  - from: /concepts/referral-(.*)
    to: /index
  ```

  {% endcut %}

### Пример ##redirects.yaml## {#file-example}

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

### Примеры для файлов {#file-examples-single}

#|
|| **Редирект** | **Пример** ||
|| Файл переименовали | 

```yaml
- from: /pricing
  to: /pricing-info
``` 

```yaml
- from: /details/(.*)-mini
  to: /details/$1-mini2
```

||
|| Файл перенесли в каталог |

```yaml
- from: feedback
  to: /troubleshooting/feedback
```
||
|| Файл перенесли в каталог выше и переименовали |

```yaml
- from: /devices/third-party/troubleshooting/reset
  to: /devices/index
```

||
|| Файл перенесли в каталог ниже и переименовали |

```yaml
- from: /phones/assistance
  to: /phones/help/index
```

||
|| Файл перенесли из каталога в корень |

```yaml
- from: /devices/index
  to: /index
```

||
|| Все файлы перенесли из каталога в корень|

```yaml
- from: /old/concepts/([^/]+)
  to: /index
```

||
|#

### Примеры для каталогов {#file-examples-dir}

#|
|| **Редирект** | **Пример** ||
|| Каталог переименовали |

```yaml
- from: /devices/settings/
  to: /phones/settings/
```
||
|| Все подкаталоги переименовали |

```yaml
- from: /(.*)/folder/
  to: /$1/renamed-folder/
```
||
|#

