# Creating screenshots and videos

The [@diplodoc/screencaster](https://github.com/diplodoc-platform/screencaster) package creates screenshots and videos for documentation. It opens a page in Chromium, performs actions in the interface, and saves the result.

An agent with MCP (Model Context Protocol) support controls Screencaster. You describe what to show, and the agent finds the page elements and follows the scenario. The package also provides a TypeScript API for use in your own application.

## Features {#features}

Use Screencaster to:

- Capture the viewport, a full page, or an individual element.
- Highlight an element in a screenshot or video.
- Record a workflow and shorten pauses between actions.
- Add narration and captions.
- Cut a clip or export it as a GIF.
- Crop screenshots, combine images, and prepare YFM markup for illustrations.

The original recording is kept alongside the processed files. You can create another version of the video without repeating the browser actions.

Screenshots are saved as PNG, and processed videos as WebM. You can convert a video to MP4 with FFmpeg for use on a website.

## Setup {#setup}

1. Install Node.js 24 or later and npm 11.5.1 or later.

1. Install the package:

    ```bash
    npm install @diplodoc/screencaster
    ```

1. Prepare Chromium for the Playwright version used by the package. Video processing also requires FFmpeg with the `libvpx-vp9` and `libopus` codecs. If FFmpeg is outside `PATH`, set its path in `FFMPEG_PATH`.

   See the [package README](https://github.com/diplodoc-platform/screencaster#development) for browser installation and environment requirements.

## Configuration {#config}

Create a `run.config.json` file. This example opens the [Playground](https://diplodoc-platform.github.io/transform/), records video, and enables screenshots with highlighted elements:

```json
{
  "version": 1,
  "directory": "./runs",
  "browser": {
    "url": "https://diplodoc-platform.github.io/transform/",
    "headless": true,
    "locale": "en-US",
    "colorScheme": "light",
    "viewport": {
      "width": 1920,
      "height": 1080
    },
    "deviceScaleFactor": 1
  },
  "policy": {
    "rules": [
      {
        "origin": "https://diplodoc-platform.github.io",
        "pathPrefix": "/transform/",
        "actions": ["read", "act"]
      }
    ]
  },
  "outputs": {
    "video": {
      "name": "walkthrough",
      "highlights": true
    },
    "screenshots": {
      "highlight": true
    }
  }
}
```

- `directory` is the output folder. Each capture gets its own subdirectory.
- `browser.url` is the page where the scenario starts.
- `browser.headless` controls whether the browser window is visible. Use `true` to hide it or `false` to show it.
- `browser.viewport` sets the page size in CSS pixels. Video recording uses the same size.
- `browser.deviceScaleFactor` sets the pixel density for screenshots. For example, `2` produces an image at twice the resolution.
- `policy` specifies which pages and actions the agent can access.
- `outputs.video` enables automatic video processing when capture finishes.
- `highlights` and `highlight` enable element outlines in videos and screenshots.

Paths are relative to the directory containing `run.config.json`. The `locale` setting changes the browser language, but does not change a language preference stored by the service.

For a page that requires authentication, supply a prepared session through `storageState` or connect your own login module. See [host authentication](https://github.com/diplodoc-platform/screencaster/blob/master/docs/host-adapters.md#host-authentication) for these options.

## Connecting an agent {#connect}

Add the MCP server to your agent's settings. For clients that use JSON configuration:

```json
{
  "mcpServers": {
    "screencaster": {
      "command": "npx",
      "args": [
        "--yes",
        "@diplodoc/screencaster",
        "--config",
        "/path/to/run.config.json"
      ]
    }
  }
}
```

Replace `/path/to/run.config.json` with the absolute path to your file. The settings format depends on your client. In clients with a different format, use the same command and arguments.

The MCP server starts with this command:

```bash
npx @diplodoc/screencaster --config ./run.config.json
```

Once connected, give the agent a [capture scenario](#example). You can provide the instruction as text, a Markdown file, or a URL that returns Markdown.

## Capture {#capture}

Specify the page URL, the sequence of actions, and the expected result after each step. For example, “Switch to the second tab and check that its text appears.”

For screenshots, specify which states to capture and which elements to highlight. Video is recorded while the agent follows the scenario.

Ask the agent to finish capture and return the output paths. Screencaster processes the recording and saves the results under `runs`. The `manifest.json` file in the capture directory lists artifacts, step statuses, and errors.

Before publishing, check that the recording shows the intended result, the text is readable, and the outlines highlight the correct elements.

## Narration and captions {#narration}

Connect a TTS provider to add narration. The package includes an adapter for [Yandex SpeechKit](https://yandex.cloud/en/docs/speechkit/tts/).

1. Create an `.env` file next to `run.config.json` and add your API key:

    ```dotenv
    SPEECHKIT_API_KEY=your_key
    ```

1. Add `envFile` and `tts` to the configuration:

    ```json
    {
      "envFile": ".env",
      "tts": {
        "provider": "speechkit",
        "options": {
          "apiKey": {"env": "SPEECHKIT_API_KEY"},
          "voice": "john",
          "speed": 1
        }
      }
    }
    ```

1. Add `narration` to the existing `outputs` object, keeping its `video` and `screenshots` settings:

    ```json
    {
      "narration": {
        "name": "narrated",
        "captions": true,
        "maxHoldSeconds": 5
      }
    }
    ```

1. On macOS and Linux, restrict access to the files:

    ```bash
    chmod 600 run.config.json .env
    ```

Write a short line of narration for each step. The agent uses these lines in the plan's `actionText` fields. After capture finishes, Screencaster adds narration to successfully completed steps. Setting `captions: true` also creates a WebVTT captions file. Attach this file to the player separately. Captions are not burned into the video frames.

If a line is longer than the available segment, Screencaster can hold a frame for up to `maxHoldSeconds`. For a short video, shorten the line so the viewer can hear it and follow the action.

The example uses the `john` voice for English. For Russian, use `jane`. Translate the scenario and narration, change the voice, and record a separate version for each language.

## Processing the results {#editing}

After capture, the agent can cut unwanted actions, create a short clip or GIF, or generate a cover. The MCP tools for these operations are `screencaster_edit`, `screencaster_clip`, and `screencaster_preview`.

Pause reduction uses recorded actions and page changes. The final duration depends on the scenario and, for narrated videos, the length of the spoken lines.

Screenshots have a separate processing workflow for cropping, highlighting, comparing states, and combining image series. See the [illustration guide](https://github.com/diplodoc-platform/screencaster/blob/master/docs/illustrations.md).

## Example {#example}

The [tabs article](../syntax/interactive-elements/tabs.md) uses an example with two sections, a list, and bold text. You can use it to record a Playground walkthrough.

[Open the example in the Playground](https://diplodoc-platform.github.io/transform/?input=%7B%2525%20list%20tabs%20%2525%7D%0A%0A-%20Tab%201%20title%0A%0A%20%20Tab%201%20text.%0A%0A%20%20*%20You%20can%20use%20lists.%0A%20%20*%20And%20**other**%20markup.%0A%0A-%20Tab%202%20title%0A%0A%20%20Tab%202%20text.%0A%0A%7B%2525%20endlist%20%2525%7D). To record a similar video, give the agent the example link above and the following instruction:

> Open the tabs example in the Diplodoc Playground and record a short video. Check the rendered result, switch to the second tab, and return to the first. Add narration and captions. Shorten agent waits in the final video, keeping the tab changes and time to read the result. Finish capture and return the output paths.
