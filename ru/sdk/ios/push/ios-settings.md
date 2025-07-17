# Настройка приложения на базе iOS для отправки push-уведомлений

Для отправки push-уведомлений в iOS-приложения используется Universal Push Notification Client SSL Certificate. При получении этого сертификата необходимо указать идентификатор вашего приложения (App ID). Его можно [создать в кабинете разработчика Apple](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).

Если App ID уже создан, отправьте запрос на сертификат.

## Шаг 1. Отправьте запрос на сертификат

1. На вашем компьютере запустите приложение **Keychain Access**.
2. Перейдите в раздел **Keychain Access** → **Certificate Assistant** → **Request a Certificate From a Certificate Authority** и введите необходимые данные. Обратите внимание на пароль. Он потребуется во время привязки сертификата в интерфейсе AppMetrica.
3. В блоке **Request is** включите опцию **Saved to disk** и нажмите кнопку **Continue**.
4. Сохраните файл запроса на компьютере и нажмите кнопку **Done**.

## Шаг 2. Получите сертификат

1. В кабинете разработчика Apple перейдите в раздел [Certificates, Identifiers & Profiles](https://developer.apple.com/account/ios/certificate).
2. В меню **Certificates** выберите **All** и перейдите в раздел **Production**.
3. Включите опцию **Apple Push Notification service SSL (Sandbox & Production)** и нажмите кнопку **Continue**.
4. В выпадающем списке **App ID** выберите идентификатор приложения, для которого требуется сертификат, и нажмите кнопку **Continue**. Выбранный **App ID** должен совпадать с вашим **bundle ID**.
5. Так как запрос на сертификат был отправлен ранее, нажмите кнопку **Continue**.
6. Нажмите кнопку **Choose File**. В появившемся окне выберите файл запроса на сертификат (например `example.certSigningRequest`) и нажмите кнопку **Choose**, а затем **Continue**.
7. Загрузите сертификат, нажав кнопку **Download**. Затем нажмите кнопку **Done**.
8. Установите сертификат с помощью двойного нажатия на файл.

## Шаг 3. Экспортируйте Private Key из установленного сертификата

1. На вашем компьютере откройте программу Keychain Access и выберите пункт меню **Certificates**.
2. Выберите в списке сертификат, который вы установили.
3. Выберите пункт меню **File** → **Export Items**. Затем укажите имя для экспортируемого файла и формат Personal Information Exchange (P12). Нажмите кнопку **Save**.
4. Задайте пароль для ключа в поле **Password** и нажмите кнопку **Ok**. Если вы не зададите пароль, сертификат не будет принят в интерфейсе AppMetrica.
5. Введите пароль от вашего компьютера, чтобы активировать экспорт. Затем нажмите кнопку **Allow**. Файл в формате P12 сохранится на компьютере.

## Шаг 4. Используйте Private Key в AppMetrica

1. В интерфейсе AppMetrica перейдите в раздел {% if locale == "ru" %}[Приложения](https://appmetrika.yandex.ru/application/list){% endif %}{% if locale == "en" %}[Приложения](https://appmetrica.yandex.com/application/list){% endif %} и выберите приложение, для которого вы хотите проводить push-кампании.
2. В меню слева выберите пункт **Настройки**.
3. Перейдите на вкладку **Push-уведомления**.
4. В блоке **iOS** нажмите кнопку **Выбрать файл** (напротив поля **Universal Push Notification Client SSL Certificate**).
5. В появившемся окне выберите файл ключа в формате P12 и загрузите его.
6. В поле **Пароль** введите пароль, заданный при сохранении ключа (шаг 3).

## См. также

- [Подключение и инициализация AppMetrica Push SDK](quick-start.md)
- [Запуск push-кампании](../../../push/marketing.md)

{{ feedback }}

<a href="../../../troubleshooting/feedback-new.html">
  <span class="button">Написать в службу поддержки</span>
</a>

{% include notitle [feedback](../../../_includes/feedback-button.md) %}
