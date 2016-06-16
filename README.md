# Flash Messages
### What is a flash message?
  A flash message is a notification on the page that displays important
  information to the user for a limited time.

### Why use flash messages?
  Building a usable web app hinges on keeping the user informed of what is going
  on and why things happen. Flash messages allow us to communicate important info
  to the user in a simple and relatively unobtrusive way to keep them informed.

### How do they work?
A flash message:
* is simply just a hash stored in the session object
* is cleared out in the next request (unless otherwise modified)
* is available the both ActionView::Base and ActionController::Base because it is stored in the session

### Where do we create a flash message?
Flash messages are added in the controller.

### What kinds of flash messages are there?
The two most common kinds of flash messages are:
* Notices - most commonly seen as `flash[:notice]`
* Alerts - most commonly seen as `flash[:alert]`
Because flash is a hash, you can technically name a flash message anything you want. For and example see [Parley's flash hash layout](https://github.com/custombit/parleysdieselperformance/blob/master/app/views/layouts/_flash_hash.html.haml)

### Is there a prettier/preferred syntax when adding a flash message?
Of course there is, the `flash[:notice]` syntax is hardly pretty enough for your beautiful code!
There have been convenience accessors** added for both `[:notice]` and `[:alert]`
* Instead of the `[:notice]` use the `.notice` method
```
flash.notice = 'This looks so much better!'
```
* Instead of the `[:alert]` use the `.alert` method
```
flash.alert = 'You look so fabulous without those brackets!'
```

** An accessor creates both a read and a write method to "set" and "get" a value.

### How to change the message duration?
A typical flash message will persist to the next action before "disappearing". Using `redirect_to` causes a page load action.

However, there are time when we do not want the flash message to persist to the next action, such as when using `render`. In this case we can use `.now`, which is only available to the current action.
```
flash.now.alert = 'You will only see on this page.'
```

If we want extend the persistance of a flash message another action, we can simply use the `.keep` method. We can choose if we want all of some of the flash has to be "kept" by passing in optional arguments.
```
# Keep the entire flash message
flash.keep
flash.notice = 'This will stick around...'

# Keep only the flash alert
flash.keep(:alert)
flash.notice = 'This will not last...'
flash.alert = 'This will stick around...'
```
