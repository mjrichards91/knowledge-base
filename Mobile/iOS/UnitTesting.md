# Unit Testing

Unit testing in a Swift application via [Quick](https://cocoapods.org/pods/Quick) and [Nimble](https://cocoapods.org/pods/Nimble).

## Install CocoaPods

First make sure CocoaPods is installed via Terminal:

```
pod --version
```

If not, install the gem:

```
sudo gem install cocoapods
```

## Create Podfile

Create the Podfile in your project and paste the following:

```ruby
# Uncomment the next line to define a global platform for your project
# platform :ios, ‘9.0’

target ‘name-of-your-project’ do
  # Comment the next line if you’re not using Swift and don’t want to use dynamic frameworks
  use_frameworks!

 target ‘name-of-your-projects-tests-folder’ do
    inherit! :search_paths
    # Pods for testing
    pod ‘Quick’
    pod ‘Nimble’
  end

end
```

## Install Pods

Simply install the Pods from the Terminal:

```
pod install
```

## Start writing tests!

Close Xcode and reopen the project using the newly generated `name-of-your-project.xcworkspace` file.

Update your test file to use Quick and Nimble:

```swift
// Add imports
import Quick
import Nimble

@testable import myProject

// Inherit from QuickSpec
class myProjectTests: QuickSpec {
    
    override func spec() {
        // Write your tests!
    }
}

```
