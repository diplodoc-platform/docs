# Variables

You can declare a variable in one of the following ways:

* Pass it in the settings when [building documentation](../tools/docs/index.md#use).
* Describe it in a [file with variable presets](../project/presets.md).

Methods for using variables in documents are discussed below.

## Substitutions {#subtitudes}

To substitute a value with a variable in the text, enter the variable name with double curly brackets before and after.

```
Some text not_var{{ variable_name }} text continued.
```

If the text contains double curly brackets but doesn't require variable substitution, add `not_var` before the construction.

```
Some text not_varnot_var{{ also_text }} text continued.
```

## Conditional operators {#conditions}

Use the conditional operators `if`, `else`, and `elsif` to include certain text fragments in the document depending on variable values. For example, to build two versions of a document for different operating systems.

```markdown
{% if  OS == 'iOS' %}

Download the app from the [App Store](https://www.apple.com/ios/app-store/).

{% else %}

Download the app from [Google Play] (https://play.google.com).

{% endif %}
```

You can also apply conditional operators to text fragments inside strings.

```markdown
Some text {% if  OS == 'iOS' %} Apple {% else %} Android {% endif %} text continued.
```

## Cycles {#cycles}

Use loops to output repetitive content for each element of an array. Inside the loop, refer to the element as a regular variable, using syntax for [substitutions](#subtitudes).

```
{% for variable_name in array_name %}

Some text not_var{{ variable_name }} text continued.

{% endfor %}
```

{% cut "Examples of using loops" %}

Let's say that in a [file with variable presets](../project/presets.md), the `users` array is set:

```yaml
default:
  users:
    - Alice
    - Mark
```

Then using loops will result in the following:

```markdown
Prefix {% for user in users %} not_var{{user}} {% endfor %} Postfix
```

Prefix Alice Mark Postfix

```markdown
Prefix

{% for user in users %}

not_var{{user}}

{% endfor %}

Postfix
```

Prefix
Alice
Mark
Postfix

{% endcut %}

## Filters {#filters}

To apply a filter, add the `|` operator and the filter name to the variable. Separate the operator with spaces before and after.

| Filter | Description |
| --- | --- |
| `capitalize` | Makes the first letter in the variable value upper case. |
| `length` | Calculates the length of the variable value. |

{% cut "Examples of using filters" %}

Let's say the following is set in a [file with variable presets](../project/presets.md):

```yaml
default:
  user:
    name: alice
  users:
    - Alice
    - Mark
```

Then using filters will result in the following:

```markdown
Hello not_var{{ user.name | capitalize }}!
```

Hello Alice!

```markdown
not_var{{ users | length }}

not_var{{ user.name | length }} | length
```

2

5

{% endcut %}

## Functions {#functions}

To invoke a function, add the `.` symbol to the variable, specify its name, and pass the necessary parameters in parentheses `()`.

| Function | Description | Parameters |
| --- | --- | --- |
| `slice(beginIndex, endIndex)` | Returns the specified part of the source array as a new array object. | `beginIndex` is an index of the element the selection begins with (numbering starts with 0).</br></br>`endIndex` is an index of the element the selection ends with (numbering starts with 0). If the parameter is omitted, all elements from the starting position to the end of the array are selected. |

{% cut "Examples of using functions" %}

Let's say the following is set in a [file with variable presets](../project/presets.md):

```yaml
default:
  user:
    name: Masha
```

Then using functions will result in the following:

```markdown
Hello Pnot_var{{ user.name.slice(1) }}!

Hello Pnot_var{{ user.name.slice(1, 2) }}vel!
```

Hello Pasha!

Hello Pavel!

{% endcut %}
