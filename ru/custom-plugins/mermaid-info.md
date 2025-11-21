# Инструкция кастомизации Mermaid-диаграмм

## Введение

Mermaid — это инструмент для создания диаграмм и графиков на основе JavaScript, который использует определения текста на основе Markdown, и средство визуализации для создания и изменения сложных диаграмм.

В рамках этой инструкции мы подготовили несколько основных диаграмм, которые могут встречаться в документациях.

## Полезные ссылки

- [Документация Mermaid](https://mermaid.js.org/ecosystem/tutorials.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play#pako:eNqrVkrOT0lVslJKyslPztZNSi1JjMlTAIPk_JzS3LxiBUOYgGN0jFJwSWJRSYxSLEwsJb88zwYorgAUs9MA8TRhUs4aIOX5BTFKUKGYPKVaAFC4IAA "title")

{% note info %}

Данная инструкция в первую очередь описывает цветовую кастомизацию диаграмм. С логикой построения диаграмм можно ознакомиться на сайте Mermaid.

{% endnote %}

## Основные условия

- Диаграммы Mermaid применимы только на yfm-страницах.
- Любая вставка начинается с ` ```mermaid` и заканчивется ` ``` `.
- Каждая диаграмма заполняется отдельно.

## Sequence diagram

- [Документация Mermaid](https://mermaid.js.org/syntax/sequenceDiagram.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play?utm_source=mermaid_live_editor&utm_medium=banner_ad&utm_campaign=visual_editor#pako:eNptzEEKwjAQheGrvGZrc4EuKoIL6xncDPHZBNIEo0Wk9O4mqcvOamC-fxZl4p2qUy8-ZwbDs5MxyXQLyHPyzlD3_eEabehwofcRZW9h4weSiG-cj7t4Y0ZCIbCUhIl_Wm46U12b_NhtdYuhFlXnrNnnAx6kx5go70atPxjSPW8 "title")

{% cut "Скриншот диаграммы" %}

- ![Screenshot 2024-08-20 at 18.03.37.png](https://avatars.mds.yandex.net/get-bunker/56833/94b2cdf43aefdc51a382f7d4d71c640e3e8aed3a/orig =x600)

{% endcut %}

### Блок кода

```
```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#4DA0FF',
      'secondaryColor': '#0667D8',
      'noteBkgColor': '#D3DCFD'
    }
  }
}%%

sequenceDiagram
    rect rgba(233, 237, 254, 1)
    note right of Alice: Alice calls John.
    Alice->>+John: Hello John, how are you?
    rect rgba(77, 160, 255, 1)
    Alice->>+John: John, can you hear me?
    John-->>-Alice: Hi Alice, I can hear you!
    end
    John-->>-Alice: I feel great!
    Alice ->>+ John: Did you want to go to the game tonight?
    John -->>- Alice: Yeah! See you there.
    end
```
```

Параметры для цветовой кастомизации:
- `'primaryColor'::` — цветовое значение для «акторов» диаграммы «Alice» и «John» и соединяющих их линий. В соответствии с дизайн-проектом указываем `'#4DA0FF'`.
- `'secondaryColor':` — цветовое знание для блоков после стрелок. В соответствии с дизайн-проектом указываем `'#0667D8'`.
- `'noteBkgColor':` — цветовое значение для обозначения блоков формата «Alice calls John». В соответствии с дизайн-проектом указываем `'#D3DCFD'`.
- `rect rgba(233, 237, 254, 1)` — цветовое значение для подложки диаграммы. Действие ограничивается вторым `end`.
- `rect rgba(77, 160, 255, 1)` — цветовое значение для темно-синего блока посередине диаграммы. Действие ограничивается первым `end`.

## Flowchart

