#Ambient.js

Ambient.js is designed to make it easier for you to make style changes based on ambient data in the page and browser.

###What is Ambient Data?
Ambient data relates to the state of your page and browser. Things like how far the user has scrolled down the page, what's currently visible on the screen, how wide the browser window is, etc. 

###Getting Started
To start off, simply include ambient.js and the plugins that you'd like to use in your page. Then make one call to ambient.init() and pass it the config object. The config object is explained in more detail below in the "JavaScript API" section.

Ambient.js in and of itself doesn't provide any functionality. All the magic happens in the plugins. I've worked hard to make plugin creation as simple and straightforward as possible, please see the "Creating Plugins" section below for more info.

###Examples
- [Sticky Header (scrollTop)](http://codepen.io/amwmedia/pen/dikcr/)

###Browser Compatibility
- Chrome
- Firefox
- IE 9+
- IE 8 (with [es5-shim](https://github.com/es-shims/es5-shim))

---

##The Config Object

`ambient.init` takes a single object that configures all the classes that you want ambient to apply and what plugins should be used when applying them. In the example below, a class of `scroll-header` will be applied to the body tag when the user scrolls 100px down the page. The `scrollTop` plugin will control this and the `min` value is part of the `scrollTop` plugin's supported config values. The plugin author can support any number of options, so you'll need to consult the plugin's documentation to know how each plugin can be used. The `scrollTop` plugin is provided as an example plugin in the ambient repo.

```javascript
ambient.init({
    'scroll-header': {   // the css class we want
        'scrollTop': {   // the plugin we will use
            min: 100     // config value for the plugin
        }
    }
})
```

Now all that is left is to apply styles to the page that take advantage of this body class! *It's THAT simple!*

---

##JavaScript API

Ambient.js has a JavaScript API which is used for configuration. It can also be used to hook into the ambient.js event bus.

###`ambient.init(config[, delay]);`
- `config`: Object
- `delay`: Number

The use of `init` was covered in `The Config Object` above. The optional `delay` parameter can be used to tell ambient how frequently you'd like to allow ambient to do an update. If set to 0, ambient will still limit the updates to once per requestAnimationFrame. This prevents overloading the browser by executing more often that could possibly be necessary.

---

###`ambient.on(action, class, handler);`
- `action`: String
- `class`: String
- `handler`: Function(action, class)

`on` is used to execute code when 1 of 3 actions occur (enter, leave, update). `enter` is when a class goes from being inactive to active, `leave` is when a class goes from active to inactive, and `update` is every time ambient updates while the class is active. In the example below we execute `doSomething()` when the scroll-header class becomes active.

The handler gets passed 2 strings, the action, and the class.

```javascript
ambient.on('enter', 'scroll-header', doSomething);
```

---

###`ambient.off(action, class, handler);`
- `action`: String
- `class`: String
- `handler`: Function(action, class)

`off` is the opposite of `on` and is used to unregister handlers from an event and class.

```javascript
ambient.off('enter', 'scroll-header', doSomething);
```
---

###`ambient.isActive(class);`
- `class`: String

`returns`: boolean

`isActive` is used to check whether a given class is currently active or not.

```javascript
ambient.isActive('scroll-header'); // true
```
---

###`ambient.getPluginValue(pluginName);`
- `pluginName`: String

`returns`: current value

`getPluginValue` can be used to retrieve the current value that a plugin is watching for changes. In the instance of `scrollTop` the value returned is the number of pixels that the user has scrolled down the page.

```javascript
ambient.getPluginValue('scrollTop'); // 175
```

---

##Creating Plugins

Full writup is coming soon... for now you can refer to template.js in the src/plugins folder for a starting point and description of all of the possible plugin functions. scrollTop.js in the same folder is a good example of a very basic plugin implementation.

---

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/40c470b679c786d2728cfe49642c0c03 "githalytics.com")](http://githalytics.com/amwmedia/ambient.js)