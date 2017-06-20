---
layout: post
title: 5 tips for speeding up your Gradle builds
img: /images/gradle.png
---

<b>Gradle</b> is a very useful tool for Android developers. Unfortunatelly, it needs a little bit speed boost. Every Android developer knows that feel when we have to add a new library to the Gradle file. Adding another library means we will wait for Gradle to <b>sync</b> our project, again, and waiting for this is really annoying sometimes. But we can speed it up with some little tricks. 


## Tip 1 - Use the latest Gradle plugin

Gradle is constantly being developed and improved. Thus, the newer and stable version will give better performance. Go to your <b>settings</b> gradle file and change the plugin version to the latest.

~~~java
buildscript {
    repositories {
        google()
    }
 
    dependencies {
        classpath ‘com.android.tools.build.gradle:3.0.0-alpha3’
    }
}
~~~
<br>

## Tip 2 - Use only needed resources

The resources we use not only increase APK size but also build time for Gradle. Therefor, adding only needed resources drops the build time. You can add all other resources for <b>production</b> builds if you want. 

~~~java
productFlavors {
  development {
    minSdkVersion 21
    //only package english translations, and xxhdpi resources   
    resConfigs (“en”, “xxhdpi”)
  }
}
~~~
<br>


## Tip 3- Don't use PNG optimization

Android Studio comes with an optimization feature for <b>PNG</b> files. This is required for production builds but not required for <b>development</b> builds. PNG optimizations are enabled by default, but are not needed for development builds. Disable them to speed up your builds.

~~~java
android {
  if (project.hasProperty(‘devBuild’)){
    aaptOptions.cruncherEnabled = false
  }
}
~~~
<br>

## Tip 4- Use always instant run

Instant run is one the best features Android Studio ever had. Though, it has some bugs need to be fixed. Nevertheless, you should always use it instead of normal run option, because it really fastens the app's loading time. 

<br>

## Tip 5- Use Gradle caching

<b>Gradle Caching</b> is new feature comes with Gradle 3.5. It enables for Gradle to cache and reuse outputs from previous builds.

~~~java
# Set this in gradle.properties
org.gradle.caching=true
~~~

<br>
## Conclusion

In this post, I tried to give some tips for fastening your Gradle. There are a lot more tips for Gradle of course and they are widely explained in Google I/O 2017 session. I suggest you to watch it. 

### References

<a href="https://android.jlelse.eu/how-to-speed-up-your-slow-gradle-builds-5d9a9545f91a">https://android.jlelse.eu/how-to-speed-up-your-slow-gradle-builds-5d9a9545f91a</a>






