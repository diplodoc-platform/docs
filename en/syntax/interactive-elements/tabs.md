# Tabs

Use tabs for mutually exclusive sections. For example, to separate instructions for different operating systems.

{% include [blank-lines](../../_includes/blank-lines-note.md) %}

```markdown
{% list tabs %}

- Tab 1 title

  Tab 1 text.

  * You can use lists.
  * And **other** markup.

- Tab 2 title

  Tab 2 text.

{% endlist %}
```

**Result:**

{% list tabs %}

- Tab 1 title

  Tab 1 text.

  * You can use lists.
  * And **other** markup.

- Tab 2 title

  Tab 2 text.

{% endlist %}

<video controls playsinline preload="metadata" poster="en/_assets/screencaster/tabs-en.png" style="width:100%">
  <source src="en/_assets/screencaster/tabs-en.mp4" type="video/mp4" />
  <track kind="subtitles" src="en/_assets/screencaster/tabs-en.vtt" srclang="en" label="English" default />
</video>

Video generated with [Diplodoc Screencaster](../../guides/screencaster.md).

{% include [common-params](../../_includes/common-params-note.md) %}
