---
access_token: 'POST_CLIENT_ACCESS_TOKEN'
---

## Installation

### With [Cocoapods](http://cocoapods.org/)

In your Podfile:

    pod "Rollbar", "~> 0.1.3"

Make sure to declare your platform as `ios` at the top of your Podfile. E.g:

    platform :ios, '7.0'

### Without Cocoapods

1. Download the [Rollbar framework](https://github.com/rollbar/rollbar-ios/releases/download/v0.1.3/Rollbar.zip).

2. Extract the Rollbar directory in the zip file to your Xcode project directory.

3. In Xcode, select _File_ -> _Add Files to "[your project name]"_ and choose the Rollbar directory from step 2.

## Configuration

In your Application delegate implementation file, add the following import statement:

```objective-c
#import <Rollbar/Rollbar.h>
```

Then add the following to `application:didFinishLaunchingWithOptions:`:

```objective-c
[Rollbar initWithAccessToken:@"{{ access_token }}"];
```

That's all you need to do to report crashes to Rollbar. To get symbolicated stack traces, follow the instructions in the "Symbolication" section below.

### Crash reporting

Crashes will be saved to disk when they occur, then reported to Rollbar the next time the app is launched.

Rollbar uses [PLCrashReporter](https://www.plcrashreporter.org/) to capture uncaught exceptions and fatal signals. Note that only one crash reporter can be active per app. If you initialize multiple crash reporters (i.e. Rollbar alongside other services), only the last one initialized will be active.

### Logging

You can log arbitrary messages using the log methods:

```objective-c
// Logs at level "info".
// Variants at "debug", "info", "warning", "error", and "critical" all exist.
[Rollbar infoWithMessage:@"Test message"];

// Log a critical, with some additional key-value data
[Rollbar criticalWithMessage:@"Unexcpected data from server" data:@{@"endpoint": endpoint,
                                                                    @"result": result}];

// Or log at a named level
[Rollbar logWithLevel:@"warning" message:@"Simple warning log message"];
```

For additional configuration information, see the documentation for [rollbar-ios](https://github.com/rollbar/rollbar-ios).

