# Jekyll Apple Help

Jekyll-Apple-Help is a [Jekyll] template and [Xcode] build system that makes it easy to author and build [Mac OS X Help Books](https://developer.apple.com/library/mac/documentation/Carbon/Conceptual/ProvidingUserAssitAppleHelp/user_help_intro/user_assistance_intro.html). Add Help to your Mac app, and start authoring in Markdown within minutes. The resulting Help has the same look & feel as Apple's Yosemite apps.

![Jekyll Apple Help Screenshot](jekyll-apple-help.png)

### Background

When recently helping develop [Xynk], I wanted to make some how-to documentation available through Apple's help system. Should be some simple HTML, right? Well, as [Apple Help veterans](http://alastairs-place.net/blog/2015/01/14/apple-help-in-2015/) know, the help developer documentation is byzantine and the tools are idiosyncratic. How to simplify help for the indie developer?

Fundimentally, Mac OS X's Apple Help Books are static web sites and Jekyll is an excellent static site generator, so the two fit naturally. In particular, Jekyll's recently added Collections feature is perfect for wrangling help topics. Add some layouts, plugins, and build-glue and you get Jekyll-Apple-Help.

## Features



## Requirements

- [Xcode]
- [Jekyll] - both standard install and [RVM](https://rvm.io) supported

Optional: [fswatch](http://brewformulas.org/Fswatch) for auto-refresh via jekyll-server.command

## Setup

The JekyllHelp template is designed for easy installation into a typical Xcode project. By default, the template's Info.plist expects the project and app to have the same name (e.g. MyApp.xcodeproj builds MyApp.app).

In the following, substitute your app/company for "MyApp"/"com.mycompany".

### Create MyAppHelp Bundle Target

0. Select _File > New > Target..._
0. Select Bundle template from _OS X > Frameworks & Libraries_
0. Enter the settings:
    - Product Name: MyAppHelp
    - Bundle Extension: help
0. Replace Xcode-generate MyAppHelp folder with JekyllHelp (renamed to MyAppHelp)
0. Update Bundles identifier to `com.mycompany.*`
0. Add a Run-Script Build-Phase with the script:
	`/usr/bin/make -C $(dirname "$PRODUCT_SETTINGS_PATH")`

Now the MyAppHelp target should build, creating the product `MyAppHelp.help`

### Integrate Help into MyApp Target

0. Add target MyAppHelp to MyApp's target dependencies (_Build Phases > Target Dependencies_)
0. Add product MyAppHelp.help to app target (via File Inspector)
0. Add to MyApp target Info properties:
	- Help Book Identifier: `com.mycompany.$(PROJECT_NAME:rfc1034identifier).help`
	- Help Book directory name: `$(PROJECT_NAME)Help.help`



## Authoring

## Apps that use Jekyll-Apple-Help

[Xynk]

[Jekyll]: http://jekyllrb.com
[Xcode]: https://developer.apple.com/xcode/
[Xynk]: http://xynkapp.com/
