# AppMetrica

AppMetrica is a set of libraries for collecting app usage statistics, creating and running push campaigns, and collecting statistics for those campaigns. You can see the data you've collected in the {% if locale == 'ru' %}[AppMetrica web interface](https://appmetrica.yandex.ru/){% endif %}{% if locale == 'en' %}[AppMetrica web interface](https://appmetrica.yandex.com/){% endif %}.

AppMetrica includes the following libraries:

- AppMetrica SDK lets you collect statistics about your app and its users. This may include information about sessions, the number of users who have installed the app, traffic sources for the app download page, and more.
- AppMetrica Push SDK, for working with push notifications and tracking push campaigns.

The SDK lets you track the following data:

- device information
- session information
- referral information (how the user got to the app download page)
- user actions inside the app
- user location
- errors that occurred during app usage
- custom events
- other data (such as the number of users who have installed the app)

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  column-gap: 50px;
  row-gap: 20px;
}
.grid-item {
  display: flex;
  flex-direction: column;
  box-shadow: 0 4px 24px rgba(0, 0, 0, .05), 0 2px 8px rgba(0, 0, 0, .05);
  border-radius: 24px;
  padding: 32px;
}
h2 {
  padding-top: 32px !important;
  margin-top: 0 !important;
}
h3 {
  padding-top: 8px !important;
  margin-top: 0 !important;
}
</style>

<div class="grid-container">
    <div class="grid-item">
        <h3><a href="android">Android</a></h3>
        <p><b>Latest SDK versions:</b>
        <ul>
        <li>AppMetrica SDK: {{ io-appmetrica-analytics-analytics }}</li>
        <li>AppMetrica Gradle Plugin: {{ io-appmetrica-analytics-gradle }}</li>
        <li>AppMetrica Push SDK: {{ push-sdk-android-version }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="ios">iOS</a></h3>
        <p><b>Latest SDK versions:</b>
        <ul>
        <li>AppMetrica SDK: {{ ios-appmetrica-sdk-version }}</li>
        <li>AppMetrica Push SDK: {{ ios-push-sdk }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="unity">Unity</a></h3>
        <p><b>Latest plugin versions:</b>
        <ul>
        <li>AppMetrica SDK plugin: {{ appmetrica-unity-plugin }}</li>
        <li>AppMetrica Push SDK plugin: {{ appmetrica-push-unity-plugin }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="flutter">Flutter</a></h3>
        <p><b>Latest plugin versions:</b>
        <ul>
        <li>AppMetrica SDK plugin: {{ appmetrica-flutter-plugin }}</li>
        <li>AppMetrica Push SDK plugin: {{ appmetrica-push-flutter-plugin }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="react-native">React Native</a></h3>
        <p><b>Latest plugin versions:</b>
        <ul>
        <li>AppMetrica SDK plugin: {{ appmetrica-react-native-plugin }}</li>
        </ul>
        </p>
    </div>
</div>
