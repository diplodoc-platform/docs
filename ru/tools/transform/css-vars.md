# CSS переменные

Пакет предоставляет набор css переменных, которые вы можете переопределить исходя из своих потребностей


| Переменная | Значение по умолчанию | Пример |
| :--------- | :-------------------: | :----- |
| _common_ | | |
|`--yfm-color-base` | <span style="display:block;background-color:var(--yfm-color-base-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Background-color у таблиц, можно смотреть на примере этой |
`--yfm-color-text` | <span style="display:block;background-color:var(--yfm-color-text-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | В `.yfm` классе дефолтный color |
`--yfm-color-link` | <span style="display:block;background-color:var(--yfm-color-link-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Любая ссылка `<a>` |
`--yfm-color-link-hover` | <span style="display:block;background-color:var(--yfm-color-link-hover-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Hover состояние ссылки `<a>` |
`--yfm-color-table` | <span style="display:block;background-color:var(--yfm-color-table-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Дефолтный color в таблице |
`--yfm-color-table-row-background` | <span style="display:block;background-color:var(--yfm-color-table-row-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Background-color для каждой второй строки в таблице |
`--yfm-color-border` | <span style="display:block;background-color:var(--yfm-color-border-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Границы таблицы |
`--yfm-color-accent` | <span style="display:block;background-color:var(--yfm-color-accent-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Цвет для тега `<hr>` или левая граница цитаты |
| _code_ | | |
`--yfm-color-inline-code` | <span style="display:block;background-color:var(--yfm-color-inline-code-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Цвет в блоке [code](../../syntax/code.md)|
`--yfm-color-inline-code-background` | <span style="display:block;background-color:var(--yfm-color-inline-code-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Background-color блока [inline-code](../../syntax/code.md#inline) |
`--yfm-color-code-background` | <span style="display:block;background-color:var(--yfm-color-code-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" /> | Background-color блока [code](../../syntax/code.md#block) |
| _hljs_ | | |
`--yfm-color-hljs-background` | <span style="display:block;background-color:var(--yfm-color-hljs-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-subst` | <span style="display:block;background-color:var(--yfm-color-hljs-subst-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-comment` | <span style="display:block;background-color:var(--yfm-color-hljs-comment-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-deletion` | <span style="display:block;background-color:var(--yfm-color-hljs-deletion-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-section` | <span style="display:block;background-color:var(--yfm-color-hljs-section-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-pseudo` | <span style="display:block;background-color:var(--yfm-color-hljs-pseudo-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-literal` | <span style="display:block;background-color:var(--yfm-color-hljs-literal-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-addition` | <span style="display:block;background-color:var(--yfm-color-hljs-addition-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-meta` | <span style="display:block;background-color:var(--yfm-color-hljs-meta-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-hljs-meta-string` | <span style="display:block;background-color:var(--yfm-color-hljs-meta-string-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
| _note_ | | Примеры можно посмотреть на [странице](../../syntax/notes.md) документации заметок|
`--yfm-color-note-tip` | <span style="display:block;background-color:var(--yfm-color-note-tip-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-tip-background` | <span style="display:block;background-color:var(--yfm-color-note-tip-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-warning` | <span style="display:block;background-color:var(--yfm-color-note-warning-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-warning-background` | <span style="display:block;background-color:var(--yfm-color-note-warning-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-important` | <span style="display:block;background-color:var(--yfm-color-note-important-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-important-background` | <span style="display:block;background-color:var(--yfm-color-note-important-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-note-info-background` | <span style="display:block;background-color:var(--yfm-color-note-info-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
| _term_ | | Примеры можно посмотреть на [странице](../../syntax/term.md) документации всплывающих подсказок|
`--yfm-color-term-title` | <span style="display:block;background-color:var(--yfm-color-term-title-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-term-title-hover` | <span style="display:block;background-color:var(--yfm-color-term-title-hover-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-term-dfn-background` | <span style="display:block;background-color:var(--yfm-color-term-dfn-background-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-term-dfn-shadow` | <span style="display:block;background-color:var(--yfm-color-term-dfn-shadow-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-term-dfn-pseudo-shadow` | <span style="display:block;background-color:var(--yfm-color-term-dfn-pseudo-shadow-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
| _modal_ | | |
`--yfm-color-modal-content` | <span style="display:block;background-color:var(--yfm-color-modal-content-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-modal-actions-hover` | <span style="display:block;background-color:var(--yfm-color-modal-actions-hover-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-modal-wide-content` | <span style="display:block;background-color:var(--yfm-color-modal-wide-content-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />
`--yfm-color-modal-wide-content-overlay` | <span style="display:block;background-color:var(--yfm-color-modal-wide-content-overlay-private);width:20px;height:20px;border: 0.5px solid black;border-radius: 50%;" />