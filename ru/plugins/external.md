# Внешние плагины

## Подключение {#require}

Отличие внешних плагинов от встроенных в том, что перед подключением их нужно предварительно установить (`npm install`), а затем — добавить в секцию плагинов `mdit-plugins`.

Для внешних плагинов в поле `plugins` указывется имя плагина.

### Примеры подключения популярных плагинов

#### Установка и настройка плагина [markdown-it-emoji](https://www.npmjs.com/package/markdown-it-emoji)

Плагин добавляет поддержку синтаксиса эмодзи и смайликов.

1. Склонируйте репозиторий CLI:

    ```bash
    git clone https://github.com/diplodoc-platform/cli.git
    ```

2. Установите зависимости и соберите проект:

    ```bash
    npm i && npm run build
    ```

3. Установите пакет с плагином:

   ```bash
   npm install i markdown-it-emoji
   ```

4. Добавьте в файл `.yfm` следующую конфигурацию:

   ```yaml
   extensions:
   - name: mdit-plugins
      plugins:
         - "markdown-it-emoji"
   ```

**Использование:**

```markdown
:smile: :heart: :thumbsup: :satellite:
```

**Результат:**

:smile: :heart: :thumbsup: :satellite:

#### Математические формулы

Плагин [markdown-it-katex](https://www.npmjs.com/package/markdown-it-katex) позволяет отображать математические формулы.

**Установка:**

```bash
npm install i markdown-it-katex
```

**Подключение:**

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
