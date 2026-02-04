# Generic

{% note info %}

Generic includer включен по умолчанию.

{% endnote %}

Вы можете сгенерировать документацию в markdown-формате любой утилитой и включить её в основную документацию.

Инклюдер сгенерирует по ней оглавление и включит контент в документацию.

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
          input: ./new_docs # опционально: переопределить входную директорию, по умолчанию будет взята указанная выше в path
          autotitle: true   # опционально: использовать автоматические заголовки из документов, по умолчанию false
      mode: link
```

Укажем сгенерированную страницу на [разводящей](*Разводящая_страница) в `doc_root/index.yaml`.

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs # название файла
    href: docs/ # путь к директории с .md файлами для сгененированного контента
```

[*Разводящая_страница]: это корневая страница раздела с навигацией по подразделам (вложенным страницам) [Подробнее](../project/leading-page.md).