# Generic

{% note info %}

Generic includer включен по умолчанию.

{% endnote %}

Generic — это встроенный [includer](*includer), который позволяет автоматически включать Markdown-файлы в структуру документации без ручного перечисления каждого заголовка в `toc.yaml`.

## Пример использования

Документация находится в директории `doc_root`. Сгенерированный контент нужно положить в директорию `doc_root/gen_docs`.

Добавим в `doc_root/toc.yaml` generic includer.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: gen_docs # путь к директории с .md файлами для сгененированного контента
      includers: # подключение generic includer
        - name: generic
          autotitle: true   # опционально: при false, проставляет в структуру название md-файлов, при true — название заголовков, по умолчанию true
      mode: link
```

Укажем сгенерированную страницу на [разводящей](*Разводящая_страница) в `doc_root/index.yaml`.

## Параметры

| Параметр | Тип | Значение по умолчанию | Описание |
| --- | --- | --- | --- |
| `autotitle` | `boolean` | `true` | При `true` — в навигации отображаются заголовки из файлов, при `false` — имена файлов. |
| `linkIndex` | `boolean` | `false` | При `true` — файлы `index.md` в поддиректориях используются как ссылка родительского элемента навигации. Раздел становится кликабельным и открывает `index.md`, при этом `index.md` не дублируется в дочерних элементах. |

## Кликабельные разделы с `linkIndex` {#link-index}

По умолчанию generic includer формирует разделы на основе названий директорий. Элемент раздела является только раскрывающимся — при нажатии он сворачивает или разворачивает список дочерних страниц, а `index.md` становится обычным дочерним элементом.

С опцией `linkIndex: true` поведение меняется: файл `index.md` внутри поддиректории становится ссылкой (`href`) родительского элемента навигации. При нажатии на раздел открывается `index.md`, а список дочерних страниц разворачивается с помощью стрелки.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: gen_docs
      includers:
        - name: generic
          linkIndex: true
      mode: link
```

### Пример

Структура директории:

```
gen_docs/
  section-a/
    index.md
    page1.md
    page2.md
  section-b/
    index.md
    page1.md
```

Без `linkIndex` (по умолчанию):

```yaml
- name: section-a        # не кликабельный, только раскрывается
  items:
    - name: index
      href: section-a/index.md
    - name: page1
      href: section-a/page1.md
    - name: page2
      href: section-a/page2.md
```

С `linkIndex: true`:

```yaml
- name: section-a        # кликабельный, открывает index.md
  href: section-a/index.md
  items:
    - name: page1
      href: section-a/page1.md
    - name: page2
      href: section-a/page2.md
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs # название файла
    href: gen_docs/ # путь к директории с .md файлами для сгененированного контента
```

[*Разводящая_страница]: Корневая страница раздела с навигацией по подразделам (вложенным страницам). [Подробнее](../project/leading-page.md)

[*includer]: Mеханизм подключения файлов.