# Media

## Images {#images}

Images must be stored in a directory whose name starts with `_`, otherwise they will be deleted during the build. The recommended uploaded file size is 5 MB, the maximum is 10 MB.

The standard markup for inserting an image is as follows:
```
![alt-текст](_images/image.png "текст_подсказки"){width=100 height=100}
```

  * `alt-text — works like the [alt attribute in HTML](https://en.wikipedia.org/wiki/Alt_attribute). It is displayed if the image fails to load, and is used for SEO and screen reader reading.

      {% note info %}
      
      To display alt-text in an SVG image, add the [attribute `inline=false`](#img-inline).
      
      {% endnote %}
      
      
  * ``_images/image.png` — the URL or path to the image file.
  * ``"tooltip_text"` — a tooltip that will be displayed when hovering over the image. Optional parameter.
  * ``width=100`, `height=100` — image dimensions. Optional parameters.

    {% note tip %}

    If you want to preserve the original aspect ratio of the image, specify only its width: `width=100`.

    {% endnote %}

    {% note warning %}

    It is not recommended to pass image dimensions via `=100x200` inside link brackets — this format breaks backward compatibility with markdown markup.

    {% endnote %}

### Image link {#image-link}

You can make an image clickable using the [link formatting rules](./links.md). To do this, add the standard image markup to the part intended for specifying the link text.

```markdown
[![An old rock in the desert](../_images/mountain.jpg "Mountain"){width=100 height=200}](https://yandex.com/images/search?text=mountain)
```

**Result:**

[![An old rock in the desert](../_images/mountain.jpg "Mountain"){width=100 height=200}](https://yandex.com/images/search?text=mountain)

### Reference-style markup for images {#reference-style}

Similar to [reference-style links](./links.md#reference-style), you can declare an image once in a special place and then refer to it by label throughout the rest of the document. This allows you to use the image multiple times without overloading the text with long URLs or other parameters.

```markdown
![An old rock in the desert][image1]

[image1]: ../_images/mountain.jpg "Mountain"
```

**Result:**

![An old rock in the desert][image1]

[image1]: ../_images/mountain.jpg "Mountain"


### SVG inlining {#img-inline}

If SVG images are used in the documentation, Diplodoc embeds them directly into the HTML code as a `` tag during generation. This solution allows applying the current documentation theme settings to the SVG.

To force disable SVG inlining, use the attribute `inline=false`, then

```
![](_images/image.svg){inline=false}
```

will be converted to 
```html
<img src="_images/image.svg"/>
```

You can control SVG image inlining at the project level using the [maxInlineSvgSize](../settings.md#content) setting, which limits the maximum size of embedded images. To disable SVG inlining, set `maxInlineSvgSize` to **zero**.

{% note info %}

The image setting `inline` has higher priority than the project setting `maxInlineSvgSize`: if an SVG image has the parameter `inline=true` set and exceeds the specified size limit, embedding into the HTML code will still be performed.

{% endnote %}

## Video {#video}

{% note info %}

Supported list of video hosting platforms: Yandex, Rutube, VK, Youtube, Vimeo, Vine, Osf, Prezi.

If your video hosting service is not supported, but it has a video export button, use the [Video from another video hosting service](#unsupported-player) section.

{% endnote %}

### Video from a supported video hosting service {#supported-host}

1. To add a video to a page, use the markup:

    ```markdown
    @[название_хостинга](id_видео_или_ссылка_на_него)
    ```

1. Replace `hosting_name` with the name of the video hosting service from the list: `yandex`, `rutube`, `vk`, `youtube`, `vimeo`, `vine`, `osf`, `prezi`.

1. Open the page with the video you want to embed in the documentation. {#href-for-video}

1. Find the code for publishing the video (the code can be found when exporting in the `iframe` tag, for example, in the "Share" section).

    ```html
    <iframe src="https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1" width="853" height="480" allow="autoplay; encrypted-media; fullscreen; picture-in-picture; screen-wake-lock;" frameborder="0" allowfullscreen></iframe>
    ```

1. Replace `video_id_or_link_to_it` with the link from the `src` attribute.

**Markup example:**

```markdown
@[vk](https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1)
```

**Result:**

@[vk](https://vk.com/video_ext.php?oid=-207738372&id=456239060&hd=2&autoplay=1)

{% note alert %}

If the video is not displayed and the player window shows the error `ERR_BLOCKED_BY_CSP`:

1\. Open the `.yfm` configuration file.
2\. Add the video hosting service to the list of allowed domains.

```yaml
resources:
  csp:
    - "frame-src":
        - "ссылка_на_видеохостинг"
```

{% cut "Configuration example" %}

```yaml
allowHtml: true
langs: ['en','ru']

resources:
  csp:
    - "frame-src":
        - "https://vk.com"
        - "https://login.vk.com"        
        - "https://runtime.strm.yandex.ru"

docs-viewer:
  langs: ['en','ru']
...
```

{% endcut %}

{% endnote %}

### Video from another video hosting service {#unsupported-player}

1. To add a video to a page, use the markup:

    ```
    @[](id_видео_или_ссылка_на_него)
    ```

1. Get a link to the [video](#href-for-video).

1. Replace `video_id_or_link_to_it` with the received link.

**Markup example:**

```markdown
@[](https://frontend.vh.yandex.ru/runtime/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)
```

**Result:**

@[](https://frontend.vh.yandex.ru/runtime/player/video/vplvic7jsotpobyc7o5b?autoplay=0&branding=0&from=documentation&mute=0&redirect_from=ugc)
