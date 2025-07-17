To send your own error message, use the following methods:

- `AppMetrica.reportError(String message, Throwable error)`
- `AppMetrica.reportError(String groupIdentifier, String message)`
- `AppMetrica.reportError(String groupIdentifier, String message, Throwable error)`

{% cut "Example with groupIdentifier" %}

If you send errors using methods with groupIdentifier, they are grouped by ID.

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   try {
       "00xffWr0ng".toInt()
   } catch (error: Throwable) {
       AppMetrica.reportError("Your ID", "Error while parsing some integer number", error)
   }
   ```

- Java

   ```java translate=no
   try {
       Integer.valueOf("00xffWr0ng");
   } catch (Throwable error) {
       AppMetrica.reportError("Your ID", "Error while parsing some integer number", error);
   }
   ```

{% endlist %}

Don't use variable values as grouping IDs. Otherwise, the number of groups increases and it becomes difficult to analyze them.

{% if locale == 'ru' %}<img src="{{ groupIdentifier }}">{% endif %}
{% if locale == 'en' %}<img src="{{ groupIdentifier-en }}">{% endif %}

{% endcut %}

{% cut "Example with message" %}

If errors are sent using the `AppMetrica.reportError(String message, Throwable error)` method, they are grouped by [stack trace](https://en.wikipedia.org/wiki/Stack_trace).

{% list tabs group=instructions %}

- Kotlin

   ```kotlin translate=no
   try {
       "00xffWr0ng".toInt()
   } catch (error: Throwable) {
       AppMetrica.reportError("Error while parsing some integer number", error)
   }
   ```

- Java

   ```java translate=no
   try {
       Integer.valueOf("00xffWr0ng");
   } catch (Throwable error) {
       AppMetrica.reportError("Error while parsing some integer number", error);
   }
   ```

{% endlist %}

{% if locale == 'ru' %}<img src="{{ stack-trace }}">{% endif %}
{% if locale == 'en' %}<img src="{{ stack-trace-en }}">{% endif %}

{% endcut %}
\ No newline at end of file
