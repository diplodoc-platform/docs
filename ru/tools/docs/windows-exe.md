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

## Шаг 2. Соберите EXE {#build}

Скопируйте в терминал целиком блок для своей системы и нажмите Enter. Он создаст папку `yfm-exe`, скачает в нее нужные пакеты и соберет файл.

{% list tabs %}

- Windows (PowerShell)

  ```powershell
  mkdir yfm-exe
  cd yfm-exe
  @'
  {
    "name": "yfm-portable",
    "version": "1.0.0",
    "bin": "node_modules/@diplodoc/cli/build/index.js",
    "pkg": {
      "scripts": [
        "node_modules/@diplodoc/cli/build/**/*.js",
        "node_modules/@diplodoc/cli/lib/**/*.js",
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
  '@ | Set-Content -Encoding Ascii package.json
  npm install @diplodoc/cli @yao-pkg/pkg
  npx pkg --compress GZip --public -t node24-win-x64 -o dist/yfm.exe package.json
  ```

- macOS и Linux

  ```shell
  mkdir yfm-exe && cd yfm-exe
  cat > package.json <<'EOF'
  {
    "name": "yfm-portable",
    "version": "1.0.0",
    "bin": "node_modules/@diplodoc/cli/build/index.js",
    "pkg": {
      "scripts": [
        "node_modules/@diplodoc/cli/build/**/*.js",
        "node_modules/@diplodoc/cli/lib/**/*.js",
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
  EOF
  npm install @diplodoc/cli @yao-pkg/pkg
  npx pkg --compress GZip --public -t node24-win-x64 -o dist/yfm.exe package.json
  ```

{% endlist %}

Последняя команда при первом запуске скачивает базовую сборку Node.js для Windows, поэтому может работать несколько минут. Предупреждения `Warning` в процессе - это нормально.

Готовый файл появится в папке `yfm-exe/dist/yfm.exe`. Размер около 160 МБ - внутри лежит полноценный Node.js.

{% cut "Что делает этот блок" %}

1. Создает папку `yfm-exe` и переходит в нее.
2. Кладет в нее файл `package.json` - список внутренних файлов CLI, которые нужно упаковать внутрь `yfm.exe`. Без этого списка собранный файл не запустится.
3. Устанавливает два пакета: сам CLI и инструмент упаковки [@yao-pkg/pkg](https://github.com/yao-pkg/pkg).
4. Запускает упаковку: параметр `-t node24-win-x64` задает целевую систему, `--compress GZip` уменьшает размер файла примерно вдвое, `-o` - путь к результату.

{% endcut %}

## Шаг 3. Проверьте результат {#check}

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

  {% cut "Как вшить плагины внутрь файла" %}

  Плагины можно упаковать внутрь `yfm.exe` на этапе сборки. Перед последней командой шага 2 скопируйте файл с плагинами в пакет CLI:

  ```shell
  mkdir -p node_modules/@diplodoc/cli/build/plugins
  cp путь-к-вашему-plugins.js node_modules/@diplodoc/cli/build/plugins/index.js
  ```

  После этого соберите файл заново - плагины будут работать на всех машинах без дополнительных файлов.

  {% endcut %}

* Чтобы обновить CLI до новой версии, соберите файл заново: выполните в папке `yfm-exe` команду `npm install @diplodoc/cli@latest` и повторите последнюю команду [шага 2](#build).

## Сборка под другие системы {#other-targets}

Тем же способом можно собрать файл для macOS или Linux - поменяйте в последней команде значение параметра `-t` и имя выходного файла:

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
npx pkg --compress GZip --public -t node24-linux-x64 -o dist/yfm-linux package.json
```
