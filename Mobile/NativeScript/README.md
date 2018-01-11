# NativeScript

Cross-plaform mobile framework that generates __*native*__ mobile apps (not webviews) through Javascript and CSS.

This framework is backed by [Telerik](https://www.telerik.com/) and [Progress](https://www.progress.com/).

## Which Flavor?

NativeScript can be written in a few different ways. With plain 'ol Javascript is the most lightweight option. Typescript can be used without Angular to take advantage of the language. Lastly, Angular can be used. It might be beneficial to use the Angular flavor if you intend to reuse logic from an Angular web app on the mobile app. Typescript is also a "first-class citizen" in the NativeScript world as that is what it is written in so taking advantage of it will play well into the envrionment. Plain 'ol Javascript can be preferred as the most simple way to get started without the overhead of learning Angular. 

## Contents

* [Learning](#learning)
* [Installation](#installation)
* [Debugging](#debugging)
* [Writing Cross-Platform Code](#writing-cross-platform-code)
* [Writing Native Code](#writing-native-code)
* [Modules](#modules)

## Learning

There are [introductory courses](https://courses.nativescripting.com/courses) provided by NativeScript to get your feet wet.

[Complete sample solutions](https://www.nativescript.org/app-samples-with-code) and [snacks](http://www.nativescriptsnacks.com/) are available demonstrating various abilities and approaches.

More [resources](https://www.nativescript.org/resources) are also available.

## Installation

Installation and interaction with NativeScript is done through CLI (command line). Follow the [getting started](https://docs.nativescript.org/start/quick-setup) guide. Be sure to use `tns doctor` to confirm installation.

To create a blank app, simply using `tns create MyApp` will create a blank "Hello World" app. [Templates](https://docs.nativescript.org/tooling/app-templates) are also available to start with a more complete solution.

To create a blank Angular app, use `tns create MyApp --ng`.

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

## Writing Cross-Platform Code

NativeScript apps use [CommonJS](http://eng.wealthfront.com/2015/06/16/an-introduction-to-commonjs/) syntax.

### Contents

* [Structure](#structure)
* [UI Components](#ui-components)
* [Layouts](#layouts)
* [CSS](#css)
* [Animations](#animations)
* [Images](#images)
* [Code Behind](#code-behind)
* [View Model](#view-model)

### Structure

An app is divided into multiple folders and files depending on Angular use:

* `app` - where views and logic exist. Most time spent coding will be here.
* `app/App_Resources` - platform specific resources such as configuration files, icons, splash screens, etc.
* `app/shared` - files to be shared across views. This can be named anything.
* `app/app.css` - global styling for the app
* `hooks` - preprocessor scripts
* `node_modules` - npm dependencies including cross-platform `tns-core-modules` and Angular implementation if using it
* `platforms` - platform specific code needed to build for each. Files here are generated from `tns build` and should be treated as read-only and ignored in Git.
* `package.json`

#### Javascript

* `app/views` - the views for the app with subfolders for each view. Each view contains a `.xml`, `.js`, and optional `.css`. This folder can be named anything.
* `app/app.js` - starting point for the app 

#### Angular

* `app/pages` - the pages for the app with subfolders for each view. Each view contains a `*.compoenent.ts` file, optional `.html`, and optional `.css` files. This folder can be named anything.
* `app/app.component.ts` - primary file that drives the Angular application
* `app/app.module.ts` - main configuration for application
* `app/main.ts` - the starting point for the app
* `tsconfig.json` - Typescript configuration

When using Angular, there will be both .js and .ts files which are generated and required for compilation. These can be ignored in the editor. If using Visual Studio Code, add this to your projects settings:

```js
"files.exclude": {
    "**/*.js": { "when": "$(basename).ts" },
    "**/*.map": { "when": "$(basename).map" }
}
```

### UI Components

The UI is made up of either .html (Angular) or .xml files. Regardless, the syntax is written in XML in both. Check the [documentation](https://docs.nativescript.org/ui/components) to see the available components. Each component is translated to a native component to give it that native look and feel.

Tips:

* The backtick character (`` ` ``) is a template literal and is used to wrap multiline strings without concatenation. 
* Close XML elements the long way. `<Button text="Click Me!></Button>` over `<Buttion text="Click Me!" />`. Angular and Typescript requires this.
* Check [this resource](http://www.hybridtonative.com/) for information on how to transition an existing Angular web app to mobile.

#### Angular

Within an Angular component, you can gain access to the page instance through the page module. Furthermore, that page can be modified before it is displayed using the OnInit module as well.

```js
import { OnInit } from "@angular/core";
import { Page } from 'ui/page';

// Implement OnInit
export class LoginComponent implements OnInit {
    
    // Inject the Page module
    constructor(private page: Page) {}

    // Required implementation
    ngOnInit() {
        this.page.actionBarHidden = true;
        this.page.backgroundImage = "res://some-background-image";
    }
}
```

### Layouts

See [documentation](https://docs.nativescript.org/ui/layouts), check out [some code samples](https://docs.nativescript.org/angular/code-samples/ui/layouts), and look into an [in-depth analysis](https://developer.telerik.com/featured/demystifying-nativescript-layouts/) for each layout. 

### CSS

See [documentation](https://docs.nativescript.org/ui/styling) on styling. CSS can be applied to an app globally, per page, and inline using the `style` attribute. Rule of thumb is to generally avoid inline styles and to make a conscience effort to place CSS correctly as gloablly or for a specific page.

For platform specific styling, add `@import url('~/platform.css');` as the first statment in the `app.css` file. Then, add specific style values to either the `platform.android.css` or `platform.ios.css` file.

Specific platform styling can be applied per view by defining the platform in the file name such as `myPage.ios.css` and `myPage.android.css`.

Angular `styleUrls` is a list of urls to stylesheets to be used by the component. Be sure to include your stylesheets if you are using Angular.

### Animations

Animations such as opacity, background color, translations, scaling, and rotating can all be controlled on the native platform from NativeScript. See [documentation](https://docs.nativescript.org/ui/animation) for more information.

### Images

Images can be referenced with a URL from a website, relative to the `app/images` folder (`~/images/logo.png`), or use platform specific resources (`res://logo_login`). Platform specific is the preferred way to reference images to deal with varying resolutions. Those images are to be put in the `app/App_Resources` folder in the appropriate spots.

A helpful tool to create images for varying resolutions is the [NativeScript Image Builder](http://nsimage.brosteins.com/).

### Events

See [documentation](https://docs.nativescript.org/core-concepts/events) on events. Each component has various events so be sure to check it's documentation as well.

### Binding

_(this only applies to an Angular app)_

Check the [documentation](https://docs.nativescript.org/angular/core-concepts/angular-data-binding) for an in-depth overview of binding with Angular.

#### One-Way Binding

To bind an attribute to a property, use the `[]` syntax:

```js
// text is bound to a property named email
<TextField [text]="email"></TextField>
```

To bind an event to a method, use the `()` syntax:

```js
// the tap event is bound to the method doSomething()
<Button (tap)="doSomething()"></Button>
```

#### Two-Way Binding

To use two way binding, use the `[(ngModel)]` attribute on your UI component.

### Angular Modules

_(this only applies to an Angular app)_

Modules provides the ability to share code between web and native as well as increases testability and maintainability.

### Angular Services

_(this only applies to an Angular app)_

Injectable is a requirement for all services. This allows the service to be injected into constructors. See documentation on [Angular's Dependency Injection](https://angular.io/guide/dependency-injection).

```js
import { Injectable } from "@angular/core";

@Injectable()
export class ModelService {
}

// In a construtor somewhere else...
constructor(private modelService: ModelService) {
}
```

To use a service, add it to your apps compoent providers:

```js
import { ModelService } from "./shared/model/model.service";

@Component({
  providers: [ModelService],
  ...
})
```

More on dependency injection:

* The Angular `Http` service can be injected into services the same as any others. This is the standard way of performing http calls in Angular. Furthermore, using that `Http` service to make a post call will create an [RxObservable](http://reactivex.io/documentation/observable.html) that needs to be subscribed to.


TODO: Move these somewhere else

* Arrow functions give the intended context to `this`.

```js
someExteralVariable = 'sup';

this.someService.someObservableFunction()
    .subscribe(
    () => {
        // this is the context of the wrapping class, not the function
        this.someExternalVariable = 'dude';
    }
```
* Spread operator `...` is ES2016 syntax

```js
let x = [2,3];
let y = [1, ...x];

// y is [1,2,3]
```

### Routing

Routing is required when navigating between pages. There are differences in routing from a web app in that Android has a back button and iOS has a swipe back gesture to consider. See Angular's [documentation](https://angular.io/guide/router) for an overview of the web routing concepts.

Using the `<page-router-outlet>` as the apps component sets up the app to use routing. This outlet extends the web version `<router-outlet>` to work with mobile concepts.

Simply import the router, inject, and navigate:

```js
import { Router } from "@angular/router";

constructor(private router: Router) {
}

someMethod() {
    this.router.navigate(['somePage']);
}
```

### Code Behind

_(this only applies to a non-Angular app)_

Named identically as the view. 

Navigation can be performed here using the [frame](#frame) module.

Adding an id to a view element allows access to it in the code behind through the page's `page.getViewById('your_id')` method.

### View Model

_(this only applies to a non-Angular app)_

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

## Writing Native Code

You are able to write native code specific to each platform without ever leaving Javascript.

Conditional `if` checks can be made once a page is loaded. This is only recommended for a small number of platform specific changes:

```js
exports.loaded = function (args) {
    page = args.object;

    if (page.ios) {
        ...
    }
};
```

More in-depth and frequent changes to a specific platform might merit a platform specific code behind file. For instance, if your view's code behind is `login.js`, you would create a `login.ios.js` and a `login.android.js` to handle the plaform specific logic.

From there, native objects (such as the iOS `ViewController` class) can be accessed using the frame module. Then, all native methods can be called on that instance similar to how you would natively:

```js
var navigationBar = frameModule.topmost().ios.controller.navigationBar;
navigationBar.barStyle = UIBarStyle.UIBarStyleBlack;
```

This process is known as "mashalling". There is documentation on how marshalling works for both [iOS](https://docs.nativescript.org/runtimes/ios/marshalling/marshalling-overview) and [Android](https://docs.nativescript.org/runtimes/android/marshalling/overview).

Views can be customized for each platform within xml using plaform specific attributes. The prefixes `ios:` and `android:` are available for all attributes on all views. For example:

```xml
<Button ios:text="foo" android:text="bar" />
```

For more information on how this native coding works, see [this blog post](https://developer.telerik.com/featured/nativescript-works/).

## Modules

Modules are included out of the box with NativeScript and others can be found through NPM.

Sources for modules and plugins:

* https://market.nativescript.org/
* https://plugins.nativescript.rocks/
* https://www.npmjs.com/ 

Tips:

* By using `--save` when installing packages, the package gets recorded in the `package.json` dependencies. This is helpful for other developers who will be working on your project and run `npm install`. 
* Not all npm modules will work with NativeScript, especially if they rely on Node.js or browser functionality. Here's a quick reference to some of the [most popular supported modules](https://github.com/NativeScript/NativeScript/wiki/supported-npm-modules).
* NativeScript plugins differ from npm modules in how they are installed. Use `tns plugin add <your-plugin-here>` to add them to your project. This command works the same as `npm install --save`, but also configures any native code required to get it to work.

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

### Validation

The [email-validator](https://www.npmjs.com/package/email-validator) module is a quick and easy way to validate email addresses.

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
