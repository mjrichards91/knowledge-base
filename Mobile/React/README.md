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

## Plugins

Note: These plugins are are found by simply searching, I have no experience using any of them.

### Notifications

There is only a module for Notifications on iOS.

* https://github.com/zo0r/react-native-push-notification 

### Offline Capabilities

* SQLite - https://github.com/andpor/react-native-sqlite-storage 

### Camera / Media

There are no modules that support using the camera. There are ones to get photos from the camera roll, however.

* https://github.com/react-native-community/react-native-camera

### Storage

[AsyncStorage](https://facebook.github.io/react-native/docs/asyncstorage.html#docsNav) is an option here.

* https://github.com/itinance/react-native-fs

### Fingerprint

### Sensors

### Geolocation

### Bluetooth

### Microphone / Audio Recording

### Permissions







