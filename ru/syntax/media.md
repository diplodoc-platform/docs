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

В недавних обновлениях добавлена поддержка сервисов VK Video/Rutube и других сервисов, в которых есть медиапроигрыватели.

Чтобы добавить на страницу видео, используйте разметку: 

```markdown
@[название_видеохостинга](id_видео_или_ссылка_на_него)
```

{% list tabs accordion %}

- Пример использования

  ```markdown
  @[](https://runtime.strm.yandex.ru/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)
  ```

  **Результат:**

  @[](https://runtime.strm.yandex.ru/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)

{% endlist %}

{% note warning %}

❗️Для VK Video, Rutube и других платформ нужно использовать ссылку, которая появляется при экспорте в iframe, а также заполнить квадратные скобки соответственно vk или rutube

```markdown
@[vk](https://vk.com/video_ext.php id=-220754053&id=456241713&hd=2)
```

**Результат:**

@[vk](https://vk.com/video_ext.php id=-220754053&id=456241713&hd=2)


{% endnote %}

Заполните поле [название_видеохостинга] зарезервированным словом из списка:

- YouTube — youtube
- Vimeo — vimeo
- Vine — vine
- Prezi — prezi
- Osf — osf
- Yandex — yandex
- Vk — vk
- Rutube — rutube

Ознакомиться с вариантами оформления и перечнем доступных видеохостингов можно на странице плагина [markdown-it-video](https://www.npmjs.com/package/markdown-it-video).


