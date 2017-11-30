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

Create the Podfile and paste the following:

```ruby
# Uncomment the next line to define a global platform for your project
# platform :ios, ‘9.0’

target ‘fizzbuzz’ do
  # Comment the next line if you’re not using Swift and don’t want to use dynamic frameworks
  use_frameworks!

 # Pods for fizzbuzz

 target ‘fizzbuzzTests’ do
    inherit! :search_paths
    # Pods for testing
    pod ‘Quick’
    pod ‘Nimble’
  end

end
```
