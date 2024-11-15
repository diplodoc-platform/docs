# Ссылки

Стандартная разметка для ссылки имеет вид:
```
[текст_ссылки](ссылка "текст_подсказки")
```

  * `текст_ссылки` — явное указание текста ссылки.
  * `ссылка` — URL или путь до файла.
  * `"текст_подсказки"` — подсказка, которая будет отображаться при наведении на текст ссылки. Необязательный параметр.

В зависимости от вида ссылки допускаются упрощения и другие варианты оформления.

## Ссылка на md-файл {#autotitle}

Вы можете оформить ссылку на md-файл без явного указания текста ссылки. Для этого добавьте сочетание символов `{#T}` на место текста, и он подставится автоматически из заголовка указанного файла.

```markdown
[{#T}](./index.md)
```

**Результат**

[{#T}](./index.md)

## Ссылка на раздел в md-файле {#auto-section-title}

Вы можете сослаться:

* На раздел текущей страницы.

  `[text](#anchor)`

  **Результат**
  
  [{#T}](#formatting)

* На раздел другой страницы.

  `[text](base.md#anchor)`

  **Результат**

  [{#T}](base.md#headers)

## URL или адрес электронной почты {#url-email}

Чтобы преобразовать URL или адрес электронной почты в ссылку, добавьте с двух сторон угловые скобки `<>`.

```markdown
<https://yandex.com/>

<alice.the.girl@yandex.com>
```

**Результат**

<https://yandex.com/>

<alice.the.girl@yandex.com>

## Reference-style разметка для ссылок {#reference-style}

Используйте reference-style ссылки, чтобы упростить восприятие исходного текста документа. Ссылки такого типа состоят из двух частей, связанных метками:
* краткое описание ссылки в тексте.
  
  `[текст_ссылки][метка_ссылки]`

* длинный URL, размещенный в специальном месте в конце параграфа или документа. 
  
  `[метка_ссылки]: URL`

```markdown
My favorite search engine is [Yandex][1].

[1]: https://yandex.com/ "The best search engine"
```

**Результат**

My favorite search engine is [Yandex][1].

[1]: https://yandex.com/ "The best search engine"

## Начертание текста ссылки {#formatting}

К тексту ссылки можно применять [строчное форматирование](./base.md#line).

```markdown
I love the **[Yandex Cloud](https://cloud.yandex.com)**.
This is the _[YFM Guide](https://yadocs.tech)_.
See the section on [`code`](#code).
Super [^men^](https://en.wikipedia.org/wiki/Major_Grom_(2017_film)).
```

**Результат**

I love the **[Yandex Cloud](https://cloud.yandex.com)**.
This is the _[YFM Guide](https://yadocs.tech)_.
See the section on [`code`](#code).
Super [^men^](https://en.wikipedia.org/wiki/Major_Grom_(2017_film)).

## Файлы {#files}

Если требуется указать ссылку на файл, можно воспользоваться специальной ссылкой с иконкой файла. После клика на такую ссылку браузер начнёт скачивать указанный файл на устройство.

```markdown
{% file src="data:text/plain;base64,Cg==" name="empty.txt" %}
```

{% file src="../../_images/cover.png" %}

{% file src="notes.md" %}

{% file src="./notes.md" %}
