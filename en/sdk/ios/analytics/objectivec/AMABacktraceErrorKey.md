# AMABacktraceErrorKey

```objectivec translate=no
extern NSErrorUserInfoKey const AMABacktraceErrorKey
```

A key from the `userInfo` dictionary of an `NSError`. It should contain the error backtrace. You can get it using the [NSThread.callStackReturnAddresses](https://developer.apple.com/documentation/foundation/nsthread/1409565-callstackreturnaddresses?language=objc) methods.

AppMetrica automatically parses the passed value.
