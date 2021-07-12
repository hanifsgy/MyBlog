---
title: "Uncover UIResponder"
date: 2021-07-12T22:13:55+07:00
draft: false
---
<h1 style="text-align: center"> Uncover UIResponder </h1>
<div style="text-align: center"><small>July - 2021</small></div>

## ![Screen Shot 2021-07-12 at 22.00.11](/Users/m.hanif.sugiyanto/Desktop/Screen Shot 2021-07-12 at 22.00.11.png)

Based on the Figure 1 we can define who is the responder

1. If the `view` is the root view of view controller, the next responder is the view controller
2. If the view is not the root view of a view controller, the next responder is the view's superview
3. If the view controller's view is the root of a `window` the next responder is the `window` object
4. If the view controller was presented by another view controller, the next responder is the presenting view controller
5. `UIWindow` is the window's nex respinder is the application object
6. `UIApplication` the app object's next responder is the application object. Only if the app delegate is an instance of `UIResponder` and is not a view, view controller, or the app object itself. Confusing?

## Responder Chain

- Apps receive and handle events using *responder objects*. 
- A responder object is any instance of `UIResponder` class and common subclasses like `UIView, UIViewController` and `UIApplication`.
- Responders reveive the raw event data and must either handle the event or forward it to another responder object.
- Who is *first responder* ?
  - Unhandled events are passed from responder to responder in the active *responder chain* which is the dynamic configuration of your app's responder objects.
  - UIKit designates a *first responder* and sends the event to that object firs. The first responder varies based on the type of event.
- `UIKit` uses view-based hit testing to determine where touch event occur. `UIKit` will compare the touch location to the bounds of view object in the view hierarchy. `hitTest:withEvent:` method of `UIView` walks the view hierarchy, looking for rhe deepest subview that contains the specified touch. That view becomes **the first responder** for the touch event.
- `clipsToBounds` property indicate specific area, when property set to `false`, subviews outside of that view's bounds are not returned even if they happen to contain the touch.



Key:

`UIResponder` An abstract interface for responding to and handling events

`UIEvent` An object that describes a single user interaction with your app



### References

https://developer.apple.com/documentation/uikit/touches_presses_and_gestures/using_responders_and_the_responder_chain_to_handle_events

https://medium.com/macoclock/responder-chain-you-should-understand-in-ios-54e96b0c4bb1
