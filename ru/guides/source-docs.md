# Source Docs

Вы можете включить документацию в формате [Source Docs](https://github.com/SourceDocs/SourceDocs) в основной документ.

{% note warning %}

sourcedocs-инклюдер находится в процессе деприкации в пользу [generic-инклюдера](generic.md).

{% endnote %}

#### Пример использования

Проект документации лежит в папке `doc_root`.

Положим результат исполнения Source Docs в папку `doc_root/docs`.

Включим его в документацию внутри `doc_root/toc.yaml`, указав `includer` sourcedocs.

Поставим ссылку на сгенерированную разводящую в основной в `doc_root/index.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: docs
      includer: sourcedocs
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs
    href: docs/
```