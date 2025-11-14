# Подключение CSS и JavaScript

{% note warning %}

Свободное подключение JavaScript-файлов разрешено только в статических сборках.

{% endnote %}

CSS-стили и JavaScript-файлы позволяют адаптировать оформление и добавить интерактивность для документации — от тонкой настройки отдельных элементов до создания уникального визуального стиля и поведения.

Чтобы подключить свой стиль или скрипт к проекту:

1. В корне проекта создайте файл со стилем или скриптом, например:  
   - для css: `_assets/style/custom.css`  
   - для js: `_assets/script/custom.js`
2. Добавьте в соответствующий файл CSS- или JavaScript-код.
3. В конфигурационный файл `.yfm` добавьте нужный блок:
    ```yaml
    resources:
      style:
        - _assets/style/custom.css
      script:
        - _assets/script/custom.js
    ```
4. Соберите проект с флагом `--allow-custom-resources`.

Пример использования стилей см. в [репозитории Diplodoc](https://github.com/diplodoc-platform/docs).
