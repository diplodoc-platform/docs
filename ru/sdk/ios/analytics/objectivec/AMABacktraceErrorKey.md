# AMABacktraceErrorKey

```objectivec translate=no
extern NSErrorUserInfoKey const AMABacktraceErrorKey
```

Ключ из словаря `userInfo` ошибки `NSError`. Должен содержать бэктрейс ошибки. Вы можете получить его с помощью методов [NSThread.callStackReturnAddresses](https://developer.apple.com/documentation/foundation/nsthread/1409565-callstackreturnaddresses?language=objc).

АppMetrica автоматически парсит переданное значение.
