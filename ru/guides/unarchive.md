# Unarchive

Вы можете использовать unarchive-инклюдер чтобы распаковать tarball перед тем как применять другие инклюдеры к контенту внутри него, например generic-инклюдер.

#### Пример использования

Есть `docs.tar` в корне проекта по пути `doc_root/docs.tar`.

Внутри `docs.tar` находится контент, который необходимо включить используя generic-инклюдер.

В этом случае нужно применить цепь инклюдеров `unarchive` -> `generic` для достижения цели.

```yaml
# doc_root/toc.yaml
title: documentation
href: index.yaml
items:
...
   - name: multiple
     include:
       path: multiple
       mode: link
       includers:
         # run unarchive includer
         - name: unarchive
           # specify tarball you want to unpack as input parameter
           input: docs.tar
           # specify output path where tarball content is going to be unpacked
           output: unpacked
         # run generic includer
         - name: generic
           # specify path from unarchive includers output field as input path
           input: unpacked
```

```yaml
# doc_root/index.yaml
title: documentation
links:
  - title: openapi
    href: openapi/
```