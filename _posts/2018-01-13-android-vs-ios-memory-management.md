---
layout: post
title: "How is iOS different from Android, requires only a needful RAM in iPhones compared to Android phones?"
tags: [Android, iOS]
image: https://www.anudit.in/assets/img/android_vs_ios/android-vs-ios.jpg
share-img: https://www.anudit.in/assets/img/android_vs_ios/android-vs-ios.jpg
---

__Just for thought:__ If you have ever wondered why iPhones running iOS aren't much RAM extensive or doesn't require much RAM than most of the Android Flagship phones are using? Why spokespersons at *Apple Inc.* aren't boastful about the amount of RAM available to most modern iPhones while showcasing them?


The reason is something fundamental and at the machine level, that means what exactly iOS do differently than Android in order manage such smooth performance despite being having less RAM. Let us find out, read along.


<center><h2>iOS vs Android</h2></center>

<center><img src="/assets/img/android_vs_ios/apple-vs-android.png"></center>


<h3>Architecture:</h3>
__Android__ was built to run Java applications across any processor - *x86, ARM, MIPS*, due to decisions made in the early days of Android's development. Android does this via a virtual-machine, which is like a virtual computer layer between the actual hardware and the software (Java software in Android's case).

Lots of memory is needed to manage this virtual machine and store both the Java byte-code and the processor machine-code as well as store the system needed for translating the Java byte-code into your device's processor machine-code.

Android was also designed to be a multi-tasking platform with background services, so in the early days, extra memory was needed for this (but it's less relevant now with iOS having background-tasks).

Android is also big on the garbage-collected memory model - where apps use all the RAM they want and the OS will later free unused memory at a convenient time (when the user isn't looking at the screen is the best time to do this!).

__iOS__ was designed to run Objective-C applications on known hardware, which is an *ARM* processor. Because *Apple* has full control of the hardware, they could make the decision to have native machine code (No virtual machine) run directly on the processor. Everything in iOS is lighter-weight in general due to this, so the memory requirements are much lower.

iOS originally didn't have background-tasks as we know them today, so in the early days, it could get away with far less RAM than what Android needed. RAM is expensive, so Android devices struggled with not-enough-memory for quite a few years in the early days, with iOS devices happily using 256MB and Android devices struggling with 512MB.

<h3>Memory Management:</h3>

In iOS, the memory is managed by the app, rather than a garbage collector. In the old days developers would have to use *alloc* and *dealloc* to manage their memory themselves - but now we have automatic reference counting, so there is a mini garbage collection system happening for iOS apps, but it's on an app basis and it's very lightweight and only uses memory for as long as it is actually needed (and with *Swift* this is even more optimised).

Android's original virtual machine, *Dalvik*, was built in an era when the industry did not know what CPU architecture would dominate the mobile world (or if one even would). Thus it was designed for *x86, ARM* and *MIPS* with room to add future architectures as needed.

The iPhone revolution resulted in the industry moving almost entirely to use the *ARM* architecture, so *Dalvik's* compatibility benefits were somewhat lost. More-so, *Dalvik* was quite a battery intensive - once upon a time Android devices had awful battery life (less than a day) and iOS devices could last a couple of days.

<h3>Runtime Environment:</h3>

Android now uses a new Runtime called __Android RunTime (ART)__. This new runtime is optimised to take advantage of the target processors as much as possible (*x86, ARM, MIPS*) - and it is a little harder to add new architectures.

ART does a lot differently to *Dalvik*; it stores the translated Java byte-code as raw machine-code binary for your device. This means apps actually get faster the more you use them as the system slowly translates the app to machine-code. Eventually, only the machine code needs to be stored in memory and the byte-code can be ignored (frees up a lot of RAM). (This is Dalvik, not ART). ART compiles the Java byte-code during the app install (how could I forget this? *Google* made such a huge deal about it too!).

In recent times, Android itself has become far more power aware, and because it uses a virtual machine Android can make power-efficiency decisions across all apps that iOS cannot (as easily). This has resulted in the bizarre situation that most developers thought they would never see where Android devices now tend to have longer battery life (a few days) than iOS devices - which now last less than a day.

The garbage collected memory of Android and its heavy multi-tasking still consumes a fair amount of memory, these days both iOS and Android are very well optimised for their general usage. The OS tend to use as much memory as it can to make the device run as smoothly as possible and as power-efficient as possible.


<h3>So, What Have We Learnt?</h3>
Remember task managers on Android? They pretty much aren't needed anymore as the OS does a fantastic job on its own. Task killing, in general, is probably worse for your phone now as it undoes a lot of the spin-up optimisation that is done on specific apps when they are sent to the background. iOS gained task killing for some unknown reason (probably iOS users demanding one be added because Android has one) - but both operating systems can do without this feature now. The feature is kept around because users would complain if these familiar features disappear. I expect in future OS versions the task-killers won't actually do anything and will become a placebo - or it will only reset the app's navigation stack, rather than kills the task entirely. 

So, in fact, you don't need to remove those recent apps from the recent activity tab. It is better to not swipe away apps. By swiping them away, you're undoing the memory and state optimisations that were applied to the app, so when you launch it the app needs to do a cold-boot and rebuild all that memory and reload all the stuff it previously had cached.

That's more processor, RAM and flash usage (in some cases with rendering, more GPU usage) - that's more battery usage.

There might be subtle differences among them, each stands better in their own unique way, you may love them both or not like them at all but in the end, it seems, well see the picture which is self-evident.
<center><img src="/assets/img/android_vs_ios/android-loves-ios.jpg"></center>

Thank you for reading.