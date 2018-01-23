# Notebook

Notebook for various snippets and learning. These should all be moved somewhere else eventually.

## NativeScript

### Placeholder

A placeholder UI element is to be used as a "placeholder" for a native UI componenet such as a CocoaPod or some other control that is not available via NativeScript.

In your view (Angular):

```xml
<Placeholder (creatingView)="creatingView($event)"></Placeholder>
```

In your component:

```js
import { CreateViewEventData } from "ui/placeholder";

creatingView(args: CreateViewEventData) {
    args.view = new FSCalendar();
}
```

### Native Code

To be able to use native members, they must be declared in the file in which they are to be used. This allows the complier to be aware of the variables at build time and at runtime the native reference will be available.

```js
declare const CGRectMake;

var rect = CGRectMake(0, 0, 100, 100);
```

### CocoaPods

Follow [the guide](https://docs.nativescript.org/plugins/cocoapods) on creating and adding a plugin that references a CocoaPod. Confirm that the iOS platform project contains an `.xcworkspace` and `Podfile` to confirm its installation. Then, to use it, declare the members needed and use as normal. NativeScript will be aware of the CocoaPod at runtime.

```js
declare const FSCalendar;

var calendar = new FSCalendar();
```

## Angular

The `selector` option on a Component defines the name of the template if it were to be used in other views. A Component selector named `foo-bar` can be used in another component with `<foo-bar></foo-bar>`. The selector value for the initial component can be inferred and does not matter. 

```js 
@Component({
    selector: "foo-bar",
    ...
})
```
