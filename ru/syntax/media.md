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

Поддерживаемый список видеохостингов: Yandex, Rutube, VK, Youtube, Vimeo, Vine, Osf, Prezi.

Если ваш видеохостинг не поддерживается, но у него есть кнопка экспорта видео, то воспользуйтесь разделом [Видео из другого видеохостинга](#unsupported-player).

{% endnote %}

### Видео из поддерживаемого видеохостинга {#supported-host}

1. Чтобы добавить на страницу видео, используйте разметку:

    ```markdown
    @[название_хостинга](id_видео_или_ссылка_на_него)
    ```

1. Замените `название_хостинга` на название видеохостинга из списка: `yandex`, `rutube`, `vk`, `youtube`, `vimeo`, `vine`, `osf`, `prezi`.

1. Откройте страницу с видео, которое нужно встроить в документацию. {#href-for-video}

1. Найдите код для публикации видео (код можно найти при экспорте в теге `iframe`, например, в разделе «Поделиться»).

    ```html
    <iframe src="https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1" width="853" height="480" allow="autoplay; encrypted-media; fullscreen; picture-in-picture; screen-wake-lock;" frameborder="0" allowfullscreen></iframe>
    ```

1. Замените `id_видео_или_ссылка_на_него` на ссылку из атрибута `src`.

**Пример разметки:**

```markdown
@[vk](https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1)
```

**Результат:**

@[vk](https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1)

{% note alert %}

Если видео не отображается, и окно проигрывателя выдает ошибку `ERR_BLOCKED_BY_CSP`:

1\. Откройте `.yfm` файл конфигурации.
2\. Добавьте видеохостинг в список разрешенных доменов.

```yaml
resources:
  csp:
    - "frame-src":
        - "ссылка_на_видеохостинг"
```

{% cut "Пример конфига" %}

```yaml
allowHTML: true
langs: ['en','ru']

resources:
  csp:
    - "frame-src":
        - "https://vk.com"
        - "https://login.vk.com"        
        - "https://runtime.strm.yandex.ru"

docs-viewer:
  project-name: diplodoc
  langs: ['en','ru']
...
```

{% endcut %}

{% endnote %}

### Видео из другого видеохостинга {#unsupported-player}

1. Чтобы добавить на страницу видео, используйте разметку:

    ```
    @[](id_видео_или_ссылка_на_него)
    ```

1. Получите ссылку на [видео](#href-for-video).

1. Замените `id_видео_или_ссылка_на_него` на полученную ссылку.

**Пример разметки:**

```markdown
@[](https://frontend.vh.yandex.ru/runtime/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)
```

**Результат:**

@[](https://frontend.vh.yandex.ru/runtime/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)