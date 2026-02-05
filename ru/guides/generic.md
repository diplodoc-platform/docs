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
          autotitle: true   # опционально: использовать автоматические заголовки из документов, по умолчанию true
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

[*Разводящая_страница]: Корневая страница раздела с навигацией по подразделам (вложенным страницам). [Подробнее](../project/leading-page.md)

[*includer]: Mеханизм подключения файлов.