{% note warning %}

Начиная с версии AppMetrica SDK iOS 4.0, отслеживание открытия приложения через deeplink работает автоматически. Для остальных вариантов настройте отслеживание вручную:

- Версия AppMetrica SDK iOS ниже 4.0. [Настройка](#ui-app-delegate) отслеживания deeplink для UIApplicationDelegate.
- [Настройка](#ui-scene-delegate) отслеживания deeplink для UISceneDelegate (AppMetrica не отслеживает такие открытия автоматически).

{% endnote %}

Отслеживание открытий необходимо для корректного трекинга [ремаркетинг-кампаний](*ремаркетинг-кампаний).
  
{% include [note_add_to_app_support_ios](../data-collection/_includes/note_add_to_app_support_ios.md) %}

### UISceneDelegate {#ui-scene-delegate}

{% list tabs group=instructions %}

- Objective-C

  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink, в `UISceneDelegate` в метод [`scene:willConnectToSession:options:`](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc) добавьте код:

  ```objectivec translate=no
  - (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session
  options:(UISceneConnectionOptions *)connectionOptions
  {
    // Universal Link
    NSUserActivity *userActivity = [[connectionOptions.userActivities allObjects] firstObject];
    if ([userActivity.activityType isEqualToString:NSUserActivityTypeBrowsingWeb]) {
      [AMAAppMetrica trackOpeningURL:context.URL];
    }
    else {
      // Deeplink
      UIOpenURLContext *context = [[connectionOptions.URLContexts allObjects] firstObject];
      if (context != nil) {
        [AMAAppMetrica trackOpeningURL:context.URL];
      }
    }
  }
  ```

  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink в запущенном приложении, используйте код:

  ```objectivec translate=no
  - (void)scene:(UIScene *)scene continueUserActivity:(NSUserActivity *)userActivity
  {
    NSURL *url = userActivity.webpageURL;
    if ([userActivity.activityType isEqualToString:NSUserActivityTypeBrowsingWeb]) {
      [AMAAppMetrica trackOpeningURL:context.URL];
    }
  }

  - (void)scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts
  {
    UIOpenURLContext *context = [[URLContexts allObjects] firstObject];
    if (context != nil) {
      [AMAAppMetrica trackOpeningURL:context.URL];
    }
  }
  ```
  
- Swift

  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink, в `UISceneDelegate` в метод [`scene(_:willConnectTo:options:)`](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene) добавьте код:

  ```swift translate=no
  func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
      // Universal Link
      if let userActivity = connectionOptions.userActivities.first {
          if userActivity.activityType == NSUserActivityTypeBrowsingWeb,
             let url = userActivity.webpageURL {
              AppMetrica.trackOpeningURL(url)
          }
      }
      
      // Deep Link
      if let context = connectionOptions.urlContexts.first {
          AppMetrica.trackOpeningURL(context.url)
      }
  }
  ```

  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink в запущенном приложении, используйте код:

  ```swift translate=no
  func scene(_ scene: UIScene, continue userActivity: NSUserActivity) {
      guard userActivity.activityType == NSUserActivityTypeBrowsingWeb,
            let url = userActivity.webpageURL else { return }
      AppMetrica.trackOpeningURL(url)
  }
  
  func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
      guard let context = URLContexts.first else { return }
      AppMetrica.trackOpeningURL(context.url)
  }
  ```
  
{% endlist %}

### UIApplicationDelegate {#ui-app-delegate}

{% note warning %}

Ручная настройка отслеживания с UIApplicationDelegate актуальна для версии AppMetrica SDK iOS ниже 4.0.

{% endnote %}

{% list tabs group=instructions %}

- Objective-C
  
  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink, используйте метод `+trackOpeningURL:` класса `AMAAppMetrica`.
  
  Чтобы вручную отслеживать открытия приложения с помощью deeplink или обработку deeplink в запущенном приложении, используйте `UIApplicationDelegate` и добавьте следующие изменения:
  
  ```objectivec translate=no
  - (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
  {
      [AMAAppMetrica trackOpeningURL:url];
      return YES;
  }
  
  // Delegate for tracking Universal links.
  - (BOOL)application:(UIApplication *)application
      continueUserActivity:(NSUserActivity *)userActivity
      restorationHandler:(void (^)(NSArray * _Nullable))restorationHandler
  {
      if ([userActivity.activityType isEqualToString:NSUserActivityTypeBrowsingWeb]) {
          [AMAAppMetrica trackOpeningURL:userActivity.webpageURL];
      }
      return YES;
  }
  ```
  
- Swift
  
  Чтобы вручную отслеживать открытия приложения с помощью Universal Link/deeplink, используйте метод `+trackOpeningURL:` класса `AMAAppMetrica`.
  
  Чтобы вручную отслеживать открытия приложения с помощью deeplink или обработку deeplink в запущенном приложении, используйте `UIApplicationDelegate` и добавьте следующие изменения:
  
  ```swift translate=no
  func application(_ application: UIApplication, openURL url: URL, sourceApplication: String?, annotation: AnyObject) -> Bool {
      AppMetrica.trackOpeningURL(url)
      return true
  }
  
  // Delegate for tracking Universal links.
  func application(_ application: UIApplication, continue userActivity: NSUserActivity, restorationHandler: @escaping ([UIUserActivityRestoring]?) -> Void) -> Bool {
      if userActivity.activityType == NSUserActivityTypeBrowsingWeb {
          if let url = userActivity.webpageURL {
              AppMetrica.trackOpeningURL(url)
          }
      }
      return true
  }
  ```

{% endlist %}
