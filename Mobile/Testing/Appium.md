# Appium

## Installation

Follow the getting started guide:
* https://github.com/appium/appium/blob/master/docs/en/about-appium/getting-started.md
* Be sure to verify the installation via `appium-doctor`

Installing iOS drivers (from the installation guide):
* For use with the iOS simulator: https://github.com/appium/appium/blob/master/docs/en/drivers/ios-xcuitest.md
* For use with a physical iOS device: https://github.com/appium/appium/blob/master/docs/en/drivers/ios-xcuitest-real-devices.md

To resolve issues with installing and linking Node and/or Carthage on macOS High Sierra:
* `chown` the brew directories: `sudo chown -R $(whoami) $(brew --prefix)/*` (https://github.com/Homebrew/brew/issues/3228)
* Run `brew link {your_package}`. Some directories might need to be created via `sudo mkdir {your_directory}` and then `chown` the brew directories again.
