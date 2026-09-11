# Audience-specific content

Use `visibility` blocks to keep human-oriented explanations and instructions for AI agents in one Markdown source.

Content outside a `visibility` block is common to both audiences. Use `human` for content shown only in the regular documentation and `agent` for content included only in machine-oriented representations:

```markdown
This paragraph is available to everyone.

:::visibility human
Use the button in the upper-right corner to create a project.
:::

:::visibility agent
Create a project by sending `POST /projects` with the required fields.
:::
```

The regular HTML and Markdown output includes common and `human` content. Agent-oriented output, such as `llms-full.txt`, includes common and `agent` content. The directive markers themselves are not included in either result.

Only the exact lowercase values `human` and `agent` are supported. YFM lint reports an invalid or missing value as an error, while rendering remains fail-closed and omits the invalid block.

During localization, both variants are translated and the `visibility` markers are preserved.

## Machine-readable representations

A regular HTML page and its Markdown companion use the human audience by default. Add `?audience=agent` to request the agent variant or `?audience=human` to select the human variant explicitly. If the opposite specific variant exists, a Markdown companion response includes an HTTP `Link` header with `rel="alternate"` and the URL of that variant.

The JSON document API supports the audience parameter for both rendered and raw content, for example `?format=json&audience=agent` and `?format=json&content=raw&audience=agent`. The response contains:

- `audience`: the audience applied to `content`.
- `audienceSpecificContent`: the specific block types found in the article, in stable `human`, `agent` order. For example, `[]` means that there are no audience-specific blocks and `["human", "agent"]` means that both types are present.
