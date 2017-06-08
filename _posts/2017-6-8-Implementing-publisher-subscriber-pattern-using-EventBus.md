---
layout: post
title: Implementing publisher/subscriber pattern using EventBus
img: /images/EventBus3.jpg
---


Publisher/subscriber pattern is widely used in Android applications. It is mostly used in Activity-Fragment communication, Services and AsyncTasks. In this pattern, a subscriber waits a message from publisher when <b><em>something</em></b> happens. This message can be anything. 

In this article, I will introduce you [EventBus](https://github.com/greenrobot/EventBus) library. It is a very useful implementation of pub/sub pattern. 

## Publish / Subscribe pattern

Publish / subscribe pattern provides s messaging system between publishers and subscribers. Subscribers registers to publishers and start waiting for a <b>certain event</b> occurs. 

![_config.yml]({{ site.baseurl }}/images/EventBus-diagram.png)

When this event occurs, publisher notyfies all of its subscribers via the <b>event bus</b>.

## EventBus library

EventBus is developed by [Greenrobot](http://greenrobot.org/) team. You can add it to your project by

<code class="codeblock">compile 'org.greenrobot:eventbus:3.0.0'</code>

From now on, we can use EventBus! Ok let's start. 

First of all, we have to register our activity (or class you are using) to event bus.

~~~java
@Override
public void onStart() {
    super.onStart();
    EventBus.getDefault().register(this);
}

@Override
public void onStop() {
    EventBus.getDefault().unregister(this);
    super.onStop();
}
~~~

We said that publishers send messages to subscribers when a certain event occurs. So lets define a message.

~~~java
public class Message{
    private final String message;

    public Message(String message) {
       this.message = message;
    }

    public String getMessage() {
        return message;
    }
}
~~~

When an event occurs, a Message object will be produced and sent it to the subscriber. Thanks to the EventBus, the only thing we have to do is adding @Subscribe annotation to our method. Note that, here <b>threadMode</b> is optional.  

~~~java
@Subscribe(threadMode = ThreadMode.MAIN)
public void onMessage(Message event){
    myTextView.setText(event.getMessage());
}
~~~

Now that we subscribe to Message event, we can get events when they are posted by publisher. Posting events are also easy.

 ~~~java
EventBus.getDefault().post(new Message("Message event is occured"));
~~~

## Sticky events

When an activity is waiting an event, it can be paused by another activity. In this scenario, activity won't be able to get event even if it resumes again. For overcoming this problem, <b>sticky events</b> can be used. 

Sticky events are posted by publisher and lives until they are consumed by a subscriber. In this way, if an event is posted when subscriber is at pause state, subscriber can get the event even once it resumes again. Sticky events is posted as follows:

 ~~~java
EventBus.getDefault().postSticky(new MessageEvent("Sticky message"));
~~~

And they are consumed as follows:

 ~~~java
@Subscribe(threadMode = ThreadMode.MAIN, sticky = true)
public void onMessage(Message event) {
    myTextView.setText(event.getMessage());
}
~~~

## Conclusion

In this post, I tried to explain publish/subscribe pattern. This pattern is very useful for communicating two classes. Instead of building this pattern, we can use EventBus library. I introduced  [EventBus](https://github.com/greenrobot/EventBus) and gave some usage examples. More documentation can be found at [Greenrobot](http://greenrobot.org/).






