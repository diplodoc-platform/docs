# Portable CLI build for Windows

You can pack the [@diplodoc/cli](https://www.npmjs.com/package/@diplodoc/cli) package into a single executable file, `yfm.exe`. The file contains both the CLI and the Node.js runtime, so the computer that runs it doesn't need anything installed: no Node.js, no npm. It also works without internet access.

This is handy when documentation is built by people without permission to install software or on machines with no internet connection.

{% note info %}

You only need to build the file once, on any computer with internet access: Windows, macOS, or Linux. The resulting `yfm.exe` can then simply be copied to other machines.

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

## Step 2. Create a folder and install the packages {#install-packages}

Run the following commands in the terminal one by one:

```shell
mkdir yfm-exe
cd yfm-exe
npm init -y
npm install @diplodoc/cli @yao-pkg/pkg
```

These commands create the `yfm-exe` folder and download the CLI and the [@yao-pkg/pkg](https://github.com/yao-pkg/pkg) packaging tool into it.

## Step 3. Create the configuration file {#config}

Create a file named `pkg.config.json` in the `yfm-exe` folder and copy the following content into it as is:

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

This file tells the packaging tool which internal CLI files must be packed into `yfm.exe`. Without it, the resulting file won't start.

{% note tip %}

You can create the file with any text editor, such as Notepad. When saving, make sure the file name is exactly `pkg.config.json`, not `pkg.config.json.txt`.

{% endnote %}

## Step 4. Build the EXE {#build}

Run a single command in the terminal (all of it, it's one line):

```shell
npx pkg node_modules/@diplodoc/cli/build/index.js -c pkg.config.json -t node24-win-x64 -o dist/yfm.exe
```

On the first run, the command downloads a base Node.js build for Windows, so it may take a few minutes. `Warning` messages during the process are normal.

The resulting file appears at `yfm-exe/dist/yfm.exe`. It's about 300 MB, as it contains a full Node.js runtime.

## Step 5. Check the result {#check}

Run the built file:

```shell
dist\yfm.exe --version
```

It should print the CLI version, for example `5.55.3`. Then build some documentation project:

```shell
dist\yfm.exe -i path-to-sources -o path-to-output
```

## How to use it {#usage}

* Copy `yfm.exe` anywhere: to another computer, a flash drive, or a network share. No installation is needed, the file is self-contained.
* All commands and options are the same as in the regular `yfm` from npm: [building a project](build.md), [build parameters](settings.md).
* On the first launch of a copied file, Windows may show a SmartScreen warning because the file isn't signed. Click **More info**, then **Run anyway**.

## Limitations {#limitations}

* Custom plugins (a `plugins.js` file next to the project) don't load in the portable build.
* To update the CLI to a new version, rebuild the file: run `npm install @diplodoc/cli@latest` in the `yfm-exe` folder and repeat [step 4](#build).

## Building for other systems {#other-targets}

The same approach works for macOS and Linux - change the `-t` parameter value and the output file name:

| System | `-t` parameter |
| --- | --- |
| Windows x64 | `node24-win-x64` |
| Windows arm64 | `node24-win-arm64` |
| macOS Apple Silicon | `node24-macos-arm64` |
| macOS Intel | `node24-macos-x64` |
| Linux x64 | `node24-linux-x64` |
| Linux arm64 | `node24-linux-arm64` |

For example, a Linux build:

```shell
npx pkg node_modules/@diplodoc/cli/build/index.js -c pkg.config.json -t node24-linux-x64 -o dist/yfm-linux
```