- [Документация Mermaid](https://mermaid.js.org/syntax/flowchart.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play?utm_source=mermaid_live_editor&utm_medium=banner_ad&utm_campaign=visual_editor#pako:eNqrVkrOT0lVslJKy8kvT85ILCpR8AmKyVMAAkcFXd18BScIxwnIqVBwjslTqgUAkRUOXw "title")


{% cut "Скриншот диаграммы" %}

![Screenshot 2024-08-20 at 18.03.45.png](https://avatars.mds.yandex.net/get-bunker/135516/2b09f92806fb378671f5f937f588d43b4178a888/orig =x289)

{% endcut %}

### Блок кода

```
```mermaid
---
title: Работа напрямую
---
flowchart LR
%% Nodes
A("DNS-сервер. 
MX указывает на шлюз"):::orange
B("Почтовый шлюз
SMTP mx.yandex.net."):::orange


%% Edges
A --> B

%% Styling
classDef orange fill:#FEEEE7,stroke:#FEEEE7,stroke-width:2px;
```
```

Параметры для цветовой кастомизации:
Для каждого «набора» цветов необходимо задавать параметры в строке

```
%% Styling
classDef orange fill:#FEEEE7,stroke:#FEEEE7,stroke-width:2px;
```

Где:

- `orange` — текстовое значение для цветового набора, которым мы задаем. Значение может быть любым.
- `fill:` — цветовое значение для блоков с текстом. В соответствии с дизайн-проектом указываем `#FEEEE7`.
- `stroke:` — цветовое значение для рамки блоков. В соответствии с дизайн-проектом указываем `#FEEEE7`.
- `stroke-width:` — ширина рамки. В соответствии с дизайн-проектом указываем `2px`.

Чтобы присвоить значения «набора» цветов для конкретного элемента, укажите название этого «набора». На примере
`A("DNS-сервер. MX указывает на шлюз"):::orange`, где `:::orange` — название цветового «набора». 

## Entity Relationship Diagram

- [Документация Mermaid](https://mermaid.js.org/syntax/entityRelationshipDiagram.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play?utm_source=mermaid_live_editor&utm_medium=banner_ad&utm_campaign=visual_editor#pako:eNp1z90KwiAYgOFbEc_tAnYWU0KoDGeDwU7MfZWwZljtZO7esx_pjzzz4_FVB2xcAzjD4KnVO68PdYfiyteFEgsm0RgmkzAgyua8ZLIiU0olKwqUob0-fdkQCHEDEpLGTYaOrTbwx_BlKXjOoqpxa_WmBbR1vsYP_XPbV9mDAdundmrdUHgh43rwT_KYvQPCFVtEZTvTXpqUWklB17ki-VSxmZBVOvKc36vdWdvu03-8L5Vr7HwDHpp4x-1jeLwCmiBtBQ "title")
- Ссылка на шаблон - TBD

{% cut "Скриншот диаграммы" %}

![Screenshot 2024-08-20 at 18.03.56.png](https://avatars.mds.yandex.net/get-bunker/135516/e981f15d23781c23b4747d11a92904ac35cf8126/orig =x529)

{% endcut %}

### Блок кода

```
```mermaid
%%{
  init: {
    'theme': 'base',
    'themeVariables': {
      'primaryColor': '#FF7F4D',
      'tertiaryColor': '#D3DCFD'
    }
  }
}%%

erDiagram
    CUSTOMER ||--o{ ORDER : places
    ORDER ||--|{ LINE-ITEM : contains
    CUSTOMER }|..|{ DELIVERY-ADDRESS : uses
```
```

Параметры для цветовой кастомизации:

- `'primaryColor':` — цветовое значение для основных блоков с текстом. В соответствии с дизайн-проектом указываем `'#FF7F4D'`.
- `'tertiaryColor':` — цветовое значение для второстепенных блоков с текстом, которые расположены на стрелках. В соответствии с дизайн-проектом указываем `'#D3DCFD'`.

## Mindmaps

- [Документация Mermaid](https://mermaid.js.org/syntax/flowchart.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play?utm_source=mermaid_live_editor&utm_medium=banner_ad&utm_campaign=visual_editor#pako:eNpdkMFOw0AMRH_Fyik5IO4VQmq5glqVcuvF3Tgbi8RevLuVUsS_k5KmQH3zm_Fo5M_CaU3FouhZ6h7DXgBMNZXlBVTVGQGsjT1LnBaAZxUPLcekNsxssWCnUjYIDd4dVN-rWdloyB0anzCxykwBVsaJYwth0iHEwbXaqR8Ac2rVYKcywCqf8HK1pUhorp0z1gLUNOQSH0koxoeD3T-i1NAQpmwU_xiXOWk_NnDgjG6avMVf6zRPP54jQSLXCn_kW8NrMkzkx7jQoQiL_68vzeeeJMH4xXBVd6rdNWhDAueyAQPZDF_IeuR6L8XXN7kLgpw "title")

{% cut "Скриншот диаграммы" %}

![Screenshot 2024-08-27 at 16.10.40.png](https://avatars.mds.yandex.net/get-bunker/56833/58b05a5962a5d3a1265f0a17caaa4078262e9b65/orig =x600)

{% endcut %}

### Блок кода

```
```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      Popularization
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```
```

{% note info %}

Цветовая кастомизация Mindmaps происходит через кастомные css-стили.

{% endnote %}

## Block Diagram

- [Документация Mermaid](https://mermaid.js.org/syntax/block.html "title")
- [Песочница Mermaid](https://www.mermaidchart.com/play?utm_source=mermaid_live_editor&utm_medium=banner_ad&utm_campaign=visual_editor#pako:eNqrVkrOT0lVslJKyslPztZNSi1JjMlTAIPk_JzS3LxiBUOYgGN0jFJwSWJRSYxSLEwsJb88zwYorgAUs9MA8TRhUs4aIOX5BTFKUKGYPKVaAFC4IAA "title")


{% cut "Скриншот диаграммы" %}

![Screenshot 2024-08-20 at 18.04.08.png](https://avatars.mds.yandex.net/get-bunker/135516/3d524554e290cea698c68ea0f97ec9086fdac8f6/orig =x190)

{% endcut %}

### Блок кода

```
```mermaid
graph TD
A["Start"]
A --> C["Stop"]
style A fill:#FEEEE7,stroke:#FEEEE7,stroke-width:4px
style C fill:#FEEEE7,stroke:#FEEEE7,stroke-width:4px
```
```

Цветовые значения в этой диаграмме задаются для каждого отдельного блока через строку вида:
- `style A` — название блока, который нужно перекрасить.
- `fill:` — цветовое значение для блока. В соответствии с дизайн-проектом указываем `#FEEEE7`.
- `stroke:` — цветовое значение для рамки блока.
- `stroke-width:` — значение ширины рамки. По умолчанию указываем `4px`.

{% note info %}

На текущий момент Diplodoc умеет поддерживать диаграмму вида «graph TD». Если указать «block-beta», как это указано в документации, диаграмма не соберется.

{% endnote %}
