# Вставка произвольного контента (Includers)

Вы можете включить в оглавление произвольный контент через `includers`, но только в случае если `includer` для этого типа контента имплементирован. Список имплементированных инклюдеров можно посмотреть [ниже](#implement-includers).

Возможные способы указания инклюдеров:

- массив `includer`-объектов в поле `includers`;

- `includer`-объект в поле `includer` (_в процессе деприкации в пользу `includers` поля_).

**Требования к `include`:**

1. `include` должен иметь поле `path`, куда контент будет включен.

2. поле `path` должно быть **путем, куда будет включен контент**.

3. свойство `mode` должно иметь значение `link или пропущенно, `link является дефолтным поведением.

**Требования к `includers`:**

`includers` должен быть массивом includer-объектов, которые будут запущенны в указанном порядке.

**Требования к `includer`:**

Параметры между includer-объектами разные, но имя `includer` является обязательным параметром.

`name` указывает имя инклюдера, который запустится.


#### Пример использования

Абстрактный пример использования инклюдеров

_Уточненный пример смотрите в разделе соответствуещего инклюдера для конкретного примера использования._

```
# toc.yaml
...
items:
  - name: <item-name>
    include:
      path: <path-where-to-include>
      includers:
        - name: <name-of-the-first-includer>
          <includer-parameter>: <includer-parameter-value>
        - name: <name-of-the-second-includer>
        - name: <name-of-the-third-includer>
      mode: link
...
```

## Список имплементированных инклюдеров {#implement-includers}

- [Generic](generic.md);
- [Open API](openapi.md);
- [Unarchive](unarchive.md);
- [Source Docs](source-docs.md) (_в процессе деприкации в пользу generic инклюдера_).