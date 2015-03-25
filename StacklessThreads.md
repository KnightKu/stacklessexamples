# -- Threading -- #

### Scheduling and Threads ###

The Stackless scheduler is directly linked to the current thread, so if you use more than one thread, the tasklets you create on each will be local to that thread. You can see the thread-safe Sleep function independently manage the tasklets that were added on any given thread on that thread.

**threadscheduling.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/threading/threadscheduling.py)

### Channels and Threads ###

Tasklets can work between channels regardless of which thread the tasklets belong to. This example demonstrates a shared sleep function which works on the initial main thread and handles sleeps from tasklets on both itself and an identical second spawned thread. It isn't recommended that this approach be used, as the 'preference' attribute of the channel does not work with regard to tasklets from another thread and these tasklets are always preferred being switched to immediately.

**interThreadChannels.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/threading/interThreadChannels.py)