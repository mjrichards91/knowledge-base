# Swift Learning

## Constant

```swift
let maximumNumberOfLoginAttempts = 10 
```

Helpful to let the reader & Swift know this value is never going to change. This holds true for arrays and dictionaries as well. This makes the actual code perform more efficiently.

## Variable

```swift
var currentLoginAttempt = 0
var welcomeMessage: String
```

The type can be inferred with an initial value and the type is not necessary.

### Multiple variable declarations: 

```swift
var x = 0.0, y = 0.0, z = 0.0
var red, green, blue: Double
```

## Strings

### Interpolation:

```swift
var friendlyWelcome = "Hello!"
print("The current value of friendlyWelcome is \(friendlyWelcome)”)
```swift

### “ToString”

```swift
String(somevar)
```

Semicolons are NOT required but are if multiple statements are on a single line:
let cat = “cat"; print(cat)

## Methods

```swift
func drawHorizontalLine(from startX: Double, to endX: Double, using color: UIColor) {
}
```

`from`: is the name of the EXTERNAL parameter (used by the callers)
`startX`: is the name of the INTERNAL parameter (used internally to the func)

```swift
func returnSomething() -> String {
}
```

returns a string value

```swift
func doSomething(_ someValue: String) -> String {
}
```

`_` is the external parameter, this removes the requirement for named parameters. Used most often as the first argument - NEVER for subsequent ones.

## Logging:

Homework: https://stackoverflow.com/questions/25951195/swift-print-vs-println-vs-nslog

## Optionals

Has 2 values: set and not set. A set optional has an associated value “on the side”. String? means an associated string value (that is optional) that could be set or not set.

An “!” unwraps the associated value. If there is not associated value, then the app will crash and burn.

Optionals do not have to unwrapped to set.

Declarations with a “!” automagically unwraps the optional value as the “?” does not. Implicitly unwrapped optional.

## UI

UILabel? is optional so that iOS has time to connect the UI to the property

## Conventions

Clarity over brevity!

## Properties

All properties must be initialized unless they are optionals. Behind the scenes, optionals are set to nil

### Computed properties:

```swift
 var displayValue: Double {
    get {
        return Double(display.text!)!
    }
    set {
        display.text = String(newValue)
    }
}
```
