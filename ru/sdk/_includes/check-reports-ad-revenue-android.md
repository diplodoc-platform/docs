## Шаг 1 Убедитесь, что SDK активирован {#activate}

Пример активации:

```java translate=no
AppMetricaConfig config = AppMetricaConfig.newConfigBuilder(API_KEY).build();
AppMetrica.activate(context, config);
```

## Шаг 2. Убедитесь, что Ad Revenue отображается в отчетах {#check-reports}

1. Совершите просмотры рекламы в приложении.

2. Убедитесь, что в отчете [In-app и Ad Revenue](../../mobile-reports/revenue-report.md) количество событий Ad Revenue соответствует количеству просмотров рекламы.
