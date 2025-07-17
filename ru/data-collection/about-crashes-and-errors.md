# Крэши/ошибки

AppMetrica позволяет собирать информацию об аварийных остановках приложения (крэшах) и ошибках. Их можно анализировать в отчетах [Крэши/Ошибки](../mobile-reports/crashes-and-errors.md).

Основные возможности анализа крэшей/ошибок в AppMetrica:

**Автоматическая загрузка mapping, SO и dSYM-файлов при сборке**

:   Информация о крэшах и ошибках на Android может отправляться в обфусцированном виде, на iOS — в десимволизированном. Из таких логов сложно извлечь данные для анализа. Чтобы логи можно было анализировать, загрузите mapping, SO или dSYM-файлы в AppMetrica.

    AppMetrica поддерживает автоматическую загрузку mapping, SO и dSYM-файлов при сборке приложения и ручную загрузку через веб-интерфейс. Подробнее в разделах:

    - [Загрузка mapping-файлов и отладочных символов на Android](upload-mapping.md).
    - [Загрузка dSYM-файлов на iOS](upload-dsym.md).

**Группировка**

:   Крэш-логи группируются в крэш-группы по [stack trace](https://en.wikipedia.org/wiki/Stack_trace).

    Группировка ошибок зависит от метода, с помощью которого они отправляются. См. в разделе [{#T}](#send-report-error).

    Внутри группы отображаются все устройства, на которых происходят крэши/ошибки. Из каждой группы можно посмотреть полный лог на конкретном устройстве.

**Открытие/закрытие крэша или ошибки**

:   Чтобы отфильтровать из отчета исправленные крэши/ошибки, их можно закрывать. Если после закрытия они будут обнаружены в версиях, в которых их ранее не было, крэш/ошибка переоткроется.

**Провязка с карточкой профиля**

:   Чтобы посмотреть события, которые предшествовали крэшу/ошибке, из лога можно перейти в [карточку профиля](../mobile-reports/profile-list.md).

**Комментарии к группе**

:   Для каждой группы можно добавить комментарий. Например, в комментарии можно вставить ссылку на задачу в трекере.

## Отправка собственного сообщения об ошибке {#send-report-error}

Примеры отправки собственного сообщения об ошибке на платформах:

- [Android](../sdk/android/analytics/android-operations.md#send-report-error)
- [iOS](../sdk/ios/analytics/ios-operations.md#send-report-error)
- [Flutter](../sdk/flutter/analytics/flutter-operations.md#send-report-error)  
- [React Native](../sdk/react-native/analytics/react-native-operations.md#send-report-error) 
- [Unity](../sdk/unity/analytics/unity-operations.md#send-report-error)

## Узнать больше {#learn-more}

- [Отчет Крэши и ошибки](../mobile-reports/crashes-and-errors.md)
- [Загрузка mapping-файлов и отладочных символов на Android](upload-mapping.md)
- [Загрузка dSYM-файлов на iOS](upload-dsym.md)
- [Документация Android](https://developer.android.com/topic/performance/vitals/crash)
- [Документация Apple](https://developer.apple.com/library/archive/technotes/tn2151/_index.html)

{{ feedback }}

<a href="../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../_includes/feedback-button.md) %}
