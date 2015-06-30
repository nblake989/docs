---
access_token: 'POST_SERVER_ACCESS_TOKEN'
---
## Installation

To send errors to Rollbar from your Python application you should use 
[pyrollbar](http://github.com/rollbar/pyrollbar) notifier library. Install pyrollbar with pip:

```python
pip install rollbar
```

## Add Rollbar to Your Django Application

In your ``ini`` file (e.g. ``production.ini``), add ``rollbar.contrib.pyramid`` to the end of your ``pyramid.includes``:

```
[app:main]
pyramid.includes =
    pyramid_debugtoolbar
    rollbar.contrib.pyramid
```
  
And add these rollbar configuration variables:

```
[app:main]
rollbar.access_token = POST_SERVER_ITEM_ACCESS_TOKEN
rollbar.environment = production
rollbar.branch = master
rollbar.root = %(here)s
```
<!-- RemoveNextIfProject -->
Be sure to replace ```POST_SERVER_ITEM_ACCESS_TOKEN``` with your project's ```post_server_item``` access token, which you can find in the Rollbar.com interface.

The above will configure Rollbar to catch and report all exceptions that occur inside your Pyramid app. However, in order to catch exceptions in middlewares or in Pyramid itself, you will also need to wrap your app inside a ```pipeline``` with Rollbar as a ```filter```.

To do this, first change your ```ini``` file to use a ```pipeline```. Change this:

```
[app:main]
#...
```

To:

```
[pipeline:main]
pipeline =
    rollbar
    YOUR_APP_NAME

[app:YOUR_APP_NAME]
pyramid.includes =
    pyramid_debugtoolbar
    rollbar.contrib.pyramid

rollbar.access_token = POST_SERVER_ITEM_ACCESS_TOKEN
rollbar.environment = production
rollbar.branch = master
rollbar.root = %(here)s

[filter:rollbar]
use = egg:rollbar#pyramid
access_token = POST_SERVER_ITEM_ACCESS_TOKEN
environment = production
branch = master
root = %(here)s
```

Note that the access_token, environment, and other Rollbar config params do need to be present in both the ```app``` section and the ```filter``` section.


For additional pyrollbar configuration options, see [Configuring pyrollbar](https://github.com/rollbar/pyrollbar).
