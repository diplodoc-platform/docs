# Медиа

## Изображения {#images}

{% note warning %}

Изображения должны храниться в каталоге, имя которого начинается с символа `_`, иначе они будут удалены при сборке.

{% endnote %}

Стандартная разметка для вставки изображения имеет вид:
```
![alt-текст](_images/image.png "текст_подсказки" =100x100)
```

  * `alt-текст` —  название изображения, задается автором. В сборке не отображается.
  * `_images/image.png` — URL или путь до файла изображения.
  * `"текст_подсказки"` — подсказка, которая будет отображаться при наведении на изображение. Необязательный параметр.
  * `=100x100` — размер изображения. Необязательный параметр.

    {% note tip %}

    Если вы хотите сохранить оригинальное соотношение сторон изображения, укажите только его ширину: `=100x`.

    {% endnote %}

### Изображение-ссылка {#image-link}

Вы можете сделать изображение кликабельным, используя [правила оформления ссылок](./links.md). Для этого добавьте стандартную разметку изображения в ту часть, которая предназначена для указания текста ссылки.

```markdown
[![An old rock in the desert](../_images/mountain.jpg "Mountain" =100x200)](https://yandex.com/images/search?text=mountain)
```

**Результат:**

[![An old rock in the desert](../_images/mountain.jpg "Mountain" =100x200)](https://yandex.com/images/search?text=mountain)

### Reference-style разметка для изображений {#reference-style}

Аналогично [reference-style ссылкам](./links.md#reference-style), вы можете один раз объявить изображение в специальном месте, а в остальном документе обращаться к нему по метке. Это позволит использовать изображение несколько раз, не перегружая текст длинными URL или другими параметрами.

```markdown
![An old rock in the desert][image1]

[image1]: ../_images/mountain.jpg "Mountain"
```

**Результат:**

![An old rock in the desert][image1]

[image1]: ../_images/mountain.jpg "Mountain"

## Видео {#video}

{% note info %}

Поддерживаются все сервисы, в которых есть медиапроигрыватели.

{% endnote %}

1. используйте разметку: 

    ```markdown
    @[название_видеохостинга](id_видео_или_ссылка_на_него)
    ```

1. Замените `название_видеохостинга` на значение, соответствующее вашему видеохостингу:

    - `youtube`
    - `vimeo`
    - `vine`
    - `prezi`
    - `osf`
    - `yandex`
    - `vk`
    - `rutube`

1. Получите ссылку на видео.

    {% cut "Инструкция по получению ссылки на видео" %}

    1. Откройте видео.
    1. Найдите код для публикации видео (его можно найти при экспорте, например, в разделе «Поделиться»).

        {% cut "Пример кода публикации" %}

        ```html
        <iframe width="720" height="405" src="https://rutube.ru/play/embed/c25a0402e866c6fed5347be6d7dbf9ca/" frameBorder="0" allow="clipboard-write; autoplay" webkitAllowFullScreen mozallowfullscreen allowFullScreen></iframe>
        ```

        {% endcut %}

    1. Используйте ссылку из атрибута `src` в разметке.

        ```markdown
        @[rutube](https://rutube.ru/play/embed/c25a0402e866c6fed5347be6d7dbf9ca/)
        ```

        **Результат**:

        @[rutube](https://rutube.ru/play/embed/c25a0402e866c6fed5347be6d7dbf9ca/)

    {% endcut %}

{% note alert %}

Если видео не показывается в окне проигрывателя с ошибкой `ERR_BLOCKED_BY_CSP`, то добавьте в файле конфигурации `.yfm` видеохостинг в список разрешенных доменов.

```yaml
resources:
  csp:
    - "frame-src":
        - "https://rutube.ru"
```

{% endnote %}

Ознакомиться с вариантами оформления и перечнем доступных видеохостингов можно на странице плагина [markdown-it-video](https://www.npmjs.com/package/markdown-it-video).