# Portable-версия CLI для Windows

Из пакета [@diplodoc/cli](https://www.npmjs.com/package/@diplodoc/cli) можно собрать один исполняемый файл `yfm.exe`. Внутри такого файла уже есть и сам CLI, и среда выполнения Node.js, поэтому на компьютере, где он запускается, не нужно ничего устанавливать: ни Node.js, ни npm. Интернет для работы тоже не требуется.

Это удобно, если документацию собирают люди без прав на установку программ или на компьютерах без доступа в интернет.

{% note info %}

Сборку достаточно выполнить один раз на любом компьютере с интернетом: Windows, macOS или Linux. Готовый `yfm.exe` можно просто копировать на другие машины.

{% endnote %}

## Шаг 1. Установите Node.js {#install-node}

Node.js нужен только на том компьютере, где вы собираете файл.

1. Скачайте установщик Node.js версии 24 или новее с [официального сайта](https://nodejs.org/).
2. Запустите его и пройдите все шаги с настройками по умолчанию.
3. Откройте терминал (в Windows - приложение **PowerShell**) и проверьте установку:

   ```shell
   node -v
   ```

   В ответ должен появиться номер версии, например `v24.18.0`.

## Шаг 2. Создайте папку и установите пакеты {#install-packages}

Выполните в терминале по очереди:

```shell
mkdir yfm-exe
cd yfm-exe
npm init -y
npm install @diplodoc/cli @yao-pkg/pkg
```

Команды создадут папку `yfm-exe` и скачают в нее CLI и инструмент сборки [@yao-pkg/pkg](https://github.com/yao-pkg/pkg).

## Шаг 3. Создайте файл настроек {#config}

Создайте в папке `yfm-exe` файл с именем `pkg.config.json` и скопируйте в него содержимое без изменений:

```json
{
  "pkg": {
    "scripts": [
      "node_modules/@diplodoc/cli/build/**/*.js",
      "node_modules/@diplodoc/client/build/server/**/*.js"
    ],
    "assets": [
      "node_modules/@diplodoc/cli/assets/**/*",
      "node_modules/@diplodoc/cli/build/manifest.json",
      "node_modules/@diplodoc/cli/package.json",
      "node_modules/highlight.js/styles/**/*"
    ]
  }
}
```

Этот файл говорит инструменту сборки, какие внутренние файлы CLI нужно упаковать внутрь `yfm.exe`. Без него собранный файл не запустится.

{% note tip %}

Создать файл можно любым текстовым редактором, например «Блокнотом». При сохранении убедитесь, что имя файла именно `pkg.config.json`, а не `pkg.config.json.txt`.

{% endnote %}

## Шаг 4. Соберите EXE {#build}

Выполните в терминале одну команду (целиком, это одна строка):

```shell
npx pkg node_modules/@diplodoc/cli/build/index.js -c pkg.config.json -t node24-win-x64 -o dist/yfm.exe
```

При первом запуске команда скачает базовую сборку Node.js для Windows, поэтому может работать несколько минут. Предупреждения `Warning` в процессе - это нормально.

Готовый файл появится в папке `yfm-exe/dist/yfm.exe`. Размер около 300 МБ - внутри лежит полноценный Node.js.

## Шаг 5. Проверьте результат {#check}

Запустите собранный файл:

```shell
dist\yfm.exe --version
```

В ответ должна появиться версия CLI, например `5.55.3`. Затем соберите какой-нибудь проект документации:

```shell
dist\yfm.exe -i путь-к-исходникам -o путь-к-результату
```

## Как пользоваться {#usage}

* Скопируйте `yfm.exe` в любое место: на другой компьютер, флешку или сетевой диск. Установка не нужна, файл самодостаточен.
* Все команды и параметры такие же, как у обычного `yfm` из npm: [сборка проекта](build.md), [параметры сборки](settings.md).
* При первом запуске скопированного файла Windows может показать предупреждение SmartScreen, потому что файл не подписан. Нажмите **Подробнее**, затем **Выполнить в любом случае**.

## Ограничения {#limitations}

* Пользовательские плагины (файл `plugins.js` рядом с проектом) из portable-версии не подключаются.
* Чтобы обновить CLI до новой версии, соберите файл заново: выполните в папке `yfm-exe` команду `npm install @diplodoc/cli@latest` и повторите [шаг 4](#build).

## Сборка под другие системы {#other-targets}

Тем же способом можно собрать файл для macOS или Linux - поменяйте значение параметра `-t` и имя выходного файла:

| Система | Параметр `-t` |
| --- | --- |
| Windows x64 | `node24-win-x64` |
| Windows arm64 | `node24-win-arm64` |
| macOS Apple Silicon | `node24-macos-arm64` |
| macOS Intel | `node24-macos-x64` |
| Linux x64 | `node24-linux-x64` |
| Linux arm64 | `node24-linux-arm64` |

Например, сборка для Linux:

```shell
npx pkg node_modules/@diplodoc/cli/build/index.js -c pkg.config.json -t node24-linux-x64 -o dist/yfm-linux
```
