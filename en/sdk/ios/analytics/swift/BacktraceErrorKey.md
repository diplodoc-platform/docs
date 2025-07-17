# BacktraceErrorKey

```swift translate=no
let BacktraceErrorKey: String
```

A key from the `userInfo` dictionary of an `NSError`. It should contain the error backtrace. You can get it using the [Thread.callStackReturnAddresses](https://developer.apple.com/documentation/foundation/thread/1409565-callstackreturnaddresses) methods.

AppMetrica automatically parses the passed value.
