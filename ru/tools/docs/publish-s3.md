# Выкладка на S3

Для публикации документации в [хранилище S3](https://cloud.yandex.ru/services/storage) используется команда `yfm publish`.

{% note warning %}

Команда не собирает документацию — перед публикацией её нужно собрать с помощью `yfm build`.

```bash
# Сборка документации
yfm build -i docs/ -o docs-html/

# Публикация в S3
yfm publish -i docs-html/ \
  --access-key-id "YCAJE..." \
  --secret-access-key "YCO..."
```

{% endnote %}

## Аргументы команды publish

#|
|| **Аргумент** | **Описание** | **Значение по умолчанию** ||
|| `--input` (`-i`){{required}} | Путь к директории с собранной документацией | — ||
|| `--endpoint` | Эндпоинт для хранилища S3 | `https://s3.amazonaws.com` ||
|| `--bucket`{{required}} | Имя бакета | — ||
|| `--prefix` |
Префикс для путей файлов.
\
Может использоваться для передачи версии сборки, тогда каждая сборка будет складываться в отдельную папку.
| — ||
|| `--region` | Регион S3-хранилища | `eu-central-1` ||
|| `--hidden` | Список glob-паттернов файлов, которые не нужно загружать в хранилище | — ||
|| `--access-key-id`{{required}} | Идентификатор ключа доступа к S3 | — ||
|| `--secret-access-key`{{required}} | Секретный ключ доступа к S3 | — ||
|#

Часть параметров рекомендуется выносить в [файл конфигурации](../../settings.md). Это позволит не повторять их при каждом запуске команды. Чувствительные данные (`--access-key-id`, `--secret-access-key`) передаются **только через аргументы**.

## Примеры

### Секция publish в конфигурационном файле **.yfm**

```yaml
publish:
  endpoint: "https://storage.yandexcloud.net"
  bucket: "my-docs-bucket"
  prefix: "docs/"
  region: "eu-central-1"
  hidden:
    - ".yfm"
```

### Аргументы командной строки

```bash
yfm publish -i docs-html/ \
  --endpoint "https://storage.yandexcloud.net" \
  --bucket "my-docs-bucket" \
  --prefix "docs/v1.0/" \
  --region "eu-central-1" \
  --access-key-id "YCAJE..." \
  --secret-access-key "YCO..."
```