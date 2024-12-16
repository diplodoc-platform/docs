# Media

## Images {#images}

{% note warning %}

Images should be stored in a directory whose name starts with `_`. Otherwise, they will be deleted when making a build.

{% endnote %}

The standard markup for inserting an image is:

```
![alt-text](_images/image.png "hint_text" =100x100)
```

* `alt-text`: Alternative image text.
* `_images/image.png`: The URL or path to the image file.
* `"hint_text"`: A hint that will be displayed when you hover over the image. Optional.
* `=100x100`: The image size. Optional.

  {% note tip %}

  If you want to keep the aspect ratio of your image, only specify its width: `100x`.

  {% endnote %}

### Images with captions

You can enable the display of the caption you need to add the { caption } as attribute, the default value is equal to the title, but it can also be passed in the attribute.

```markdown
![Alt text](../../_images/mountain.jpg "Default caption text" =100x100){ caption }

![Alt text](../../_images/mountain.jpg "Title" =100x100){ caption="Specified caption text" }
```

**Result**

![Alt text](../../_images/mountain.jpg "Default caption text" =100x100){ caption }

![Alt text](../../_images/mountain.jpg "Title" =100x100){ caption="Specified caption text" }


### Images as links {#image-link}

You can make an image clickable using [link design rules](./links.md). To do this, add the standard image markup to the part where the link text usually goes.

```markdown
[![An old rock in the desert](../../_images/mountain.jpg "Mountain" =100x200)](https://yandex.com/images/search?text=mountain)
```

**Result**

[![An old rock in the desert](../../_images/mountain.jpg "Mountain" =100x200)](https://yandex.com/images/search?text=mountain)

### Reference-style markup for images {#reference-style}

Similarly to [reference-style links](./links.md#reference-style), you can declare an image in a special place once and refer to it using a tag throughout the document. This will allow you to use the image multiple times without overloading the text with long URLs or other parameters.

```markdown
![An old rock in the desert][image1]

[image1]: ../../_images/mountain.jpg "Mountain"
```

**Result**

![An old rock in the desert][image1]

[image1]: ../../_images/mountain.jpg "Mountain"
## Videos {#video}

To add videos to a page, use markup:

```markdown
@[video_hosting_site_name](video_id_or_link_to_video)
```

To review the style options and list of available video hosting services, see the [markdown-it-video](https://www.npmjs.com/package/markdown-it-video) plugin page.
