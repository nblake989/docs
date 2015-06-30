---
access_token: 'POST_CLIENT_ITEM_ACCESS_TOKEN'
---
## Installation

Download the Rollbar [rollbar-php](https://github.com/rollbar/rollbar-php) notifier
and place rollbar.php somewhere in your path.

## Send a Message to Rollbar

Add the following code to one of your PHP pages:

```php
<?php
// installs global error and exception handlers
Rollbar::init(array('access_token' => '{{ access_token }}'));

// Message at level 'info'
Rollbar::report_message('testing 123', 'info');

// Catch an exception and send it to Rollbar
try {
    throw new Exception('test exception');
} catch (Exception $e) {
    Rollbar::report_exception($e);
}

// Will also be reported by the exception handler
throw new Exception('test 2');
?>
```

Within a few seconds of loading this page, the message and errors should appear in your Rollbar dashboard.

Once you've verified you have the notifier library installed, your access token works,
and you can connect to rollbar, the [rollbar-php](https://github.com/rollbar/rollbar-php)
documentation can show you how to automatically report exceptions and log message to Rollbar.
