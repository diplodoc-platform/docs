# Generic

Generic — это встроенный [инклюдер](*includer) для включения Markdown-файлов в структуру документации без ручного перечисления каждого заголовка в `toc.yaml`.

## Пример использования {#example}

Документация находится в директории `doc_root`. Сгенерированный контент нужно положить в директорию `doc_root/gen_docs`.

Добавим в `doc_root/toc.yaml` generic-инклюдер.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: gen_docs # путь к директории с .md файлами для сгененированного контента
      includers: # подключение generic-инклюдер
        - name: generic
          autotitle: true
      mode: link
```

Укажем сгенерированную страницу на [разводящей](*Разводящая_страница) в `doc_root/index.yaml`.

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs # название файла
    href: gen_docs/ # путь к директории с .md файлами для сгененированного контента
```

## Параметры {#settings}

| Параметр | Тип | Значение по умолчанию | Описание |
| --- | --- | --- | --- |
| `autotitle` | `boolean` | `true` | При `true` — в навигации отображаются заголовки из файлов, при `false` — имена файлов. |
| `linkIndex` | `boolean` | `false` | При `true` — файлы `index.md` в поддиректориях используются как ссылка родительского элемента навигации. Раздел становится кликабельным и открывает `index.md`, при этом `index.md` не дублируется в дочерних элементах. |
| `orderBy` | `string` | не задано | Способ [сортировки элементов](#sorting): `natural` (числа в именах сравниваются как числа) или `filename` (строгий лексикографический порядок). Без этого параметра порядок зависит от файловой системы. |
| `order` | `string` | `asc` | Направление [сортировки](#sorting): `asc` или `desc`. Работает только вместе с `orderBy`. |

## Кликабельные разделы с `linkIndex` {#link-index}

По умолчанию generic-инклюдер формирует разделы на основе названий директорий. Элемент раздела является только раскрывающимся — при нажатии он сворачивает или разворачивает список дочерних страниц, а `index.md` становится обычным дочерним элементом.

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

## Сортировка элементов {#sorting}

По умолчанию generic-инклюдер сохраняет порядок, в котором файлы пришли от файловой системы. Это значит, что для документов с числовыми именами (`1.md`, `2.md`, `3.md`, …, `10.md`, …, `100.md`) порядок может быть непредсказуемым.

Чтобы получить детерминированный порядок, задайте параметр `orderBy`:

- `natural` — «естественная» сортировка: каждая последовательность цифр в имени сравнивается как число. Корректно работает для чисто числовых имён (`1`, `2`, `3`, …, `9`, `10`, `11`, …, `99`, `100`), имён с числовым префиксом (`1-intro`, `2-setup`, `10-deep`) и для нескольких групп цифр (`chapter-1-1`, `chapter-1-2`, `chapter-1-10`).
- `filename` — строгий лексикографический порядок. Например: `1`, `10`, `100`, `11`, `2`, `20`, `9`.

Параметр `order` задаёт направление: `asc` (по возрастанию, по умолчанию) или `desc` (по убыванию). Работает только если задан `orderBy`.

Сортировка применяется рекурсивно ко всем уровням оглавления.

### Пример: естественная сортировка числовых файлов

Структура:

```
gen_docs/
  1.md
  2.md
  10.md
  20.md
  100.md
```

Конфигурация:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Результирующий порядок: `1`, `2`, `10`, `20`, `100`.

### Пример: сортировка вложенных директорий

Структура:

```
gen_docs/
  chapter-1/
    intro.md
    section-1.md
    section-2.md
    section-10.md
  chapter-2/
    intro.md
  chapter-10/
    intro.md
```

Конфигурация:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Результирующий порядок на верхнем уровне: `chapter-1`, `chapter-2`, `chapter-10`. Внутри `chapter-1`: `intro`, `section-1`, `section-2`, `section-10`.

### Пример: числовой префикс и несколько групп цифр

Структура:

```
gen_docs/
  1-intro.md
  2-setup.md
  10-advanced.md
  chapter-1-1.md
  chapter-1-2.md
  chapter-1-10.md
```

Конфигурация:

```yaml
includers:
  - name: generic
    orderBy: natural
```

Результирующий порядок: `1-intro`, `2-setup`, `10-advanced`, `chapter-1-1`, `chapter-1-2`, `chapter-1-10`. Каждая последовательность цифр в имени сравнивается как число — поэтому `chapter-1-10` идёт после `chapter-1-2`, а не между `chapter-1-1` и `chapter-1-2`.

[*Разводящая_страница]: Корневая страница раздела с навигацией по подразделам (вложенным страницам). [Подробнее](../project/leading-page.md)

[*includer]: Mеханизм подключения файлов.