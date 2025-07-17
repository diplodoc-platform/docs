# AMAPluginErrorDetails class

## Properties {#property_summary}

#|
|| [exceptionClass](#property_exceptionClass) | Name of the error class/interface/character (depending on the plugin being used). ||
|| [message](#property_message) | Short error description. ||
|| [backtrace](#property_backtrace) | Error backtrace. ||
|| [platform](#property_platform) | Name of the plugin where the error occurred. ||
|| [virtualMachineVersion](#property_virtualMachineVersion) | Virtual machine version. ||
|| [pluginEnvironment](#property_pluginEnvironment) | Plugin integration environment. ||
|#

### exceptionClass {#property_exceptionClass}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *exceptionClass;
```

Name of the error class/interface/character (depending on the plugin being used). No more than 100 characters. AppMetrica truncates any characters over the limit.

### message {#property_message}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *message;
```

Short error description. No more than 1000 characters. AppMetrica truncates any characters over the limit.

### backtrace {##property_backtrace}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSArray<AMAStackTraceElement *> *backtrace;
```

Error backtrace. No more than 200 stack frames. AppMetrica truncates the value if it exceeds the limit.

### platform {##property_platform}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *platform;
```

Name of the plugin where the error occurred. No more than 100 characters. AppMetrica truncates any characters over the limit.

Use the constants defined in `AMAPluginErrorDetails` for popular plugins, or specify a custom string for plugins that don't have a corresponding constant.

### virtualMachineVersion {##property_virtualMachineVersion}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSString *virtualMachineVersion;
```

Virtual machine version. No more than 100 characters. AppMetrica truncates any characters over the limit.

In this property, you can specify the plugin version that you're using (for example, Unity or Flutter).

### pluginEnvironment {##property_pluginEnvironment}

```objectivec translate=no
@property (nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *pluginEnvironment;
```

Plugin integration environment. A custom dictionary containing any additional information about the plugin.

No more than 50 key-value pairs. No more than 100 characters for the key, and no more than 2000 characters for the value. AppMetrica truncates any characters over the limit.
