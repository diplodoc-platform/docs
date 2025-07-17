In AppMetrica, a session is the period of time a user interacts with the app.

**Background session**

A background session starts with the AppMetrica SDK initialization.

If, during a background session, AppMetrica receives the [`onResume()`](https://developer.android.com/guide/components/activities/activity-lifecycle#onresume) system event for Android or the [`UIApplicationDidBecomeActiveNotification`](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification) system event for iOS, a user session begins.

Any events sent before these system events refer to background sessions.

A background session can refer to:

- A period of time between clicking an app icon and displaying the app's interface.
- Start of services that accept push notifications.

**User session**

A user session starts when AppMetrica receives the following system events:

- For Android: [`onResume()`](https://developer.android.com/guide/components/activities/activity-lifecycle#onresume).
- For iOS: [`UIApplicationDidBecomeActiveNotification`](https://developer.apple.com/documentation/uikit/uiapplicationdidbecomeactivenotification).

A user session ends when the session timeout expires. The session timeout is counted from the moment the user minimizes the app.

Any events sent after the system events mentioned above refer to user sessions.

By default, AppMetrica considers a session new if a user returns to the app after a [significant period of time](*timeout-session) after the app switched to background mode (the user minimized the app or opened system settings).
