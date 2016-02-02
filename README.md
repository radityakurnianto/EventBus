EventBus
========
EventBus is publish/subscribe event bus optimized for Android.<br/>
<img src="EventBus-Publish-Subscribe.png" width="500" height="187"/>

EventBus...

 * simplifies the communication between components
    * decouples event senders and receivers
    * performs well with Activities, Fragments, and background threads
    * avoids complex and error-prone dependencies and life cycle issues
 * makes your code simpler
 * is fast
 * is tiny (~50k jar)
 * is proven in practice by apps with 100,000,000+ installs
 * has advanced features like delivery threads, subscriber priorities, etc.

 [![Build Status](https://travis-ci.org/greenrobot/EventBus.svg?branch=master)](https://travis-ci.org/greenrobot/EventBus)

Index and its Limitations
-------------------------
The "subscriber index" is a new feature of EventBus 3. It is an optional optimization to speed up initial subscriber registration. The subscriber index can be created during build time using EventBus' annotation processor. It is not required to use the index, but it's recommended on Android because of its poor reflection speed regarding annotations.

Note that only those @Subscribers methods can be indexed for which the subscriber AND event class are public. Non-indexed methods have to be looked-up at runtime using reflection.

Also, @Subscribe annotations are not recognized when inside of anonymous classes

EventBus in 4 steps
-------------------
1. Define events:<br/>
<code>public class MessageEvent { /* Additional fields if needed */ }</code><br/><br/>
2. Register your subscriber (in your onCreate or in a constructor):<br/>
<code>eventBus.register(this);</code><br/><br/>
3. Declare your subscribing method<br/>
<code>@Subscribe</code><br/>
<code>public void onEvent(AnyEventType event) {/* Do something */};</code><br/><br/>
4. Post events:<br/>
<code>eventBus.post(event);</code>

Add EventBus to your project
----------------------------
EventBus is available on Maven Central. Please ensure that you are using the latest version by [checking here](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22de.greenrobot%22%20AND%20a%3A%22eventbus%22)

Gradle:
```
    compile 'org.greenrobot:eventbus:3.0.0'
```

Maven:
```
<dependency>
    <groupId>org.greenrobot</groupId>
    <artifactId>eventbus</artifactId>
    <version>3.0.0</version>
</dependency>
```

[Or download EventBus from Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22de.greenrobot%22%20AND%20a%3A%22eventbus%22)

How-to, Developer Documentation
-------------------------------
Details on EventBus and its API are available in the [HOWTO document](HOWTO.md).

How does EventBus compare to other solutions, like Otto from Square? Check this [comparison](COMPARISON.md).

Additional Features and Notes
-----------------------------

* **Based on annotations:** Event handling methods can be named however you want, and only need to be annotated with **@Subscribe**.
* **Performance optimized:** It's probably the fastest event bus for Android.
* **Convenience singleton:** You can get a process wide event bus instance by calling EventBus.getDefault(). You can still call new EventBus() to create any number of local busses.
* **Subscriber and event inheritance:** Event handler methods may be defined in super classes, and events are posted to handlers of the event's super classes including any implemented interfaces. For example, subscriber may register to events of the type Object to receive all events posted on the event bus.

FAQ
---
**Q:** How is EventBus different to Android's BroadcastReceiver/Intent system?<br/>
**A:** Unlike Android's BroadcastReceiver/Intent system, EventBus uses standard Java classes as events and offers a more convenient API. EventBus is intended for a lot more uses cases where you wouldn't want to go through the hassle of setting up Intents, preparing Intent extras, implementing broadcast receivers, and extracting Intent extras again. Also, EventBus comes with a much lower overhead.

**Q:** How to do pull requests?<br/>
**A:** Ensure good code quality and consistent formatting. EventBus has good test coverage: if you propose a new feature or fix a bug, please add a unit test.

Release History, License
------------------------
[CHANGELOG](CHANGELOG.md)

Copyright (C) 2012-2016 Markus Junginger, greenrobot (http://greenrobot.org)

EventBus binaries and source code can be used according to the [Apache License, Version 2.0](LICENSE).

More Open Source by greenrobot
==============================
[__greenrobot-common__](https://github.com/greenrobot/greenrobot-common) is a set of utility classes and hash functions for Android & Java projects.

[__greenDAO__](https://github.com/greenrobot/greenDAO) is an ORM optimized for Android: it maps database tables to Java objects and uses code generation for optimal speed.

[Follow us on Google+](https://plus.google.com/b/114381455741141514652/+GreenrobotDe/posts) to stay up to date.