---
title: "Intro Bazel"
date: 2021-05-10T21:18:00+07:00
draft: false 
---

# Intro Bazel
*Fast, Correct*

## Xcode Build System
When we develop iOS Application, Xcode is the best choice right now. Xcode are smarter IDE but lack of build systems. The main goal of Xcode Build System is to orchestrate execution of various task that will eventually produce an executable program.
Xcode build system is like a black box. Just click *Run* or *cmd + b* Xcode will gather all your code and build the applications. 
Xcode already included *Caching* mechanism as long as users do not run the *Product* -> *Clean* feature before build the applications. If you want to gain some insight /Behing the Scene of the Xcode Build Process/ [Behind the Scenes of the Xcode Build Process - WWDC 2018 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2018/415/)
and refer this too [Building Faster in Xcode - WWDC 2018 - Videos - Apple Developer](https://developer.apple.com/videos/play/wwdc2018/408/)
Caching mechanisms are very interested idea right? we will take a look how big companies with complexity of their app tackle build times problems.

## Bazel
Refer on bazel documentations, why we should use?
Bazel is fast and reliable. 
-> Bazel caches all previously done work and tracks changes to both file content and build commands. This way, Bazel knows when something need to be rebuild, and just rebuild only the changes.

## How Bazel Work?
First, Bazel will does the following:
1. *Loads* the BUILD files relevant to the target
2. *Analyzes* the inputs and the dependencies
3. *Execute* the build actions on the inputs until the final build outputs are produced

## Action Before Start
Before we migrate the project using Bazel workflow, we must learn how Xcode build first. You can use some quick tools like *Xcodegen* to learn the structure of your project. Cocoapods 3rd party management tools in Xcode are great but we need to create framework to acceptable in Bazel workflow, you can refer *PodToBUILD*. Bazel are great but for starting project you will exhausting. Build from small first then improve later.

We will discover Build sample application using Bazel on iOS App on next article.


## References
[Bazel overview - Bazel 4.0.0](https://docs.bazel.build/versions/4.0.0/bazel-overview.html)
