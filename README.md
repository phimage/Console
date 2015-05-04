# Phiole - Φole
[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat
            )](http://mit-license.org)
[![Platform](http://img.shields.io/badge/platform-iOS/MacOS-lightgrey.svg?style=flat
             )](https://developer.apple.com/resources/)
[![Language](http://img.shields.io/badge/language-swift-orange.svg?style=flat
             )](https://developer.apple.com/swift)
[![Issues](https://img.shields.io/github/issues/phimage/Prephirences.svg?style=flat
           )](https://github.com/phimage/Phiole/issues)

[<img align="left" src="/logo-128x128.png" hspace="20">](#logo)

Simple object to wrap three [NSFileHandle](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSFileHandle_Class/index.html): 'output', 'error' to write and 'input' to read

There is of course a default instance for [standard streams](http://en.wikipedia.org/wiki/Standard_streams)
```swift
let csl = Phiole.std
```

This object could be used in script or CLI application instead of using `println()`.
This adds the following abilities : 
* Write to a file by declaring transparently an [NSFileHandle](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/Foundation/Classes/NSFileHandle_Class/index.html) as output stream
* Write to error stream
* Read from input stream

[Swift scripts: How to write small command line scripts in Swift](http://practicalswift.com/2014/06/07/swift-scripts-how-to-write-small-command-line-scripts-in-swift/)

:warning: Phiole is not a login system. Use instead project like [CocoaLumberjack](https://github.com/CocoaLumberjack/CocoaLumberjack)

# Usage
## Write to ouput stream
```swift
csl.println("write string and pass to the new line")
csl.print("write string without new line")
csl.println() // write new line
```
## Write to error stream
```swift
csl.errorln("write an error")
```
## Read from user input
```swift
if line = csl.readLine() {
  // do something
}
```
## Writing to a file
Create the file handle for writing (file must exist)
```swift
if let fileHandle = NSFileHandle(forWritingAtPath: "myoutput.file") { ..
```
Initialize the console object
```swift
var newCsl = csl.withOutput(fileHandle)
// or with more code
var newCsl = Phiole(input: input: Phiols.std.input, output: fileHandle, error: Phiols.std.error)
```
Write as usual
```swift
newCsl.println("write to a file")
```
Finally don't forget to close the file handle
```swift
fileHandle.closeFile()
```

## Add some colors in terminal or xcode
You can manually add color with decorated method
```
csl.println(Phiole.Color.green.fg("write in red"))
```
Or for all ouputs
```
csl.outputColor = .Green
csl.errorColor = .Red
... write here ...

// reset
csl.outputColor = .None
```

### For Xcode
**XcodeColors** is a simple plugin for Xcode, it allows you to use colors in the Xcode debugging console.

Full installation instructions can be found on the XcodeColors project page:  
https://github.com/robbiehanson/XcodeColors

Then you must add environment variable `XcodeColors` = `YES` in your Scheme

## More examples
In [main.swift](/Phiole/main.swift) or [Natalie (generate code from storyboard and ouput to standard stream or specified file)](https://github.com/phimage/Natalie/blob/console/natalie.swift)

# Setup #

## Copy/Paste ##
Just copy/paste code with licence in your script, or import swift file in your CLI project

## Using [cocoapods](http://cocoapods.org/) ##

Add `pod 'Phiole', :git => 'https://github.com/phimage/Phiole.git'` to your `Podfile` and run `pod install`. 

Add `use_frameworks!` to the end of the `Podfile`.

##  Licence
```
The MIT License (MIT)

Copyright (c) 2015 Eric Marchand (phimage)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

# Logo #
By [kodlian] (http://www.kodlian.com/), inspired by [apple swift logo](http://en.wikipedia.org/wiki/File:Apple_Swift_Logo.png)
### Why a logo?
I like to see an image for each of my projects when I browse them with [SourceTree](http://www.sourcetreeapp.com/)
