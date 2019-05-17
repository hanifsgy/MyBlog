---
title: "Memory Management: Weak and Unowned"
date: 2019-05-16T18:30:49+07:00
draft: false
---

### Automatic Reference Counting

Swift uses *Automatic Reference Counting* (ARC) to track and manage your app's memory usage.  You can check [Swift docs](https://docs.swift.org/swift-book/LanguageGuide/AutomaticReferenceCounting.html) for more detail information to memory management. 

> Whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a *strong reference* to the instance. The reference is called a “strong” reference because it keeps a firm hold on that instance, and does not allow it to be deallocated for as long as that strong reference remains.
>
> Reference counting applies only to **instance** of classes. **Structures** and **enumerations** are **value** types, not reference types, and are not stored and passed by reference—  [source](https://www.avanderlee.com/swift/weak-self/).

### Simple Usage 🤘

`weak self` and `unowned self` give ARC the required information between relationships in our code. For more detail to define `weak self` and `unowned self`:

##### Weak

- Always used on *var*
- Always used on an *optionals*
- Automatically changes itself to nil when the underlying reference  go away

#### Unowned

- Always used with *non-optional* types

- Automatically *crash* if you access it and the underlying reference is gone

### Best Practices 🧠

#### Example: Weak

When to use `weak self` ? The simple answer is whenever we declared *instance* optional variable as they can automatically be set to `nil`.  This example defines two classes called `Fighter` and `Champion`, which model a block of `champion` and its `fighter`:

```swift
class Fighter {
    let name: String
    var champion: Champion?
    
    init(name: String) {
        self.name = name
    }
    
    deinit {
        print("Fighter \(name) is being deinitialized")
    }
}

class Champion {
    let year: Int
    var fighter: Fighter?
    
    init(year: Int) {
        self.year = year
    }
    
    deinit {
        print("Fighter \(fighter?.name ?? "") is being deinitialized")
    }
}

var fighter: Fighter? = Fighter(name: "Chris John")
var champion: Champion? = Champion(year: 2011)

fighter!.champion = champion
champion!.fighter = fighter

fighter = nil
champion = nil
```

Every `Fighter` instance has a `name` property of type `String` and an optional `champion` that is initially to be `nil`. The `champion` property is optional, because some `fighter` may not always have a title `champion`.  Similarly, every `Champion` instances have a `year` property of type `String` and an optional `fighter` property that is initially nil. I assume in this case  `champion` may not always have the same `fighter` 🙊. 

Linking these two instances creates a strong reference between `Fighter` and `Champion`. The `Fighter` ha a strong reference to `Champion` instance, and the `Champion` instance has a strong reference to the `Fighter`. Gotcha! You found a retain cycle 👀.

#### Solving Weak

A Simple solution to handle this strong reference is to make `Champion` type's `fighter` property is declared as a `weak` reference. Because in this case, we need just one `weak` reference to break the loop / retain cycle. A `weak` reference doesn't increment the referenced object's retain count, while still letting us get access to the object while it's still in memory. And in another case, sometimes we meet `weak self` inside the closure, but why? if `self` also retains the closure you must use the `weak` combined with `self`. 

> Always use weak combined with self inside closures to avoid retain cycle.

#### Unowned Self

Like a weak reference, `unowned` does not keep a strong hold on the instance. According to the Apple docs, when to use `unowned self`

> Use a weak reference whenever it is valid for that reference to become nil at some point during its lifetime. Conversely, use an unowned reference when you know that the reference will never be nil once it has been set during initialization.

An `unowned` reference is expected to always have a value. As a result, ARC never sets an unowned reference’s value to `nil`, which means that unowned references are defined using non-optional types. Unfortunately, if you're accessing an instance which no longer there can cause a crash. `weak` is always safer 🤗.

