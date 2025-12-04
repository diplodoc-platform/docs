# Профилирование

Текст размечается с помощью [условных операторов](https://diplodoc.com/docs/ru/syntax/vars#conditions) или [переменных](https://diplodoc.com/docs/ru/syntax/vars). При сборке в каждый выходной документ подставляются только нужные фрагменты текста.

## Организация проекта

1. В корне проекта создайте папку `common` с исходными файлами.   
    
1. В корне проекта создайте папки для каждой версии документа. Например, `android` и `ios` для разных платформ.

1. В папках для версий документов настройте [конфигурационные файлы](#configs). 

Пример организации структуры:

```
project_name
├── common  # папка с файлами проекта
│   ├── ru # языковая папка
│   │   ├── index.md
│   |   ├── presets.yaml
│   |   └── toc.yaml
|   └── en  # языковая папка
│       ├── index.md
│       ├── presets.yaml
│       └── toc.yaml
├── document_name_1  # Папка собираемого документа, например android, windows или tld-com
│   ├── .yfm
├── document_name_2
│   ├── .yfm
├── document_name_3
|   ├── .yfm
```

## Шаг 1. Добавьте пресеты переменных {#prepare-conditions}

Cоздайте [файл `presets.yaml`](https://diplodoc.com/docs/ru/project/presets). Общий файл располагается в корневой директории проекта и содержит все переменные для каждого условия профилирования.

Значения переменных, которые установлены по умолчанию, поместите в пресет `default`. Он является обязательным.

Уникальные значения поместите в отдельные пресеты для каждого условия профилирования.

{% cut "Пример файла `presets.yaml` для разных платформ" %}

``` yaml
default: # набор значений по умолчанию
  locale: ru
  platform: browser

ios: # набор значений для ios
  platform: ios

android: # набор значений для android
  platform: android
  ```

{% endcut %}

Обычно условия профилирования называют `product`, `platform`, `audience`, но можно использовать и любые другие имена, которые приняты в вашем проекте.

#### Узнайте больше

- [Как работать с переменными](https://diplodoc.com/docs/ru/syntax/vars)


## Шаг 2. Разметьте текст документа {#set-conditions-text}

Текст размечается с помощью [условных операторов](https://diplodoc.com/docs/ru/syntax/vars#conditions) или [переменных](https://diplodoc.com/docs/ru/syntax/vars).

{% note warning %}

Если текст размечен с помощью переменных, то в файле `presets.yaml` должны быть пресеты для каждого варианта профилирования. При сборке значения переменных берутся из пресета `default` и пресета, который указан в [конфигурационном файле `.yfm`](https://diplodoc.com/docs/ru/settings#config) в параметре `varsPreset`.

{% endnote %}

Условия для профилирования могут быть составными. Несколько условий объединяются с помощью операторов `or` или `and`.

{% cut "Примеры разметки условными операторами" %}


**Три фрагмента, которые отличаются для каждой платформы:**

```
{% if platform == "ios" %}
Скачайте приложение в [App Store](https://www.apple.com/ios/app-store/).
{% endif %}

{% if platform == "android" %}
Скачайте приложение в [Google Play](https://play.google.com).
{% endif %}

{% if platform == "browser" %}
Откройте страницу в браузере.
{% endif %}
```

**Фрагмент можно отнести к нескольким платформам:**

```
{% if platform == "ios" or platform == "android" %}
Скачайте приложение.
{% endif %}
```

**Фрагмент должен отображаться для определенной платформы и только в выбранном регионе:**

```
{% if platform == "browser" and locale == "ru" %}
Откройте страницу example.ru.
{% endif %}
```

{% endcut %}


## Шаг 3. Разметьте оглавление документа {#set-conditions-toc}

[Оглавление документа `toc.yaml`](https://diplodoc.com/docs/ru/project/toc) размечается при помощи условного оператора `when`:

```
when: условие == "значение"
```

{% cut "Примеры" %}

**Две страницы, которые отображаются для разных платформ:**

   ```yaml
   - name: Обзор iOS
     href: iOS-overview.md
     when: platform == "ios"
   - name: Обзор Android
     href: android-overview.md
     when: platform == "android"
   ```

**Одна страница отображается для нескольких платформ:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" or platform == "android"
```

**Страница должна отображаться для определенной платформы и только в выбранном регионе:**

```yaml
- name: Обзор
  href: overview.md
  when: platform == "ios" and locale == "ru"
```

{% endcut %}

[//]: # (TODO: вычитать раздел 4) 

## Шаг 4. Настройте конфигурационные файлы {#configs}

Конфигурационные файлы необходимы для правильной сборки и публикации проекта.

### Файл `.yfm` {#yfm}

В [конфигурационный файл `.yfm`](https://diplodoc.com/docs/ru/settings#config) добавьте следующие параметры сборки:

```yaml
apply-presets: true
varsPreset: "имя-пресета"
```

В поле `varsPreset` укажите имя пресета из [шага 1](#prepare-conditions).
