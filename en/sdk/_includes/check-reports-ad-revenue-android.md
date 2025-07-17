## Step 1. Make sure that the SDK is activated. {#activate}

Activation example:

```java translate=no
AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY).build();
AppMetrica.activate(context, config);
```

## Step 2. Make sure that the ad revenue data is included in the reports {#check-reports}

1. View ads in the app.

2. Make sure that the [In-app and Ad Revenue](../../mobile-reports/revenue-report.md) report shows the same number of ad revenue events as the number of ad views.
