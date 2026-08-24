# Portable CLI build

You can pack the [@diplodoc/cli](https://www.npmjs.com/package/@diplodoc/cli) package into a single executable file for Windows, macOS, or Linux. The file contains both the CLI and the Node.js runtime, so the computer that runs it doesn't need anything installed: no Node.js, no npm. It also works without internet access.

This is handy when documentation is built by people without permission to install software or on machines with no internet connection.

{% note info %}

You only need to build the file once, on any computer with internet access. The resulting file can then simply be copied to other machines with the same operating system.

{% endnote %}

## Step 1. Install Node.js {#install-node}

Node.js is only required on the computer where you build the file.

1. Download the Node.js installer, version 24 or newer, from the [official website](https://nodejs.org/).
2. Run it and complete all steps with the default settings.
3. Open a terminal (on Windows, the **PowerShell** app) and check the installation:

   ```shell
   node -v
   ```

   It should print a version number, for example `v24.18.0`.

## Step 2. Build the executable {#build}

Pick the tab with the system the file will run on. Copy the entire block into the terminal and press Enter: it creates the `yfm-exe` folder, downloads the required packages into it, and builds the file.

{% list tabs %}

- Windows

  Run in **PowerShell**:

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

  The resulting file: `yfm-exe/dist/yfm.exe`.

- macOS

  Run in Terminal:

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
  npx pkg --compress GZip --public -t node24-macos-arm64 -o dist/yfm package.json
  ```

  The resulting file: `yfm-exe/dist/yfm`.

  {% note info %}

  The command builds a file for Macs with Apple Silicon processors (M1 and newer). For Intel-based Macs, replace `node24-macos-arm64` with `node24-macos-x64` in the last command.

  {% endnote %}

- Linux

  Run in the terminal:

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
  npx pkg --compress GZip --public -t node24-linux-x64 -o dist/yfm package.json
  ```

  The resulting file: `yfm-exe/dist/yfm`.

  {% note info %}

  The command builds a file for x64 processors. For arm64 (for example, Raspberry Pi or ARM servers), replace `node24-linux-x64` with `node24-linux-arm64` in the last command.

  {% endnote %}

{% endlist %}

On the first run, the last command downloads a base Node.js build for the target system, so it may take a few minutes. `Warning` messages during the process are normal.

The resulting file is about 150 MB, as it contains a full Node.js runtime.

{% cut "What this block does" %}

1. Creates the `yfm-exe` folder and switches into it.
2. Puts a `package.json` file into it - the list of internal CLI files that must be packed into the executable. Without this list, the resulting file won't start.
3. Installs two packages: the CLI itself and the [@yao-pkg/pkg](https://github.com/yao-pkg/pkg) packaging tool.
4. Runs the packaging: the `-t` parameter sets the target system, `--compress GZip` roughly halves the file size, and `-o` sets the output path.

{% endcut %}

## Step 3. Check the result {#check}

Run the built file. On Windows:

```shell
dist\yfm.exe --version
```

On macOS and Linux:

```shell
./dist/yfm --version
```

It should print the CLI version, for example `5.55.3`. Then build some documentation project:

```shell
dist\yfm.exe -i path-to-sources -o path-to-output
```

## How to use it {#usage}

* Copy the file anywhere: to another computer, a flash drive, or a network share. No installation is needed, the file is self-contained.
* All commands and options are the same as in the regular `yfm` from npm: [building a project](build.md), [build parameters](settings.md).
* The file isn't signed, so security features may ask for confirmation on the first launch:
  * on Windows, click **More info** and then **Run anyway** in the SmartScreen window;
  * on macOS, if the file was downloaded from the internet, allow it in **System Settings** → **Privacy & Security**, or remove the quarantine attribute with `xattr -d com.apple.quarantine path-to-file`.

## Limitations {#limitations}

* The file only runs on the system it was built for. If you need both Windows and macOS, build two files, see [building for another system](#other-targets).
* Custom plugins (a `plugins.js` file next to the project) don't load in the portable build.

  {% cut "How to bake plugins into the file" %}

  Plugins can be packed into the file at build time. Before the last command of step 2, copy your plugins file into the CLI package:

  ```shell
  mkdir -p node_modules/@diplodoc/cli/build/plugins
  cp path-to-your-plugins.js node_modules/@diplodoc/cli/build/plugins/index.js
  ```

  Then rebuild the file - the plugins will work on all machines without any extra files.

  {% endcut %}

* To update the CLI to a new version, rebuild the file: run `npm install @diplodoc/cli@latest` in the `yfm-exe` folder and repeat the last command of [step 2](#build).

## Building for another system {#other-targets}

You can build on one system and run on another: for example, build a Windows file on macOS. To do that, change the `-t` parameter value in the last command of step 2:

| System | `-t` parameter |
| --- | --- |
| Windows x64 | `node24-win-x64` |
| Windows arm64 | `node24-win-arm64` |
| macOS Apple Silicon | `node24-macos-arm64` |
| macOS Intel | `node24-macos-x64` |
| Linux x64 | `node24-linux-x64` |
| Linux arm64 | `node24-linux-arm64` |

For example, building a Windows file on any system:

```shell
npx pkg --compress GZip --public -t node24-win-x64 -o dist/yfm.exe package.json
```
