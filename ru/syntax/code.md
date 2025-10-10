# Фрагменты кода

Фрагмент кода можно добавить в текст или вынести в отдельный блок.

## В тексте {#inline}

Чтобы добавить фрагмент кода в текст, используйте символ `.
```markdown
`Фрагмент кода` в тексте.
```

**Результат:**

`Фрагмент кода` в тексте.

{% include [not_var](../_includes/not_var-info.md) %}

{% note tip %}

Рекомендуется использовать не более 100 символов, так как текст в таком фрагменте не переносится. Для большего числа символов оформите код отдельным блоком.

{% endnote %}

## Отдельным блоком {#block}

Чтобы оформить фрагмент кода как отдельный блок, отделите его от остального текста с двух сторон символами ```.

Для подсветки синтаксиса укажите в начальной строке язык, на котором написан код. Например:

````markdown
```sql
  price= '2000'
  size= '24'  
  color= 'primary'
  variant= 'detailed' 
```
````

{% cut "Список поддерживаемых языков" %}

* apache;
* bash;
* coffeescript;
* cpp;
* cs;
* css;
* diff;
* go;
* http;
* ini;
* java;
* javascript;
* json;
* kotlin;
* less;
* lua;
* makefile;
* xml;
* markdown;
* nginx;
* objectivec;
* perl;
* php;
* plaintext;
* properties;
* python;
* ruby;
* rust;
* scss;
* shell;
* sql;
* swift;
* typescript;
* **yaml**.

{% endcut %}

Ознакомиться с полным перечнем доступных языков можно в [GitHub](https://github.com/highlightjs/highlight.js/tree/master/src/languages).

### Отображение номеров строк {#line-numbers}

Если необходимо включить отображение номеров строк в блоке кода, используйте ключевое слово `showLineNumbers`.

Пример использования:

````markdown
```sql showLineNumbers
  price = '2000'
  size = '24'  
  color = 'primary'
  variant = 'detailed' 
```
````

**Результат:**

```sql showLineNumbers
  price = '2000'
  size = '24'  
  color = 'primary'
  variant = 'detailed' 
```
