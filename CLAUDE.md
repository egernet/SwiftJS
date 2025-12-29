# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SwiftJS is a cross-platform JavaScript engine for Swift that provides Swift bindings to JavaScriptCore. It supports macOS, iOS, tvOS, watchOS, and Linux platforms using Swift 5.3+.

## Build Commands

```bash
# Build the project
swift build

# Run all tests
swift test
```

## Linux System Requirements

JavaScriptCore must be installed on Linux:
- Ubuntu: `apt-get -y install libjavascriptcoregtk-4.0-dev`
- CentOS 8: `yum -y install webkit2gtk3-jsc-devel`
- Amazon Linux 2: `yum -y install webkitgtk4-jsc-devel`

## Architecture

### Platform-Conditional Compilation

The package uses conditional compilation for cross-platform support:
- **Apple platforms**: Uses native `JavaScriptCore` framework directly
- **Linux**: Uses `CJSCore` target which provides C header mappings to GTK's JavaScriptCore

This is configured in `Package.swift` with `#if os(Linux)` directives.

### Core Components

- **JSVirtualMachine** - Manages JavaScript execution context groups and garbage collection
- **JSContext** - Main entry point for JavaScript execution; evaluates scripts and manages the global object
- **JSObject** - Core wrapper for JavaScript values with subscript access, type coercion, and property management
- **JSFunction** - Creates Swift callbacks and constructors callable from JavaScript
- **JSArrayBuffer** - JavaScript typed array support
- **JSPropertyDescriptor** - Configures property attributes (writable, enumerable, configurable)

### Dependencies

- **Doggie** (6.4.0+) - Provides `DoggieCore` utility functions
