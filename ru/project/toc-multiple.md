# Несколько оглавлений

Можно разделить проект документации на части, сгруппировав статьи в несколько оглавлений и связав их перекрестными ссылками.

## Как сгруппировать статьи {#multitoc}

Если завести в какой-то папке проекта файл оглавления `toc.yaml`, то во всех статьях из этой папки и вложенных в неё папок будет выводиться оглавление из этого файла.

Например, в указанной структуре:

```
input-folder
|-- toc.yaml # корневое оглавление
|-- article1.md
|-- article2.md
|-- folder1
    |-- article3.md
|-- folder2
    |-- toc.yaml # оглавление подраздела
    |-- article4.md
    |-- article5.md
    |-- folder3
        |-- article6.md
```

* в файлах `article1.md`, `article2.md`, `article3.md` будет использоваться оглавление из корневого `toc.yaml`,
* в файлах `article4.md`, `article5.md`, `article6.md` будет использоваться оглавление из `folder2/toc.yaml`.

Перекрёстные ссылки между оглавлениями можно делать через включение в `toc.yaml` пунктов из другого оглавления или [расширенную навигацию](./navigation.md) проекта.

Возможное содержание файлов оглавления из примера:

#|
||

##toc.yaml##

|

##folder2/toc.yaml##

||
||

```yaml
items:
  - name: Article 1
    href: article1.md
  - name: Article 2
    href: article2.md
  - name: Article 3
    href: folder1/article3.md
  - name: Article 4
    href: folder2/article4.md # ссылка на подраздел
```

|

```yaml
items:
  - name: Article 4
    href: article4.md
  - name: Article 5
    href: article5.md
  - name: Article 6
    href: folder3/article6.md
  - name: Back to Article 1
    href: ../article1.md # ссылка в корневое оглавление
```

||
|#
