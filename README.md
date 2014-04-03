#flexpoint

Flexpoint is designed to make it easier for you to make style changes based on ambient data in the page and browser.

##What is Ambient Data?
Ambient data relates to the state of your page and browser. Things like how far the user has scrolled down the page, what's currently visible on the screen, how wide the browser window is, etc. 

##Getting Started
To start off, simply include flexpoint.js and the plugins that you'd like to use in your page. Then make one call to flexpoint.init() and pass it the config object. The config object is explained in more detail below in the "JavaScript API" section.

Flexpoint in and of itself doesn't provide any functionality. All the magic happens in the plugins. I've worked hard to make plugin creation as simple and straightforward as possible, please see the "Creating Plugins" section below for more info.

---

##The Config Object

`flexpoint.init` takes a single object that configures all the classes that you want flexpoint to apply and what plugins should be used when applying them. In the example below, a class of `scroll-header` will be applied to the body tag when the user scrolls 100px down the page. The `scrollTop` plugin will control this and the `min` value is part of the `scrollTop` plugin's supported config values. The plugin author can support any number of options, so you'll need to consult the plugin's documentation to know how each plugin can be used. The `scrollTop` plugin is provided as an example plugin in the flexpoint repo.

```javascript
flexpoint.init({
    'scroll-header': {
        'scrollTop': {
            min: 100
        }
    }
})
```

Now all that is left is to apply styles to the page that take advantage of this body class! *It's THAT simple!*

---

##JavaScript API

flexpoint has a JavaScript API which is used to configure flexpoint. It can also be used to hook into the flexpoint event bus.

###`flexpoint.init(config);`
- `config` => Object

The use of `init` was covered in `The Config Object` above.

---

###`flexpoint.on(event, class, handler);`
- `event` => String
- `class` => String
- `handler` => Function(event, class)

`on` is used to execute code when 1 of 3 events occur (enter, leave, update). `enter` is when a class goes from being inactive to active, `leave` is when a class goes from active to inactive, and `update` is every time flexpoint updates while the class is active. In the example below we execute `doSomething()` when the scroll-header class becomes active.

The handler gets passed 2 strings, the event, and the class.

```javascript
flexpoint.on('enter', 'scroll-header', doSomething);
```

---

###`flexpoint.off(event, class, handler);`
- `event` => String
- `class` => String
- `handler` => Function(event, class)

`off` is the opposite of `on` and is used to unregister handlers from an event and class.

```javascript
flexpoint.off('enter', 'scroll-header', doSomething);
```
---

###`flexpoint.isActive(class);`
- `class` => String

`returns` => boolean

`isActive` is used to check whether a given class is currently active or not.

```javascript
flexpoint.isActive('scroll-header'); // true
```
---

###`flexpoint.getPluginValue(pluginName);`
- `pluginName` => String

`returns` => current value

`getPluginValue` can be used to retrieve the current value that a plugin is watching for changes. In the instance of `scrollTop` the value returned is the number of pixels that the user has scrolled down the page.

```javascript
flexpoint.getPluginValue('scrollTop'); // 175
```

---

##Creating Plugins

Coming soon...