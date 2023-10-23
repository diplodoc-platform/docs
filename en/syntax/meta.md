# Comments and metadata

Comments and metadata are markup elements that are not displayed in the built file. They're used to store information in the source text for SEO or the authors of the document.

## Comments {#comments}

To add a comment, use the following markup. Make sure there is an empty line before the comment.

```markdown
[//]: # (Comment)
```

## Metadata {#meta}

You can add metadata in YAML format at the beginning of a file. After conversion, it is returned with the resulting HTML.

```yaml
---
title: Title
description: Description
---
```

