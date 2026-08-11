# Unarchive

You can use the unarchive includer to unpack a tarball before applying other includers to the content inside it, such as the generic includer.

#### Usage example

There is `docs.tar` in the project root at the path `doc_root/docs.tar`.

Inside `docs.tar` there is content that needs to be included using the generic includer.

In this case, you need to apply a chain of includers `unarchive` -> `generic` to achieve the goal.

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