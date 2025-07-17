Сессия в AppMetrica — период взаимодействия пользователя с приложением.

**Фоновая сессия**

Фоновая сессия начинается с инициализации AppMetrica SDK.

Если во время фоновой сессии AppMetrica получила системное событие [`onResume()`](https://developer.android.com/guide/components/activities/activity-lifecycle#onresume) для Android или [`UIApplicationDidBecomeActiveNotification`](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification) для iOS, то начинается пользовательская сессия.

Все события, которые были отправлены до системных событий, относятся к фоновой сессии.

Примеры фоновой сессии:
  
- Период от нажатия на иконку приложения до отображения интерфейса.
- Запуск сервисов, принимающих push-уведомления.

**Пользовательская сессия**

Пользовательская сессия начинается, когда AppMetrica получает системные события:

- Для Android: [`onResume()`](https://developer.android.com/guide/components/activities/activity-lifecycle#onresume).
- Для iOS: [`UIApplicationDidBecomeActiveNotification`](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification).

Пользовательская сессия заканчивается, когда истекает таймаут сессии. Таймаут сессии отсчитывается с момента сворачивания приложения.

Все события, которые были отправлены после системных событий, относятся к пользовательской сессии.

По умолчанию AppMetrica считает сессию новой, если пользователь вернулся в приложение через [продолжительный промежуток](*timeout-session) времени после того, как приложение переключилось в фоновый режим (пользователь свернул приложение, открыл системные настройки).
