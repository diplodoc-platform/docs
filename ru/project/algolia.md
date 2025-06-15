## Поиск с Algolia

[Algolia](https://www.algolia.com/) — облачная система поиска для быстрого и релевантного поиска по документации Diplodoc. Подходит для больших объемов данных, обеспечивает мгновенную выдачу результатов и легко интегрируется во фронтенд документации.

**Исходный код и дополнительные инструкции расширения Algolia:**
[https://github.com/diplodoc-platform/algolia-extension](https://github.com/diplodoc-platform/algolia-extension)

> Для регистрации аккаунта Algolia может понадобиться VPN.

## Быстрый старт

1. **Зарегистрируйтесь в Algolia**  
   Перейдите на [algolia.com](https://www.algolia.com/) и создайте аккаунт. После этого получите App ID, Write API Key и Search API Key для вашего приложения.  
   _(Подробнее см. раздел [“Регистрация и настройки Algolia”](#registraciya-i-nastrojki-algolia))_

2. **Установите Diplodoc CLI и расширение Algolia (глобально)**  
   ```bash
   npm install -g @diplodoc/cli
   npm install -g @diplodoc/algolia-extension
   ```
   _(Подробнее о вариантах установки — в разделе [“Установка”](#ustanovka))_

3. **Сконфигурируйте поиск в `.yfm`**  
   В корневом `.yfm` пропишите:
   ```yaml
   search:
     provider: algolia
     appId: <ваш app id>
     searchApiKey: <ваш search key>
     index: true
   ```
   _(Пример с расширенными настройками — см. [“Пример расширенной настройки”](#primer-rasshirennoj-nastrojki))_

4. **Передайте ключи и запустите сборку**  
   Для безопасной сборки передавайте Write API Key через флаг CLI:
   ```bash
   yfm -i ./docs -o ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
   ```

### Регистрация и настройки Algolia

1. Зарегистрируйтесь на [algolia.com](https://www.algolia.com/) (может потребоваться VPN).
2. В панели Algolia создайте приложение (Application) и получите:
   - **App ID** ― идентификатор приложения
   - **Write API Key** ― секретный ключ для индексации данных
   - **Search API Key** ― ключ для поиска на клиенте
3. Имя индекса (`indexName`) можно не задавать, по умолчанию `"docs"`.

### Установка

Существует два варианта установки расширения для поиска Algolia:

- **Глобальная установка** — подходит для большинства типовых сценариев, если вы просто хотите собрать документацию с поддержкой облачного поиска.
- **Локальная установка в репозитории** — рекомендуется, если вы используете собственные плагины, дорабатываете cli или работаете в команде с общим package.json.

**Глобальная установка:**
```bash
npm install -g @diplodoc/cli
npm install -g @diplodoc/algolia-extension
```
Запуск сборки с расширением:
```bash
yfm -i ./docs -o ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
```

**Локальная установка в проекте @diplodoc/cli:**
```bash
npm install @diplodoc/algolia-extension
```
Запуск сборки с расширением:
```bash
npm start -- -i ./docs -o ./docs-out --extensions @diplodoc/algolia-extension --api-key "your-write-key"
```

### Источники для передачи параметров

Параметры расширения можно задавать через CLI, переменные окружения и файл `.yfm`:

| Параметр      | CLI-флаг            | Переменная среды       | .yfm                       | Назначение                               |
|---------------|---------------------|------------------------|----------------------------|------------------------------------------|
| provider      | --search-provider   | ALGOLIA_PROVIDER       | search.provider            | Провайдер поиска (`algolia`)             |
| appId         | --app-id            | ALGOLIA_APP_ID         | search.appId               | Algolia App ID                           |
| apiKey        | --api-key           | ALGOLIA_API_KEY        | search.apiKey (см. выше)   | Секретный ключ для индексации            |
| indexName     | --index-name        | ALGOLIA_INDEX_NAME     | search.indexName           | Имя индекса (по умолчанию "docs")        |
| index         | --index             | -                      | search.index               | Загружать ли индекс в Algolia            |
| searchApiKey  | --search-api-key    | ALGOLIA_SEARCH_API_KEY | search.searchApiKey        | Ключ для поиска на клиенте               |
| api           | --search-api        | ALGOLIA_API_PATH       | search.api                 | Путь к JS-API поиска                     |
| indexSettings | -                   | -                      | search.indexSettings       | Настройки индекса Algolia                |
| querySettings | -                   | -                      | search.querySettings       | Настройки поисковых запросов             |


{% note warning "Пояснение по видам ключей" %}

- **apiKey (Write API Key):**
  Секретный ключ, используется для загрузки и обновления данных в Algolia во время сборки или индексации. Храните его секретно, не публикуйте в репозитории или выложенных файлах конфигурации: используйте переменные среды либо флаги CLI.

- **searchApiKey (Search API Key):**
  Ключ для фронтенд-поиска, попадает в финальную сборку документации. Без него поиск на клиенте работать не будет. Этот ключ безопасен для публикации в файле `.yfm`.

{% endnote %}

### Пример расширенной настройки

```yaml
search:
  provider: algolia
  appId: <ваш app id>
  indexName: docs
  index: true
  searchApiKey: <ваш search api key>
  indexSettings:
    searchableAttributes:
      - title
      - content
      - headings
      - keywords
    attributesToHighlight:
      - title
      - content
  querySettings:
    hitsPerPage: 10
    attributesToRetrieve:
      - title
      - content
      - url
      - section
```

### Сборка и индексация

- По умолчанию расширение создает локальные индексы в каталоге `_search` вашей выходной папки. Эти индексы доступны для локального поиска и не загружаются в облако.
- Если в конфиге задан параметр `index: true` (или используется CLI-флаг `--index`), то при каждой сборке документации индекс будет не только формироваться локально, но и автоматически загружаться (обновляться) в Algolia после сборки.
- Если вы хотите разделить эти процессы — например, сначала собрать документацию, проверить результат, а индекс загружать только после финальной проверки или отдельно по расписанию — настройте сборку без параметра `index` (или явно с `index: false`). Тогда при сборке создаются только локальные индексы. Позднее для загрузки или обновления индекса в облако используйте отдельную команду:

```bash
yfm index -i ./docs-out --extensions "$(npm root -g)/@diplodoc/algolia-extension" --api-key "your-write-key"
```

#### Частые вопросы и проблемы

- Поиск не работает — проверьте, что `searchApiKey` корректно передан в конфиге.
- Ошибка при индексации — проверьте правильность и способ передачи `write apiKey`.
- Данные не появляются в Algolia — убедитесь, что выставлен параметр `index: true` в конфиге или используется ключ `--index` при запуске.
