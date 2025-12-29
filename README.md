# SwiftJS

[![Github Actions](https://github.com/SusanDoggie/SwiftJS/workflows/Builder/badge.svg)](https://github.com/SusanDoggie/SwiftJS/actions)
[![codecov](https://codecov.io/gh/SusanDoggie/SwiftJS/branch/main/graph/badge.svg)](https://codecov.io/gh/SusanDoggie/SwiftJS)
![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20iOS%20%7C%20Linux-lightgrey.svg?style=flat)
[![GitHub release](https://img.shields.io/github/release/SusanDoggie/SwiftJS.svg)](https://github.com/SusanDoggie/SwiftJS/releases)
[![Swift](https://img.shields.io/badge/swift-5.3-orange.svg?style=flat)](https://swift.org)
[![MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

A cross platform JavaScript engine for Swift.

## Installation

Add SwiftJS to your `Package.swift`:

```swift
dependencies: [
    .package(url: "https://github.com/egernet/SwiftJS.git", from: "1.3.0")
]
```

## Usage

### Basic JavaScript Evaluation

```swift
import SwiftJS

let context = JSContext()
let result = context.evaluateScript("1 + 2")
print(result.doubleValue!) // 3.0
```

### Working with JavaScript Objects

```swift
let context = JSContext()

// Create and manipulate objects
let array = context.evaluateScript("[1, 2, 3]")
print(array[0].doubleValue!) // 1.0
print(array.count) // 3

// Access properties
let obj = context.evaluateScript("({name: 'John', age: 30})")
print(obj["name"].stringValue!) // "John"
```

### Swift Functions in JavaScript

```swift
let context = JSContext()

let multiply = JSObject(newFunctionIn: context) { context, this, args in
    let a = args[0].doubleValue!
    let b = args[1].doubleValue!
    return JSObject(double: a * b, in: context)
}

context.global["multiply"] = multiply
let result = context.evaluateScript("multiply(6, 7)")
print(result.doubleValue!) // 42.0
```

### JSON Interoperability

```swift
let context = JSContext()

// Swift dictionary to JavaScript object
let data: [String: Any] = ["name": "Alice", "scores": [10, 20, 30]]
context.global["data"] = JSObject(jsonObject: data, in: context)

// JavaScript object to Swift
let jsObj = context.evaluateScript("({x: 1, y: 2})")
let dict = jsObj.toJsonObject() as? [String: Any]
```

## System Requirements

For Linux platforms, you need to install JavaScriptCore

### Ubuntu

    apt-get -y install libjavascriptcoregtk-4.0-dev

### CentOS 8

    yum -y install webkit2gtk3-jsc-devel

### Amazon Linux 2

    yum -y install webkitgtk4-jsc-devel

## Contributing

To contribute a feature, please [create an issue](https://github.com/SusanDoggie/SwiftJS/issues/new) or [make a pull request](https://github.com/SusanDoggie/SwiftJS/compare).
