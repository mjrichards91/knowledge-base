# React Native

## Installation

Follow the [getting started guide](http://facebook.github.io/react-native/docs/getting-started.html) provided by React Native.

`npm 5` is currently not suppported to create and run a project ([source](https://github.com/facebook/react-native/issues/14767)). Use `yarn` instead.

```bash
$ brew install yarn
$
$ create-react-native-app AwesomeProject
$
$ yarn start
```

Make sure `watchman` is installed as well to correctly start the project server 

```bash
$ brew install watchman
```

## Basics

* Uses JSX syntax for embedding XML within Javascript

## Components

* Comprised of Components with only a `render` function as a requirement

## Props

* Props are generally Javascript variables that can be bound in the JSX syntax
* Components can be built to be reused in a view - Greeting component that prints “Hello {name}” and the render component containing many `<Greeting name=“Mike”/>`
* Props are static

## State

* State are variables that are dynamic throughout the app’s lifecycle
* The initial state should be set in the constructor `this.state = { isShowingText = true };`
* Changes to the state should be made in the `setState` function 
  ```js 
  this.setState(previousState => {
       return { isShowingText: !previousState.isShowingText };
  });
  ```
* A state container like Redux can also be used to manage state. Changes would be applied to Redux rather than the `setState` function in this case.
* React Native state is handled the exact same in React so understanding the web version will apply the same to mobile.

## Style

* Styling is set through javascript values that are similar to CSS
* A more comprehensive set of styles can be created through the `StyleSheet` object
  ```js
  const styles = StyleSheet.create({
    bigblue: {
      color: 'blue',
      fontWeight: 'bold',
      fontSize: 30,
    },
    red: {
      color: 'red',
    },
  });
  ```
## Layout
  
### Height & Width

* Sizes of components can be explicitly set to a specific size (10, 100, etc.) or use a `flex` size that takes up a proportional amount of the available space. 

### Flexbox

* `Flexbox` is used to control the direction and alignment of its items. This value is set on a components `style`.
  ```js
  <View style={{
    flex: 1,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
  }}>
  ```
## Text Input

* `TextInput` controls contain the typical placeholder and text changed event. The changed event can be tied into changing the state.
  ```js
  <TextInput
    style={{height: 40}}
    placeholder="Type here to translate!"
    onChangeText={(text) => this.setState({text})}
  />
  ```

## Plugins

Note: These plugins are are found by simply searching, I have no experience using any of them.

### Notifications

There is only a module for Notifications on iOS.

* https://github.com/zo0r/react-native-push-notification 

### Offline Capabilities

* SQLite - https://github.com/andpor/react-native-sqlite-storage 
* Network Status - https://facebook.github.io/react-native/docs/netinfo.html

### Camera / Media

There are no modules that support using the camera. There are ones to get photos from the camera roll, however.

* Camera Roll - https://facebook.github.io/react-native/docs/cameraroll.html#docsNav 
* https://github.com/react-native-community/react-native-camera

### Storage

[AsyncStorage](https://facebook.github.io/react-native/docs/asyncstorage.html#docsNav) is an option here.

* https://github.com/itinance/react-native-fs

### Fingerprint

* https://github.com/hieuvp/react-native-fingerprint-scanner

### Sensors

* https://github.com/kprimice/react-native-sensor-manager

### Geolocation

* https://facebook.github.io/react-native/docs/geolocation.html#docsNav
* https://github.com/transistorsoft/react-native-background-geolocation

### Bluetooth

* BLE - https://github.com/Polidea/react-native-ble-plx
* Bluetooth Classic - https://github.com/rusel1989/react-native-bluetooth-serial 

### Microphone / Audio Recording

* https://github.com/jsierles/react-native-audio

### Permissions

* https://github.com/yonahforst/react-native-permissions







