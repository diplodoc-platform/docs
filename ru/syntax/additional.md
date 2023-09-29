# Дополнительные возможности

Ниже перечислены элементы разметки, которые не поддерживаются по умолчанию, но могут быть подключены с помощью [плагинов markdown-it](https://www.npmjs.com/search?q=keywords:markdown-it-plugin).

О том, как подключить дополнительный плагин, читайте в [инструкции](../plugins/import.md).

## Нижний регистр {#sub}

**Плагин:** [markdown-it-sub](https://www.npmjs.com/package/markdown-it-sub)

Чтобы вывести символ в нижнем регистре, добавьте с двух сторон `~`.

```markdown
H~2~O
```

Проголосовать за поддержку нижнего регистра в YFM по умолчанию можно в [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/70).

## Подчеркнутый текст {#underline}

**Плагин:** [markdown-it-ins](https://www.npmjs.com/package/markdown-it-ins)

Чтобы подчеркнуть текст, добавьте с двух сторон `++`.

```markdown
++qwerty++
```

Проголосовать за поддержку подчеркнутого текста в YFM по умолчанию можно в [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/71).

## Сноски {#footnotes}

**Плагин:** [markdown-it-footnote](https://www.npmjs.com/package/markdown-it-footnote)

Используйте сноски, если необходимо указать дополнительную информацию, не усложняя текст. Сноски состоят из двух частей, связанных метками:

* ссылка в тексте документа, которая отображается в верхнем индексе;
* блок дополнительной информации. Обычно размещается в конце документа.

```markdown
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.
```

Проголосовать за поддержку сносок в YFM по умолчанию можно в [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/72).

## Списки задач {#tasks-list}

Импортируйте плагин из пакета следующий образом:
```
const checkbox = require('@diplodoc/transform/lib/plugins/checkbox');
```

Список задач представляет из себя список чекбоксов. Обычному элементу соответствует символ `- [ ]` , отмеченному — `- [x]`. В описании задачи можно использовать [строчное форматирование](./base.md#line).

```markdown
- [x] ~~Write the press release~~
- [ ] Update the website
- [ ] Contact the media
```

Проголосовать за поддержку списков задач в YFM по умолчанию можно в [GitHub issues](https://github.com/yandex-cloud/yfm-transform/issues/73).

## Формулы {#formulas}

**Плагин:** [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex) (см. [другие версии](https://www.npmjs.com/search?q=markdown-it-katex))

Плагин использует библиотеку KaTeX для отображения математических обозначений. Пример формулы:

```markdown
$\sqrt{3x-1}+(1+x)^2$
```
