{% note warning %}

Starting with version 4.0 of the AppMetrica SDK for iOS, app openings via deeplinks are tracked automatically. For other versions, set up tracking manually:

- iOS AppMetrica SDK version below 4.0. [Setting up](#ui-app-delegate) deeplink tracking for UIApplicationDelegate.
- [Setting up](#ui-scene-delegate) deeplink tracking for UISceneDelegate (AppMetrica doesn't track such app openings automatically).

{% endnote %}

You need to track app openings to correctly track [remarketing campaigns](*remarketing campaigns).

{% include [note_add_to_app_support_ios](../data-collection/_includes/note_add_to_app_support_ios.md) %}

### UISceneDelegate {#ui-scene-delegate}

{% list tabs group=instructions %}

- Objective-C

   To manually track app openings via universal links or deeplinks, in `UISceneDelegate`, add the following code to the [`scene:willConnectToSession:options:`](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene?language=objc) method:

   ```objectivec translate=no
   - (void)scene:(UIScene *)scene willConnectToSession:(UISceneSession *)session
   options:(UISceneConnectionOptions *)connectionOptions
   {
     //Universal Link
     NSUserActivity *userActivity = [[connectionOptions.userActivities allObjects] firstObject];
     if ([userActivity.activityType isEqualToString:NSUserActivityTypeBrowsingWeb]) {
       [AMAAppMetrica trackOpeningURL:context.URL];
     }
     else {
       //Deeplink
       UIOpenURLContext *context = [[connectionOptions.URLContexts allObjects] firstObject];
       if (context != nil) {
         [AMAAppMetrica trackOpeningURL:context.URL];
       }
     }
   }
   ```

   To manually track app openings via universal links or deeplinks in a running app, use the following code:

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

   To manually track app openings via universal links or deeplinks, in `UISceneDelegate`, add the following code to the [`scene(_:willConnectTo:options:)`](https://developer.apple.com/documentation/uikit/uiscenedelegate/3197914-scene) method:
   
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

   To manually track app openings via universal links or deeplinks in a running app, use the following code:

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

Manual setup of tracking with UIApplicationDelegate is relevant for iOS AppMetrica SDK versions below 4.0.

{% endnote %}

{% list tabs group=instructions %}

- Objective-C

   To manually track app openings via universal links or deeplinks, use the `+trackOpeningURL:` method of the `AMAAppMetrica` class.

   To manually track app openings using deeplinks or deeplink handling in a running app, use `UIApplicationDelegate` and add the following modifications:

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

   To manually track app openings via universal links or deeplinks, use the `+trackOpeningURL:` method of the `AMAAppMetrica` class.

   To manually track app openings using deeplinks or deeplink handling in a running app, use `UIApplicationDelegate` and add the following modifications:

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
