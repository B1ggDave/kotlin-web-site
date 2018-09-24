---
type: tutorial
layout: tutorial
title:  "Multiplatform Project: iOS and Android"
description: "Sharing code between iOS and Android"
authors: Eugene Petrenko
date: 2018-10-04
showAuthorInfo: false
issue: EVAN-6029
---

In this tutorial we will create iOS and Android multiplatform application, 
that uses Kotlin/JVM for Android and Kotlin/Native for the iOS. We will share
common code between our two applications.

In this tutorial you will:
 - Create a multiplatform Gradle project 
   - Add Gradle sub-project for Android
   - Add XCode project for iOS
   - Configure IDEs to work with those projects
 - Create common code to share between platforms
 
 


# Setting up Local Environment

We will be using [IntelliJ Community Edition](https://jetbrains.com/idea) for the example. The same should work
in IntelliJ Ultimate too. You need to make sure you have the latest version of 
Kotlin plugin installed, 1.3.x or newer.
More information you may in the settings dialog under *Language & Frameworks | Kotlin Updates*.

For the iOS and macOS targets you also need to have XCode and XCode commandline tools installed and configured.
You may download and install XCode from the [Apple Developer Site](https://developer.apple.com/xcode/).

For Android is it required to have JDK 1.8 (not newer) installed. You may download and install it
from [Oracle](https://java.sun.com). 
For Android application we need to install Android SDK is required to build Android applications. For that,
you may refer to the [Google Android Studio](https://developer.android.com/studio/) site. There you may either
download and install Android Studio, which will help you to install the SDK, or use the *Download Options*
to download commandline tools.


You may need to install [cocoapods](https://cocoapods.org/).

You need the following tools on your macOS machine for development. You need to have macOS
machine to compile for iOS or macOS platform. It will still be possible to author code from
every OS.

 

# Creating Android Project

Let's use Android Studio to create our Android project. You should have the latest version of it and you
should have the latest Kotlin plugin installed as well
(check *Configure | Preferences | Language & Frameworks | Kotlin Updates* for that).

We select the *Start New Android Project* item. If you are using IntelliJ IDEA, you need to select *Android* in 
the list in the left. Android Studio will help to make sure Android SDK is installed.   

![New Project]({{ url_for('tutorial_img', filename='native/mpp-ios-android/new-android-project-studio.png') }})

Do not forget to check the *Include Kotlin support* checkbox. On the next page you may customize
your Android requirements. Defaults will work for the tutorial, so you may
simply click through it. Similarly, on the third page, we select the *Empty Activity* option and click *Next*. 
We agree on default names of the Activity on the next screen and click *Finish*.  

It may fail opening the project with a Gradle import error. You may need to
[add Kotlin EAP repository](https://youtrack.jetbrains.com/issue/KT-18835#focus=streamItem-27-2718879-0-0), 
for that we add the the line

<div class="sample" markdown="1" mode="groovy" theme="idea" data-highlight-only="1" auto-indent="false">

```groovy
maven { url 'https://dl.bintray.com/kotlin/kotlin-eap' }
```
</div>
into the `build.gradle` file under the both `buildscript { .. repositories { .. ` blocks.

In the IntelliJ IDEA, you may also need to make sure Gradle is running under JDK 1.8, otherwise, the project import
may [fail](https://youtrack.jetbrains.com/issue/IDEA-199397).


## Running Android Project in Android Studio

At that point we shall be able to compile and run the project. Let's click on the `App` run configuration
to have our project running either on a real Android Device or in the emulator. 


![Start the Application]({{ url_for('tutorial_img', filename='native/mpp-ios-android/studio-start-app.png') }})


# Setting up Multiplatform Project

That is the best time for us to configuration the multiplatform project right now. The multiplatform project
is the way to share code between Android, iOS and other platforms. We will have 100% Kotlin code that will
be compiled both to Android and iOS. 
