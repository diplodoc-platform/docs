# Библиотека Mermaid

Mermaid — это наиболее популярная и современная библиотека для создания диаграмм и блок-схем в браузере с помощью простого языка разметки. Она позволяет создавать диаграммы, используя синтаксис, похожий на Markdown. 

Библиотека имеет множество встроенных шаблонов и функций для создания различных типов диаграмм, например: блок-схемы, графы, деревья, диаграммы Ганта, mind-карты, C4-диаграммы.

Список поддерживаемых диаграмм постоянно пополняется, и с ним можно ознакомиться в [официальной документации](https://mermaid.js.org/intro/).

## Расширение Diplodoc Mermaid

Это расширение для платформы Diplodoc, которое позволяет поддерживать диаграммы Mermaid.

Расширение содержит несколько частей:

* [среда выполнения Mermaid](#runtime);
* [плагин преобразования Markdown](#plugin);
* [React hook и компонент для интеллектуального управления Mermaid](#react).

### Быстрый старт

1. Подключите расширение:

    ```
   import mermaid from '@diplodoc/mermaid-extension';
   import transform from '@diplodoc/transform';
   
    const {result} = await transform(`
   \`\`\`mermaid
   graph TD
       A[Christmas] -->|Get money| B(Go shopping)
   \`\`\`
   `, {
       plugins: [
           mermaid.transform({ bundle: false })
       ]
   });
   ```

2. Подключите среду выполнения Mermaid на вашу страницу:

   ```html
   <html>
       <head>
           <!-- Информацию о '_assets/mermaid-extension.js' смотрите в разделе 'Плагин преобразования Markdown' -->
           <script src="_assets/mermaid-extension.js" async />
       </head>
       <body style="background: #000">
          ${result.html}
           <script>
               // Информация о 'mermaidJsonp' в разделе 'среда выполнения Mermaid' 
               window.mermaidJsonp = window.mermaidJsonp || [];
               window.mermaidJsonp.push((mermaid) => {
                   mermaid.initialize({ theme: 'dark' });
                   mermaid.run();
               });
           </script>
       </body>
   </html>   
   ```

### Cреда выполнения Mermaid {#runtime}

Сложность работы с библиотекой Mermaid в том, что у нее большой размер пакета. Наиболее ожидаемым поведением является его асинхронная загрузка. Но если необходимо отключить опцию `startdownload` для Mermaid, то неизвестно, когда Mermaid будет инициализирован.

Подготовленная среда выполнения Mermaid предназначена для решения этой проблемы. В ней отключена опция `startOnLoad` в Mermaid, чтобы точно контролировать шаг рендеринга. Затем добавляется глобальный обратный вызов `mermaidJsonp` для обработки загрузки Mermaid.

Кроме того, доступ к API Mermaid ограничивается двумя способами:

* инициализация - настройка Mermaid перед следующим запуском рендеринга;
* запуск рендеринга диаграмм.

Пример:

```
window.mermaidJsonp = window.mermaidJsonp || [];

// This callback will be called when runtime is loaded
window.mermaidJsonp.push((mermaid) => {
    mermaid.initialize({ theme: 'dark' });
    mermaid.run();
});

// You can configure more that one callback
window.mermaidJsonp.push((mermaid) => {
    console.log('Render diagrams');
});
```

#### Пользовательские параметры инициализации 

Метод `mermaid.initialize` имеет дополнительные параметры конфигурации:

* `zoom` - включает функцию масштабирования диаграммы и ее изучения. Может быть логическим значением или объектом с внутренними реквизитами. Значение по умолчанию: false.
* `showMenu` - показывает навигационное меню. Значение по умолчанию: false.
* `bindKeys` - включает элементы управления `wasd`. Значение по умолчанию: false. Используйте параметры `w/a/s/d` для просмотра диаграммы, `e/q` для увеличения или уменьшения масштаба и `r` для изменения положения диаграммы. 
* `maximumScale` - максимальный размер масштабирования. Значение по умолчанию: 5.
* `resetOnBlur` - сброс положения диаграммы по щелчку мыши. Значение по умолчанию: false.


### Плагин преобразования Markdown {#plugin}

Конфигурация плагина для пакета `@diplodoc/transform`:

* `runtime` - имя скрипта времени выполнения, который будет отображаться в разделе `results script`. Значение по умолчанию: `_assets/mermaid-extension.js`.

* `bundle` - логический флаг для включения/отключения копирования связанной среды выполнения в целевой каталог. Значение по умолчанию: true.
    Чтобы узнать где находится целевой каталог выполните `<transformer output option>/<plugin runtime option>`

* `classes` - дополнительные классы, которые будут добавлены к диаграммам Mermaid. Например: `my-own-class and-other-class`.


### React hook и компонент для интеллектуального управления Mermaid {#react}

Упрощенное управления Mermaid с помощью react:

```
import React from 'react'
import { transform } from '@diplodoc/transform'
import mermaid from '@diplodoc/mermaid-extension/plugin'
import { MermaidRuntime } from '@diplodoc/mermaid-extension/react'

const MERMAID_RUNTIME = 'extension:mermaid';

const Doc: React.FC = ({ content }) => {
    const result = transform(content, {
      plugins: [
        // Инициализируйте плагин для рендеринга клиент/сервер
        mermaid.transform({
          // Не изменять файловую систему
          bundle: false,
          // Установите пользовательское имя среды выполнения для поиска в результирующих скриптах
          runtime: MERMAID_RUNTIME
        })
      ]
    })
  
    // Загружайте Mermaid только в том случае, если необходимо отобразить одну или несколько диаграмм
    if (result.script.includes(MERMAID_RUNTIME)) {
      // Слишком большую среду выполнения Mermaid загружайте асинхронно
      import('@diplodoc/mermaid-extension/runtime')
    }
  
    return <div dangerouslySetInnerHTML={{ __html: result.html }} />
}

export const App: React.FC = ({ theme }) => {
    return <>
        <Doc content={`
            \`\`\`mermaid
            graph TD
                A[Christmas] -->|Get money| B(Go shopping)
                B --> C{Let me think}
            \`\`\`
        `}/>
        <MermaidRuntime
            zoom={{
              showMenu: true,
              bindKeys: true,
              resetOnBlur: true,
            }}
        />
    </>
}
```