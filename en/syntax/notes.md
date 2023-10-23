# Notes

A note is a highlighted block that contains important information.

Depending on the content, notes with different titles and formatting are used:

* Note: Additional information.
* Advice: A recommendation.
* Important: A warning.
* Attention: A restriction.
* A note with its own header.

Notes can include any YFM markup, but we don't recommend overloading them with elements. Choose a simple design and don't overuse notes because this will distract the user from the main content.

## Comment

```markdown
{% note info %}

This is info.

{% endnote %}
```

**Result**

{% note info %}

This is info.

{% endnote %}

## Tip

```markdown
{% note tip %}

This is a tip.

{% endnote %}
```

**Result**

{% note tip %}

This is a tip.

{% endnote %}

{% endcut %}

## Warning

```markdown
{% note warning %}

This is a warning.

{% endnote %}
```

**Result**

{% note warning %}

This is a warning.

{% endnote %}

## Alert

```markdown
{% note alert %}

This is an alert.

{% endnote %}
```

**Result**

{% note alert %}

This is an alert.

{% endnote %}

## Custom header

```markdown
{% note info "Custom header" %}

This is a note with its own header.

{% endnote %}
```

**Result**

{% note info "Custom header" %}

This is a note with its own header.

{% endnote %}

```markdown
{% note info "" %}

This is a note without a header.

{% endnote %}
```

**Result**

{% note info "" %}

This is a note without a header.

{% endnote %}

