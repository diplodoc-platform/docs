# Migrating from GCM to Firebase

Since the AppMetrica Push SDK version 0.2.0, it uses the Firebase Cloud Messaging (FCM) service to send push messages on the Android platform.

This section explains the steps for migrating the application from Google Cloud Messaging to Firebase Cloud Messaging.

## Step 1. Import a project

Import a Google project (if you used Google APIs to create a project):

1. Go to the [Firebase console](https://console.firebase.google.com/).
2. Click the **Add project** button.
3. In the drop-down list, select the name of the project you are planning to run push campaigns for.
4. Select the country your organization is officially registered in and click **Add Firebase**.
5. Click **Add Firebase to your Android app** and follow the instructions.

## Step 2. Configuring your app

Edit the `AndroidManifest.xml` file:

1. Rename `ymp_gcm_project_number` to `ymp_gcm_default_sender_id` and get the following result:

   ```xml translate=no
   <meta-data android:name="ymp_gcm_default_sender_id" android:value="number:SENDER_ID"/>
   ```

   {{ sender-id }}

2. Add the following to the `application` element:

   ```xml translate=no
   <meta-data android:name="ymp_firebase_default_app_id" android:value="APP_ID"/>
   ```

   {{ app-id }}

{{ feedback }}

<a href="../../../troubleshooting/feedback-new">
  <span class="button">Contact support</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
