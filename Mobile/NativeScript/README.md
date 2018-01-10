# NativeScript

Cross-plaform mobile framework that generates __*native*__ mobile apps (not webviews) through Javascript and CSS.

This framework is backed by [Telerik](https://www.telerik.com/) and [Progress](https://www.progress.com/).

## Contents

* [Learning](#learning)
* [Installation](#installation)
* [Debugging](#debugging)
* [Writing Apps](#writing-apps)
* [Modules](#modules)

## Learning

There is a tutorial provided by NativeScript as either [text-based](https://docs.nativescript.org/tutorial) or [video](https://courses.nativescripting.com/courses/171132/lectures/2573585).

## Installation

Installation and interaction with NativeScript is done through CLI (command line). Follow the [getting started](https://docs.nativescript.org/start/quick-setup) guide. Be sure to use `tns doctor` to confirm installation.

## Debugging

Use the `tns run` command to start your app. While the app is running, live changes can be made to the code and the watcher will automagically persist to the running application.

```bash
$ tns run android
$ tns run ios
```

### Tips

* Live updates will not work when new dependencies are added. 
* `console.log` can be used to print primitive values to the console. 
* `console.dir` should be used to output objects.

## Writing Apps

NativeScript apps use [CommonJS](http://eng.wealthfront.com/2015/06/16/an-introduction-to-commonjs/) syntax.

### Contents

* [Structure](#structure)
* [Layouts](#layouts)
* [CSS](#css)
* [Images](#images)
* [Code Behind](#code-behind)
* [View Model](#view-model)

### Structure

An app is divided into multiple folders and files:

* `app` - where views and logic exist. Most time spent coding will be here.
* `app/App_Resources` - platform specific resources such as configuration files, icons, splash screens, etc.
* `app/shared` - files to be shared across views
* `app/views` - the views for the app with subfolders for each view. Each view contains a `.xml`, `.js`, and optional `.css`.
* `app/app.css` - global styling for the app
* `app/app.js` - starting point for the app 
* `hooks` - preprocessor scripts
* `node_modules` - npm dependencies including cross-platform `tns-core-modules`
* `platforms` - platform specific code needed to build for each. Files here are generated from `tns build` and should be treated as read-only and ignored in Git.
* `package.json`

### Layouts

See [documentation](https://docs.nativescript.org/ui/layouts), check out [some code samples](https://docs.nativescript.org/angular/code-samples/ui/layouts), and look into an [in-depth analysis](https://developer.telerik.com/featured/demystifying-nativescript-layouts/) for each layout. 

### CSS

See [documentation](https://docs.nativescript.org/ui/styling) on styling. CSS can be applied to an app globally, per page, and inline using the `style` attribute. Rule of thumb is to generally avoid inline styles and to make a conscience effort to place CSS correctly as gloablly or for a specific page.

For platform specific styling, add `@import url('~/platform.css');` as the first statment in the `app.css` file. Then, add specific style values to either the `platform.android.css` or `platform.ios.css` file.

### Images

Images can be referenced with a URL from a website, relative to the `app/images` folder (`~/images/logo.png`), or use platform specific resources (`res://logo_login`). Platform specific is the preferred way to reference images to deal with varying resolutions. Those images are to be put in the `app/App_Resources` folder in the appropriate spots.

A helpful tool to create images for varying resolutions is the [NativeScript Image Builder](http://nsimage.brosteins.com/).

### Code Behind

Named identically as the view. 

Navigation can be performed here using the [frame](#frame) module.

Adding an id to a view element allows access to it in the code behind through the page's `page.getViewById('your_id')` method.

### View Model

[Observable](#observable) is the module that is used as the view model.

A page's binding context can be set to an observable module (i.e the view model):

```js
var observableModule = require('data/observable');

var user = new observableModule.fromObject({
    email: 'user@domain.com',
    password: 'password'
})

page.bindingContext = user;
```

## Modules

Note: Not experienced in all modules, but each are worth evaluating for use.

* https://market.nativescript.org/
* https://www.npmjs.com/ 


### Frame

The [Frame module](https://docs.nativescript.org/cookbook/ui/frame) is used to perform navigation.

```js
var frameModule = require('ui/frame');

frameModule.topmost().navigate('views/myView/myView');
```

### Observable

The [Observable module](https://docs.nativescript.org/cookbook/data/observable) is used as the view model in the MVVM convention.

```js
require('data/observable');
```

There is also an [Observable Array module](https://docs.nativescript.org/cookbook/data/observable-array) that can be used to bind an array collection.

```js
var ObservableArray = require("data/observable-array").ObservableArray;

var pageData = new observableModule.fromObject({
    groceryList: new ObservableArray([
        { name: "eggs" },
        { name: "bread" },
        { name: "cereal" }
    ])
});
```

### Fetch

The [Fetch module](https://docs.nativescript.org/cookbook/fetch) is used to make remote requests. It can be accessed globally in NativeScript without having to require it with simply `fetch()`.

```js
// This is not necessary, but shown for context
require('fetch')
```

### Dialogs

The [Dialogs module](https://docs.nativescript.org/ui/dialogs) can be used to display a variety of dialogs from action sheets, confirmation boxes, alerts, and prompts.

```js
require('ui/dialogs')
```

### Notifications

* https://code.tutsplus.com/tutorials/code-a-real-time-app-with-nativescript-push-notifications--cms-29475
* https://github.com/NativeScript/push-plugin
* https://github.com/EddyVerbruggen/nativescript-local-notifications

Firebase

* https://github.com/EddyVerbruggen/nativescript-plugin-firebase

### Offline Capabilities

SQLite

* https://github.com/NathanaelA/nativescript-sqlite
* https://code.tutsplus.com/tutorials/code-a-real-time-nativescript-app-sqlite--cms-29057

Check connectivity

* https://docs.nativescript.org/cookbook/connectivity
* https://www.thepolyglotdeveloper.com/2017/07/determine-network-availability-nativescript-angular-mobile-app/

### Camera / Media

* https://docs.nativescript.org/hardware/camera
* https://github.com/NativeScript/nativescript-camera 

### Storage

* https://docs.nativescript.org/cookbook/file-system

### Fingerprint

* https://github.com/EddyVerbruggen/nativescript-fingerprint-auth

### Sensors

* https://www.npmjs.com/package/nativescript-accelerometer
* (iOS only) https://github.com/stephenfeather/nativescript-coremotion

### Geolocation

* https://github.com/NativeScript/nativescript-geolocation

### Bluetooth

* https://www.npmjs.com/package/nativescript-bluetooth

### Microphone / Audio Recording

* https://github.com/bradmartin/nativescript-audio

### Permissions
