# AppMetrica

AppMetrica — набор библиотек для сбора статистики использования приложения, для создания и ведения push-кампаний и сбора статистики по ним. Собранные данные можно просматривать в {% if locale == 'ru' %}[веб-интерфейсе AppMetrica](https://appmetrica.yandex.ru/){% endif %}{% if locale == 'en' %}[AppMetrica web interface](https://appmetrica.yandex.com/){% endif %}.

AppMetrica включает в себя следующие библиотеки:

- AppMetrica SDK — позволяет получать статистическую информацию о приложении и его пользователях. Например, информацию о сессиях, количестве пользователей, установивших приложение, источниках их переходов на страницу скачивания приложения и другое.
- AppMetrica Push SDK — позволяет работать с push-уведомлениями и отслеживать ход push-кампании.

SDK позволяет отслеживать следующие данные:

- информация об устройстве;
- информация о сессиях;
- информация об источнике перехода пользователя на страницу скачивания приложения;
- действия, выполненные пользователем в приложении;
- местоположение пользователя;
- ошибки, возникающие во время использования приложения;
- собственные события;
- другие данные (например, количество пользователей, установивших приложение).

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
        <p><b>Актуальные версии SDK:</b>
        <ul>
        <li>AppMetrica SDK: {{ io-appmetrica-analytics-analytics }}</li>
        <li>AppMetrica Gradle Plugin: {{ io-appmetrica-analytics-gradle }}</li>
        <li>AppMetrica Push SDK: {{ push-sdk-android-version }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="ios">iOS</a></h3>
        <p><b>Актуальные версии SDK:</b>
        <ul>
        <li>AppMetrica SDK: {{ ios-appmetrica-sdk-version }}</li>
        <li>AppMetrica Push SDK: {{ ios-push-sdk }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="unity">Unity</a></h3>
        <p><b>Актуальные версии плагина:</b>
        <ul>
        <li>AppMetrica SDK: {{ appmetrica-unity-plugin }}</li>
        <li>AppMetrica Push SDK: {{ appmetrica-push-unity-plugin }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="flutter">Flutter</a></h3>
        <p><b>Актуальные версии плагина:</b>
        <ul>
        <li>AppMetrica SDK: {{ appmetrica-flutter-plugin }}</li>
        <li>AppMetrica Push SDK: {{ appmetrica-push-flutter-plugin }}</li>
        </ul>
        </p>
    </div>
    <div class="grid-item">
        <h3><a href="react-native">React Native</a></h3>
        <p><b>Актуальные версии плагина:</b>
        <ul>
        <li>AppMetrica SDK: {{ appmetrica-react-native-plugin }}</li>
        </ul>
        </p>
    </div>
</div>
