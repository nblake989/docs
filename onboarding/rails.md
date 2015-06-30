---
access_token: 'POST_SERVER_ACCESS_TOKEN'
---
## Installation

To send errors to Rollbar from your Ruby application you should use
[rollbar-gem](http://github.com/rollbar/rollbar-gem) notifier library.

If you're using bundler, add

```ruby
gem 'rollbar', '~> 1.5.3'
```

and run

```sh
bundle install
```

otherwise you can simply

```sh
gem install rollbar
```

## Add Rollbar to Your Rails Application


Run the following command from your Rails root:

```bash
$ rails generate rollbar {{ access_token }}
```

That will create the file ```config/initializers/rollbar.rb```, which initializes Rollbar and holds your access token and other configuration values.

If you want to store your access token outside of your repo, run the same command without arguments and create an environment variable ```ROLLBAR_ACCESS_TOKEN``` that holds your server-side access token:

```bash
$ rails generate rollbar
$ export ROLLBAR_ACCESS_TOKEN={{ access_token }}
```

For Heroku users:

If you're on Heroku, you can store the access token in your Heroku config:

```bash
$ heroku config:add ROLLBAR_ACCESS_TOKEN={{ access_token }}
```

To confirm that your application is properly configured, run:

```bash
$ rake rollbar:test
```

This will raise an exception within a test request; if it works, you'll see a stacktrace in the console, and the exception will appear in the Rollbar dashboard.


