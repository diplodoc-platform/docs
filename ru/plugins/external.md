# Внешние плагины

## Подключение {#require}

Отличие внешних плагинов от встроенных в том, что перед подключением их нужно предварительно установить (`npm install`), а затем — добавить в секцию плагинов `mdit-plugins`.

Для внешних плагинов в поле `plugins` указывется имя плагина.

### Пример подключения

**Установка и настройка плагина [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex)**.

Плагин позволяет отображать математические формулы.

1. Склонируйте репозиторий CLI:

    ```bash
    git clone https://github.com/diplodoc-platform/cli.git
    ```

2. Установите зависимости и соберите проект:

    ```bash
    npm i && npm run build
    ```

3. Установите парсер и пакет с плагином:

   ```bash
   npm install markdown-it
   ```

   ```bash
   npm install i markdown-it-katex
   ```

4. Добавьте в файл `.yfm` следующую конфигурацию:

   ```yaml
   extensions:
   - name: mdit-plugins
      plugins:
         - "markdown-it-katex"
   ```

**Использование:**

```markdown
$\sqrt{3x-1}+(1+x)^2$
```

**Результат:**

$\sqrt{3x-1}+(1+x)^2$
