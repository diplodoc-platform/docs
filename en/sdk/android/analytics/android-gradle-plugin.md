# AppMetrica Gradle Plugin

AppMetrica lets you collect information about native and Java crashes. You can analyze them in the [Crashes](../../../mobile-reports/crashes-and-errors.md) report. See also [Crashes/errors](../../../data-collection/about-crashes-and-errors.md).

To reduce the size of an app, [optimize](https://developer.android.com/studio/build/shrink-code) the code during a release build.

If the code was compressed and obfuscated during the build of an Android application, information about crashes is transmitted in obfuscated form. To extract data for analysis from such crash logs, AppMetrica performs server-side deobfuscation.

To do this, upload the mapping files or debug symbols of SO files to AppMetrica, either automatically when building the app or manually via the web interface.

To send files, enable the AppMetrica Gradle Plugin.

## Restrictions {#restrictions}

- Upload mapping files if you use [ProGuard](https://www.guardsquare.com/en/products/proguard/manual) or [R8](https://r8.googlesource.com/r8/). If you don't compress or obfuscate the code, don't enable the plugin.

- The plugin's operation depends on the versions of `com.android.tools.build:gradle` (AGP) and gradle. The plugin is compatible with the following versions:

    - `com.android.tools.build:gradle` from `7.2.0` to `8.8.0` (except for `8.0.*`);
    - gradle from `7.4` to `8.12`. We don't guarantee that the plugin will work with other versions.

    The plugin's functionality is not guaranteed when using Gradle `8.0` and AGP `7.4.*` together.

- The plugin does not support [Configuration Cache](https://docs.gradle.org/current/userguide/configuration_cache.html) in Gradle. All plugin tasks are marked as incompatible with this feature, and when using them, you will see a warning from Gradle.

- It is recommended to disable the plugin for local builds. This will speed up the project build. The plugin must be enabled only for CI builds.

## Connecting the plugin {#connecting}

To enable the plugin:

1. Add the following dependency to the Gradle root file:

   {% list tabs %}

    - build.gradle.kts

        ```kotlin translate=no
        plugins {
            id("io.appmetrica.analytics") version "{{ io-appmetrica-analytics-gradle }}" apply false
        }
        ```

    - build.gradle

        ```groovy translate=no
        plugins {
            id "io.appmetrica.analytics" version "{{ io-appmetrica-analytics-gradle }}" apply false
        }
        ```

   {% endlist %}

   {% cut "Enabling plugin using `buildscript`" %}

   Add the following dependency to the Gradle root file:

   {% list tabs %}

    - build.gradle.kts

        ```kotlin translate=no
        buildscript {
            repositories {
                mavenCentral()
            }
            dependencies {
                classpath("io.appmetrica.analytics:gradle:{{ io-appmetrica-analytics-gradle }}")
            }
        }
        ```

    - build.gradle

        ```groovy translate=no
        buildscript {
            repositories {
                mavenCentral()
            }
            dependencies {
                classpath 'io.appmetrica.analytics:gradle:{{ io-appmetrica-analytics-gradle }}'
            }
        }
        ```

   {% endlist %}

   {% endcut %}

2. Add connecting and configuring the plugin to the app's Gradle file:

   {% list tabs %}

   - build.gradle.kts

        ```kotlin translate=no
        plugins {
            id("com.android.application")
            id("io.appmetrica.analytics")
        }

        appmetrica {
            postApiKey = { applicationVariant -> "Post Api key for variant" }
            // or setPostApiKey("Post Api key")
            enable = { applicationVariant -> true }                           // Optional
            offline = { applicationVariant -> false }                         // Optional
            mappingFile = { applicationVariant -> null }                      // Optional
            enableAnalytics = true                                            // Optional
            allowTwoAppMetricas = { applicationVariant -> false }             // Optional
            ndk {                                                             // Optional
                enable = { applicationVariant -> false }
                soFiles = { applicationVariant -> listOfSoFiles }             // Optional
                additionalSoFiles = { applicationVariant -> listOfSoFiles }   // Optional
                addNdkCrashesDependency = { applicationVariant -> true }      // Optional
            }
        }
     ```

   - build.gradle

        ```groovy translate=no
        plugins {
            id 'com.android.application'
            id 'io.appmetrica.analytics'
        }

        appmetrica {
            postApiKey = { applicationVariant -> "Post Api key for variant" }
            // or postApiKey = "Post Api key"
            enable = { applicationVariant -> true }                           // Optional
            offline = { applicationVariant -> false }                         // Optional
            mappingFile = { applicationVariant -> null }                      // Optional
            enableAnalytics = true                                            // Optional
            allowTwoAppMetricas = { applicationVariant -> false }             // Optional
            ndk {                                                             // Optional
                enable = { applicationVariant -> false }
                soFiles = { applicationVariant -> listOfSoFiles }             // Optional
                additionalSoFiles = { applicationVariant -> listOfSoFiles }   // Optional
                addNdkCrashesDependency = { applicationVariant -> true }      // Optional
            }
        }
        ```

   {% endlist %}

   #|
   || **Parameter** | **Description** ||
   || `postApiKey*` | Post API key or lambda function that returns a Post API key for `ApplicationVariant`. Read more about `ApplicationVariant` in the [Android](https://developer.android.com/studio/build/build-variants) and [Javadoc](https://www.javadoc.io/doc/com.android.tools.build/gradle/0.7.2/com/android/build/gradle/api/ApplicationVariant.html) documentation.
   You can get the Post API key in the AppMetrica Settings. It's used to identify your app.

   If `offline = true`, the parameter is optional. ||
   || `enable` | Lambda function that accepts `ApplicationVariant` and returns whether to use the plugin for this build option.
   If the plugin is not used, the apk does not change and the mapping file does not load.

   By default, it returns `true` only for `buildType = 'release'`.

   {% note info %}

   Use one of the parameters to specify assembly types: `enable` or `mappingBuildTypes`.

   {% endnote %}
   ||
   || `mappingBuildTypes` | List of `buildType` build types for which the mapping file will be sent.
   Default value: `['release']`.

   To disable the uploading of mapping files for a specific type of build, delete that `buildType` from the list.

   {% note info %}

   Use one of the parameters to specify assembly types: `enable` or `mappingBuildTypes`.

   {% endnote %}
   ||
   || `offline` | Enables the `offline` mode. Boolean or a lambda function that accepts `ApplicationVariant`.

   Acceptable values:

   * `true` — Doesn't upload a file to AppMetrica. If enabled, it outputs the archive path to the log after the build is complete. You can upload it manually via the web interface.
   * `false` — Automatically uploads the mapping file.
      The default value is `false`. ||
      || `mappingFile` | Lambda function that accepts `ApplicationVariant` and returns the mapping file to upload. If it returns `null`, the default value is used.

   The default value is `ApplicationVariant.mappingFileProvider`. ||
   || `enableAnalytics` | Lets plugin usage statistics be sent to AppMetrica. `Boolean`.

   Acceptable values:

   * `true` — Sending statistics is enabled.
   * `false` — Sending statistics is disabled.
      The default value is `true`. ||
      || `allowTwoAppMetricas` | A lambda function that accepts `ApplicationVariant` and checks the use of two AppMetrica libraries at the same time.

   Acceptable values:

   * `false` — The plugin checks that only one library version is used in the project: `io.appmetrica.analytics:analytics` or `com.yandex.android:mobmetricalib`. If not, an exception is thrown.
   * `true` — The plugin checks the use of two AppMetrica libraries at the same time, the check result is logged.

   The default value is `false`. ||
   || `ndk` | This parameter is required to load characters from the SO file to track native crashes. ||
   || `ndk.enable` | A lambda function that accepts `ApplicationVariant` and returns whether to load the characters from the SO files for this build option.

   The default value is `false`. ||
   || `ndk.soFiles` | A lambda function that accepts `ApplicationVariant` and returns a list of SO files.

   By default, the plugin searches for SO files in the Android Studio project folders.

   You need to redefine the path if your SO files are in an unusual location or the plugin can't find them. ||
   || `ndk.additionalSoFiles` | A lambda function that accepts `ApplicationVariant` and returns a list of additional SO files to load the characters from. ||
   || `ndk.addNdkCrashesDependency` | A lambda function that accepts `ApplicationVariant` and returns whether to include the `io.appmetrica.analytics:analytics-ndk-crashes` dependency.

   The default value is `true`. ||
   |#

3. If the `ndk` parameter is enabled, debug characters are sent using the `upload${variant.name.capitalize()}AppMetricaNdkSymbols` Gradle task. To call a task automatically, you can add it to a file `app/build.gradle` the following code:

   {% list tabs %}

   - build.gradle.kts

        ```kotlin translate=no
        android.applicationVariants.configureEach {
            val variant = this
            val uploadSymbolsTask = project.tasks.findByName("upload${variant.name.capitalize()}AppMetricaNdkSymbols")
            if (uploadSymbolsTask != null) {
                variant.assembleProvider.configure { it.finalizedBy(uploadSymbolsTask) }                     // if you use apk
                project.tasks.named("bundle${variant.name.capitalize()}") { finalizedBy(uploadSymbolsTask) } // if you use aab
            }
        }
        ```

   - build.gradle

        ```groovy translate=no
        android.applicationVariants.configureEach { variant ->
            def uploadSymbolsTask = project.tasks.findByName("upload${variant.name.capitalize()}AppMetricaNdkSymbols")
            if (uploadSymbolsTask != null) {
                variant.assembleProvider.configure { it.finalizedBy(uploadSymbolsTask) }                     // if you use apk
                project.tasks.named("bundle${variant.name.capitalize()}") { finalizedBy(uploadSymbolsTask) } // if you use aab
            }
        }
        ```

   {% endlist %}

## Manual loading {#manual-loading}

To manually load, enable and use the plugin in `offline` mode. This is necessary to link the mapping file to the app build.

1. In the app/build.gradle file, turn on the `offline` mode and run the build.

   {% list tabs %}

   - build.gradle.kts

        ```kotlin translate=no
        appmetrica {
            offline = { true }
        }
        ```

   - build.gradle

        ```groovy translate=no
        appmetrica {
            offline = { true }
        }
        ```

   {% endlist %}

2. In the AppMetrica interface, go to the app settings from the menu on the left.
3. Go to the **Crashes** → **Android** tab.
4. Click **Choose file** and upload the ZIP archive.

## Description of generated files {#generated-files}

The plugin for work generates files in the `app/build/appmetrica` folder.
The folder structure is given below.

```
app/build/appmetrica
└── release - the name of AndroidApplicationVariant
    ├── info.txt - the file with meta information for searching for a mapping file and symbols
    ├── res - the folder with resources that will be used to build the application
    │   ├── raw
    │   │   └── keep_appmetrica_resources.xml - rules for R8 on resource conservation
    │   └── values
    │       └── appmetrica_resources.xml - resources required for work
    ├── result - the folder with archives that you need to upload manually when using offline mode
    │   ├── mapping.zip - the final archive with mappings
    │   └── symbols.zip - the final archive with symbols
    └── symbols - a folder with symbols that came from so files
        ├── libmyapplication_0E6CC10E8293F1B2DF0293FBE44887AD0.ysym
        ├── libmyapplication_3CDE92724603DA3A59BC6E311625A4000.ysym
        ├── libmyapplication_6F5C61C0E96CAEFD1E7ED491F806DA100.ysym
        └── libmyapplication_F3E083A014DD2840F0E730B6BB138E4A0.ysym
```

## Build errors {#errors}

Possible errors during a build:

- `IllegalStateException` — Enable code obfuscation using ProGuard or R8 Compiler.
- `HttpResponseException` — Check your internet connection.

If you encounter further errors, please contact [technical support](../../../troubleshooting/feedback-new.md).

## Learn more {#learn-more}

- [Crashes and errors report](../../../mobile-reports/crashes-and-errors.md)
- [Android documentation](https://developer.android.com/topic/performance/vitals/crash)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
