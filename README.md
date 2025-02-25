# ConsolePerseusLogger — Xcode 14.2+

> Light-weight logger in Swift. Hereinafter `CPL` stands for `Console Perseus Logger`.<br/>

[![Actions Status](https://github.com/perseusrealdeal/ConsolePerseusLogger/actions/workflows/main.yml/badge.svg)](https://github.com/perseusrealdeal/ConsolePerseusLogger/actions/workflows/main.yml)
[![Style](https://github.com/perseusrealdeal/ConsolePerseusLogger/actions/workflows/swiftlint.yml/badge.svg)](https://github.com/perseusrealdeal/ConsolePerseusLogger/actions/workflows/swiftlint.yml)
[![Version](https://img.shields.io/badge/Version-1.0.3-green.svg)](/CHANGELOG.md)
[![Platforms](https://img.shields.io/badge/Platforms-macOS%2010.13+_|_iOS%2011.0+-orange.svg)](https://en.wikipedia.org/wiki/List_of_Apple_products)
[![Xcode 14.2](https://img.shields.io/badge/Xcode-14.2+-red.svg)](https://en.wikipedia.org/wiki/Xcode)
[![Swift 5.7](https://img.shields.io/badge/Swift-5.7-red.svg)](https://www.swift.org)
[![License](http://img.shields.io/:License-MIT-blue.svg)](/LICENSE)

## Integration Capabilities

[![Standalone](https://img.shields.io/badge/Standalone%20-available-informational.svg)](/PerseusLoggerStar.swift)
[![Swift Package Manager compatible](https://img.shields.io/badge/Swift%20Package%20Manager-compatible-4BC51D.svg)](/Package.swift)

## Approbation Matrix

> [A3 Environment](https://docs.google.com/document/d/1K2jOeIknKRRpTEEIPKhxO2H_1eBTof5uTXxyOm5g6nQ/edit?usp=sharing) / [Approbation Results](/APPROBATION.md) / [CHANGELOG](/CHANGELOG.md) for details.

## In brief > Idea to use, the Why

> USE LOGGER LIKE A VARIABLE ANYWHERE YOU WANT.<br/>

![Screenshot 2024-10-13 at 14 00 48](https://github.com/user-attachments/assets/98b8eb7d-06cc-4c3a-ab7a-4997a844bc74)

```ruby

import ConsolePerseusLogger

log.message("[\(type(of: self))].\(#function)")

```

| Level | Message Type | Purpose                               |
| :---: | :----------- | :------------------------------------ |
| 5     | DEBUG        | Debugging only                        |
| 4     | INFO         | Helpful, but not essential            |
| 3     | NOTICE       | Might result in a failure             |
| 2     | ERROR        | Errors seen during the code execution |
| 1     | FAULT        | Faults and bugs in the code           |

# Manual
## Setting the Logger for Work

> Options used by default are different and depend on DEBUG/RELEASE.

| Options     | Default in DEBUG | Default in RELEASE | Description                                            |
| :---------- | :--------------: | :----------------: | :----------------------------------------------------- |
| tuned       | .on              | .off               | If .off no matter what level no message will be passed |
| output      | .xcodedebug      | .consoleapp        | Message output target                                  |
| level       | .debug           | .notice            | No any messages on any level above                     |
| short       | true             | true               | FALSE: Message goes with file name and line number     |
| marks       | true             | true               | FALSE: Message text, TRUE: [LOG] [DEBUG] Message text  |
| logObject   | nil              | nil                | Mac Console Subsystem and Category values group        |
| debugIsInfo | true             | true               | Only if Simulator. TRUE: DEBUG is INFO with DEBUG text |

> NOTE: If logObject is nil CPL uses default values for Subsystem "Perseus" and Category "Logger" accordingly.

```ruby

//
//  main.swift
//

import ConsolePerseusLogger

// MARK: - Log to Mac Console

log.logObject = ("MyApp", "MyLogger") // Subsystem and Category.

log.output = .consoleapp
log.turned = .on

log.level = .debug
log.message("The app's start point...", .info)

```

### Getting access to the Logger of Submodule

> In case if CPL used as a standalone file in submodule (package).

```ruby

//
//  main.swift
//

import ConsolePerseusLogger

import class SubmoduleA.PerseusLogger
import class SubmoduleB.PerseusLogger

typealias sublogA = SubmoduleA.PerseusLogger
typealias sublogB = SubmoduleB.PerseusLogger

// MARK: - Subloggers

sublogA.turned = .off
sublogB.turned = .off

// MARK: - Logger

log.level = .debug
log.message("The app's start point...", .info)

```

### Console on Mac and Simulator

> Just a matter of fact that Console on Mac doesn't show any DEBUG message from any app running on Simulator ("Include Debug Messages" tapped).<br/>

> Console Perseus Logger running on Simulator doesn't pass DEBUG message, instead it passes INFO message with text of DEBUG message, so, a passed message being INFO looks like a DEBUG and it works perfactly well.<br/>

> If for some reasons Simulator must pass DEBUG like a DEBUG message there is an option exists (it's true by default if Simulator):

```ruby

#if targetEnvironment(simulator)
    log.debugIsInfo = false // Use Case: Mac Console in use to redirect logs to file on disk.
#endif

```

## Build system requirements

- [macOS Monterey 12.7.6+](https://apps.apple.com/by/app/macos-monterey/id1576738294) / [Xcode 14.2+](https://developer.apple.com/services-account/download?path=/Developer_Tools/Xcode_14.2/Xcode_14.2.xip)

# Third-party software

- Style [SwiftLint](https://github.com/realm/SwiftLint) / [Shell Script](/SucceedsPostAction.sh)
- Action [mxcl/xcodebuild@v3.3](https://github.com/mxcl/xcodebuild/releases/tag/v3.3.0)
- Action [cirruslabs/swiftlint-action@v1](https://github.com/cirruslabs/swiftlint-action/releases/tag/v1.0.0)

# Points taken into account

- Preconfigured Swift Package manifest [Package.swift](/Package.swift)
- Preconfigured SwiftLint config [.swiftlint.yml](/.swiftlint.yml)
- Preconfigured SwiftLint CI [swiftlint.yml](/.github/workflows/swiftlint.yml)
- Preconfigured GitHub config [.gitignore](/.gitignore)
- Preconfigured GitHub CI [main.yml](/.github/workflows/main.yml)

# License MIT

Copyright © 7531 - 7533 Mikhail A. Zhigulin of Novosibirsk<br/>
Copyright © 7531 - 7533 PerseusRealDeal

- The year starts from the creation of the world according to a Slavic calendar.
- September, the 1st of Slavic year. It means that "Sep 01, 2024" is the beginning of 7533.

[LICENSE](/LICENSE) for details.

## Credits

<table>
<tr>
    <td>Balance and Control</td>
    <td>kept by</td>
    <td>Mikhail A. Zhigulin</td>
</tr>
<tr>
    <td>Source Code</td>
    <td>written by</td>
    <td>Mikhail A. Zhigulin</td>
</tr>
<tr>
    <td>Documentation</td>
    <td>prepared by</td>
    <td>Mikhail A. Zhigulin</td>
</tr>
<tr>
    <td>Product Approbation</td>
    <td>tested by</td>
    <td>Mikhail A. Zhigulin</td>
</tr>
</table>

- Language support: [Reverso](https://www.reverso.net/)
- Git client: [SmartGit](https://syntevo.com/)

# Author

> Mikhail A. Zhigulin of Novosibirsk.
