# Uploading attached files

{% note info %}

You can add attachments in the Push API using the [Sending push messages](../../../mobile-api/push/post-send-batch.md) operation (the `attachments` parameter).

{% endnote %}

Configure uploading attached files in push notifications by calling the downloadAttachmentsForNotificationRequest method ([objective-c](objectivec/AMPAppMetricaPush.md#method_downloadAttachmentsForNotificationRequest)/[swift](swift/AppMetricaPush.md#method_downloadAttachmentsForNotificationRequest)):

**Objective-C**
:   ```objectivec translate=no
    @implementation NotificationService

    - (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
        self.contentHandler = contentHandler;
        self.bestAttemptContent = [request.content mutableCopy];

        [AMPAppMetricaPush setExtensionAppGroup:@"EXTENSION_AND_APP_SHARED_APP_GROUP_NAME"];
        [AMPAppMetricaPush handleDidReceiveNotificationRequest:request];

        [AMPAppMetricaPush downloadAttachmentsForNotificationRequest:request
                                                               callback:^(NSArray<UNNotificationAttachment *> *attachments, NSError *error) {
                                                                   if (error != nil) {
                                                                       NSLog(@"Error: %@", error);
                                                                   }
                                                                   [self completeWithBestAttemptAndAttachments:attachments];
                                                               }];
    }

    - (void)serviceExtensionTimeWillExpire {
        [self completeWithBestAttemptAndAttachments:nil];
    }

    - (void)completeWithBestAttemptAndAttachments:(NSArray<UNNotificationAttachment *> *)attachments
    {
        @synchronized (self) {
            if (self.contentHandler != nil) {
                if (attachments != nil) {
                    self.bestAttemptContent.attachments = attachments;
                }
                self.contentHandler(self.bestAttemptContent);
                self.contentHandler = nil;
            }
        }
    }

    @end
    ```

**Swift**
:   ```swift translate=no
    class NotificationService: UNNotificationServiceExtension {

        private var contentHandler: ((UNNotificationContent) -> Void)?
        private var bestAttemptContent: UNMutableNotificationContent?
        private let syncQueue = DispatchQueue(label: "NotificationService.syncQueue")

        override func didReceive(_ request: UNNotificationRequest, withContentHandler contentHandler: @escaping (UNNotificationContent) -> Void) {
            self.contentHandler = contentHandler
            self.bestAttemptContent = (request.content.mutableCopy() as? UNMutableNotificationContent)

            // ...

            AppMetricaPush.downloadAttachments(for: request) { attachments, error in
                if let error = error {
                    print("Error: \(error)")
                }
                self.completeWithBestAttempt(attachments: attachments)
            }
        }

        override func serviceExtensionTimeWillExpire() {
            completeWithBestAttempt(attachments: nil)
        }

        func completeWithBestAttempt(attachments: [UNNotificationAttachment]?) {
            syncQueue.sync {
                if let contentHandler = contentHandler, let bestAttemptContent = bestAttemptContent {
                    if let attachments = attachments {
                        bestAttemptContent.attachments = attachments
                    }
                    contentHandler(bestAttemptContent)
                    self.bestAttemptContent = nil
                    self.contentHandler = nil
                }
            }
        }

    }
    ```

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
