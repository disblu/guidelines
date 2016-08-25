# Swift Walkthrough

The main purpose of this guide is to create code that is concise, readable and simple.✌🏻

- [1 Naming](#1-naming)
   - [1.1 Protocols](#11-protocols)
   - [1.2 Enumerations](#12-enumerations)
   - [1.3 Language](#13-language)
- [2 How it works](#2-how-it-works)
   - [2.1 Integrity](#21-integrity)
   - [2.2 States](#22-states)
- [3 How to use it](#3-how-to-use-it)
   - [3.1 Identify yourself](#31-identify-yourself)
   - [3.2 Text Editor](#32-text-editor)
   - [3.3 Current configuration](#33-current-configuration)
   - [3.4 Basic commands](#34-basic-commands)
       - [3.4.1 Creating a new repository](#341-creating-a-new-repository)
       - [3.4.2 Tracking files](#342-tracking-files)
       - [3.4.3 Ignoring files](#343-ignoring-files)
       - [3.4.4 Cloning a repository](#344-cloning-a-repository)
       - [3.4.5 Log](#345-log)
       - [3.4.6 Branches](#346-branches)
       - [3.4.7 Merging](#347-merging)
       - [3.4.8 Resolving merge conflicts](#348-resolving-merge-conflicts)
       - [3.4.9 Stash](#349-stash)
- [4 Conventions](#4-conventions)
    - [4.1 Branch naming](#41-branch-naming)
    - [4.2 Commits](#42-commits)
       - [4.2.1 Structure](#421-structure)
       - [4.2.2 Message](#422-message)
    - [4.3 Merging](#43-merging)
- [5 Alternatives](#5-alternatives)
- [Thanks to](#thanks-to)

# 1 Naming
Use descriptive names with camel case for classes, methods, variables, etc. Type names (classes, structures, enumerations and protocols) should be UpperCamelCase, while method names and variables should be lowerCamelCase.

Good:

```Swift
private let maximumBookCount = 100

class BookContainer {
  var bookButton: UIButton
  let bookWidthPercentage = 0.85
}
```

Bad:

```
let MAX_BOOK_COUNT = 100

class app_bookContainer {
  var bBut: UIButton
  let bWidthPct = 0.85
}
```
According to [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/#follow-case-conventions), abbreviations and initialisms that appear in all uppercase should be uniformly uppercase or lowercase.

Good:
```
let urlString: URLString
let userID: UserID
```
Bad:
```
let uRLString: UrlString
let userId: UserId
```

When specifying the type of an identifier, always put the colon immediately after the identifier, followed by a space and then the type name.

```
class Coffee: Drink { ... }

let timeToCoffee: NSTimeInterval = 2

func makeCoffee(type: CoffeeType) -> Coffee { ... }
```

Rationale: The type specifier is saying something about the identifier so it should be positioned with it.

Also, when specifying the type of a dictionary, always put the colon immediately after the key type, followed by a space and then the value type.

```
let capitals: [Country: City] = [ Spain: Madrid ]
```

## 1.1 Protocols
According to Apple's API Design Guidelines, protocols names that describe what something is should be a noun. Examples: ```Collection```, ```BookFactory```. Protocols names that describe an ability should end in -ing, -able, or -ible. Examples: ```Relatable```, ```Resizing```.


## 1.2 Enumerations

You introduce enumerations with the enum keyword and place their entire definition within a pair of braces. Cases are to be written in LowerCamelCase.

```
enum CompassPoint {
    case north
    case south
    case east
    case west
}
```
or 
```
enum CompassPoint {
    case north, south, east, west
}
```

## 1.3 Language

Everything should be in US English!

Good:
```
let red = CGColor.redColor()
```
Bad:
```
let rojo = CGColor.redColor()
```



