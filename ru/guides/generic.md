# Generic

Вы можете сгенерировать документацию в markdown-формате любой утилитой и включить её в основную документацию.

Инклюдер сгенерирует по ней оглавление и включит контент в документацию.

#### Пример использования

Проект документации лежит в `doc_root` папке.

Положим сгенерированный контент в папку `doc_root/docs`.

Включим этот контент с помощью generic-инклюдера в `doc_root/toc.yaml`.

Подключим разводящую в `doc_root/index.yaml`.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
  - name: docs
    include:
      path: docs
      includers:
        - name: generic
          input: docs
      mode: link
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: docs
    href: docs/
```