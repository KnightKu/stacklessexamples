# -- Networking With Twisted -- #

### Twisted - Timer Integration ###

In this example, most of the time is spent in the Twisted event loop. This approach allows you to control the granularity of tasklet execution based on time. At 30fps, a timer executes that schedules Stackless tasklets to run - a simple tasklet just prints "do-op".

**TwistedTimerReactorControl.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/TwistedTimerReactorControl.py)

### Twisted - Yield Integration ###

In this example, a large portion of the time is spent in Stackless. This approach allows you to control the granularity of tasklet execution based on cooperative yield points in the tasklet. At 30fps, a timer executes that prints the fps. A simple tasklet just prints "." and yields to the reactor. The reactor processes all pending events, then reschedules the tasklet.

This example eats a lot of cpu, because no time is spent blocking - the control is constantly being passed back and forth between the reactor and Stackless.

**TwistedYieldReactorControl.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/TwistedYieldReactorControl.py)

### Twisted - Deferred Integration ###

In this example, most of the time is spent in the Twisted event loop. This approach allows you to control the granularity of tasklet execution based on deferred operations a tasklet waits on. At 30fps, a timer executes that prints the fps. A simple tasklet begins a deferred operation, and waits for the result. During that time, control is returned to the reactor.

Because of the possibility that a deferred operation completes immediately, a channel subclass is used to hold the value and return it without any rescheduling. stackless.channel.send() would otherwise block the tasklet before it could call stackless.channel.receive().

**TwistedYielddeferReactorControl.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/TwistedYielddeferReactorControl.py)

### Twisted Perspective Broker Producer-Consumer ###

This example uses Stackless together with Twisted Perspective Broker(PB) Perspective Broker (affectionately known as PB) is an asynchronous, symmetric network protocol for secure, remote method calls and transferring of objects.

PB has support for direct or authenticated sessions where the user receives a "Perspective" containning the methods it could call. This example mimics the producer consumer example having the production queue (stack) in a server and the producers and consumers accessing it over the network using predefined exported methods.

For more information on PB check: http://twistedmatrix.com/projects/core/documentation/howto/index.html

**twistedProdCon-Server.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/twistedProdCon-Server.py)

**twistedProdCon-Client.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/twistedProdCon-Client.py)

### Twisted Webserver ###

Demonstrates the use of Stackless with Twisted to implement a web server. It has a downside in that Stackless' scheduling cannot run while Twisted blocks.

**TwistedWebserver.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/TwistedWebserver.py)

2010 Note. As of 2008, this is an obsolete approach. I wrote this when I didn't know better. I will soon remove this example.

### Twisted Threaded Webserver ###

Demonstrates the use of Stackless with Twisted to implement a web server. Unlike the previous example Twisted is run in a separate thread from the Stackless scheduler, which allows tasklets to continue executing while Twisted blocks.

2010 Note. As of 2008, this is an obsolete approach. I wrote this when I didn't know better. I will soon remove this example.

**TwistedWebserverThreaded.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/twisted/TwistedWebserverThreaded.py)

### Partial Solution to Santa Claus Problem ###

simpleSanta.py - http://code.google.com/p/stacklessexamples/downloads/detail?name=simpleSanta.py

Demonstrates the use of Twisted and the new stackless.select() method in solving a non-trivial concurrency problem - John Trono's <a href='http://delivery.acm.org/10.1145/190000/187391/p8-trono.pdf?key1=187391&key2=2436321921&coll=DL&dl=ACM&CFID=113381262&CFTOKEN=31691828'>The Santa Claus Problem</a> Use in conjunction with stackless\_v2.py