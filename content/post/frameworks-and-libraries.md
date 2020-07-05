---
title: "Frameworks and Libraries"
date: 2020-07-05T12:33:23+07:00
draft: true
---

# Frameworks and Libraries
## Frameworks
A framework is a hierarchical directory that encapsulates shared resources, such as a dynamic shared library, nib files, image files, localized strings, header files, and reference documentation in a single package. Multiple applications can use all of these resources simultaneously. The system loads them into memory as needed and shares the one copy of the resource among all applications whenever possible —Apple.

Splitting code into smaller frameworks have some advantages in iOS development. Frameworks can keep larger and complex code into smaller and make it maintainable. 
In the development of iOS framework can be divided into /dynamic libraries/ and /static libraries/.  When you build Xcode project, it will compile code into an object files. Based on [WWDC18](https://developer.apple.com/videos/play/wwdc2018/415/)  Xcode have to complete and link source code, copy and process resource like headers, asset catalogues and event interface builder (like storyboard, xib files). And finally Xcode will do code sign and even do some /linting/ process and validation. 
Object files (*.o) contains the executable machine code and other information used by the linker — /The process of merging external libraries with app’s source code files is known as linking/. Linker will gather all of object files and create an executable binary. Here we come two optional linking process which is dynamic and static. 

## Static Libraries (.a)
Static libraries are collection of object files and ending with `.a`  created by an archiver tool. It can be extractable using some archiver tool. 
/Statically/ linked means the files will be included into app binary. It will make app binary larger than usually. Launch time will be slower because of bloated app executable.
Every files `.swift` will be map as object files which is `.o`  then compile as a static `.a` files which is hardly coupled in app project. 

## Dynamic Libraries (.dylib)
Dynamic libraries, rather than being copied into app binary dynamic means the libraries will be linked when the app needed. It will be loaded into memory and can be happen either at load time or at runtime. Dynamic make binary app size smaller, since it is shared. The cons are slower call library because it is located outside application executable. 

## Real World
In terms real word iOS application development, choosing static and dynamic we first must understand business purposes. We need to know why we need to create framework, does it will be linked as dynamic or static? After we defined our structure MainApp it will make easier that smaller piece of code linked as static or dynamic. 
Third-party dependencies sometimes not supported yet to be statically linked, If we choose CocoaPod as dependency management we should take care of it. `use_frameworks!` default in DSL CocoaPod will be linkage dependencies into dynamic ones, but we can defined linkage dependencies into static using `:linkage => :static`.  If you want to fully control over project structure and setup I think Carthage should be good. I will write some of tour real world application using custom frameworks on next post~ cheers :D