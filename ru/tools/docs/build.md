# Сборка документации

Cборка проекта выполняется командой `yfm build` с параметрами:

* `--input, -i` — путь до директории проекта (по умолчанию — текущая папка);
* `--output, -o` — путь до директории для выходных данных (обязательный параметр).

```shell script
# полная команда
yfm build -i ./input-folder -o ./output-folder

# также, доступна сокращенная форма без build
yfm -o ./output-folder
```

Стандартным выходным форматом сборщика является HTML.

Полный список параметров сборки можно [найти в статье](settings.md) или вывести в консоли командой `yfm build --help`.

## YFM → YFM {#yfm}

Вы можете выполнить промежуточную сборку YFM в YFM. Для этого при выполнении команды укажите ключ запуска `--output-format=md`.

При сборке в YFM выполняются:
* [вставки](../../project/toc-includes.md) и [проверки условия видимости разделов](../../project/toc.md#when) в файлах оглавлений;
* [проверки условия отображения контента](../../syntax/vars.md#conditions) на страницах документа;
* [подстановки переменных](../../syntax/vars.md#subtitudes), если указан параметр `apply-presets`;
* [инлайнинг SVG-изображений](../../syntax/media.md#img-inline);
* [подстановки заголовков статей вместо {#T}](../../syntax/links.md#autotitle).

Используйте этот вид сборки, чтобы поддерживать несколько вариантов документации для разных пользователей. Если в документации есть разделы с внутренней информацией, вы можете держать два репозитория — приватный и публичный, и синхронизировать приватный в публичный с помощью условий.

## Watch-режим {#watch}

{% note info "Beta-функциональность" %}

При возникновении проблем сообщите об этом с помощью [GitHub issues](https://github.com/diplodoc-platform/cli/issues).

{% endnote %}

Вы можете автоматизировать пересборку отдельных статей при их изменении. Для этого вызовите `yfm build` с параметром `--watch`: после сборки проекта программа перейдёт в режим инкрементальной пересборки и будет создавать или обновлять статьи после сохранения изменений в исходных файлах документации.

Для удобства, после пересборки открытого в браузере файла выполняется автоматическая перезагрузка страницы.

## Статистика сборки {#build-stats}

При запуске с ключом [`--build-stats`](settings.md#build-stats-flag) (или `buildStats: true` в [файле конфигурации](../../settings.md#config)) рядом с output записывается файл `yfm-build-stats.json` с метриками текущей сборки. Файл предназначен для CI-дашбордов, отслеживания регрессий и диагностики — для рантайма он не нужен.

Что попадает в файл:

* `cli` — версия пакета, версия Node, платформа, архитектура, релиз ОС.
* `build` — `startedAt`, `finishedAt`, `durationMs`, грубое разбиение по фазам `phasesMs.{prepare, entries, finalize}` (на основе времени `Entry`-хука), `outputFormat`, `langs`, `inputDir`, `outputDir`, `features` (включённые булевы флаги), `memoryUsageMb` (`heapUsed` в момент завершения, в МБ), `worker.maxOldSpace`.
* `counters` — `tocs`, `entriesPlanned` / `entriesProcessed`, разбивки `entriesByExtension` и `entriesByLang`, `headings` и `contentBytes` (для md-страниц), а также `graph.{entries, sources, resources, missed, edges}` — снимок графа зависимостей: страницы, включаемые файлы, ассеты, отсутствующие пути и число рёбер.
* `output` — `files`, `totalBytes`, `bytesByExtension`.
* `schemaVersion` — версия формата файла. При расширении формата схема будет совместимой; ломающие изменения увеличат это число.

Пример выходного файла:

```json
{
  "schemaVersion": 1,
  "cli": { "version": "5.29.0", "node": "v22.22.0", "platform": "darwin", "arch": "arm64" },
  "build": {
    "durationMs": 1474,
    "phasesMs": { "prepare": 1242, "entries": 148, "finalize": 84 },
    "outputFormat": "html",
    "langs": ["ru", "en"],
    "features": ["addAlternateMeta", "allowHtml", "buildStats", "sanitizeHtml"],
    "memoryUsageMb": 256
  },
  "counters": {
    "tocs": 3,
    "entriesPlanned": 133,
    "entriesProcessed": 133,
    "entriesByExtension": { ".md": 122, ".yaml": 11 },
    "entriesByLang": { "ru": 91, "en": 42 },
    "headings": 345,
    "contentBytes": 1693771,
    "graph": { "entries": 130, "sources": 12, "resources": 74, "missed": 0, "edges": 129 },
    "warnings": 0,
    "errors": 0
  },
  "output": {
    "files": 421,
    "totalBytes": 45350699,
    "bytesByExtension": { ".html": 2865454, ".js": 9721257, ".png": 24588860 }
  }
}
```
