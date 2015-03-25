# An introduction for newcomers #

[Stackless Python](http://www.stackless.com) is an enhanced version of the Python programming language. It allows programmers to reap the benefits of thread-based programming without the performance and complexity problems associated with conventional threads. The microthreads that Stackless adds to Python are a cheap and lightweight convenience which can if used properly, give the following benefits:

  * Improved program structure.
  * More readable code.
  * Increased programmer productivity.


# Stackless Documentation #

In the repository, you will find documentation gathered from the internet related to Stackless design, presentations and tutorials.


# Stackless Usage #

In this project we aim to have usage examples with Stackless from beginners to real life problems.

Here follows links to examples for features found in Stackless Python. There are examples where only Stackless is used and pages dedicated for Stackless integration with external frameworks like [Twisted](http://www.twistedmatrix.com) and [PyQt](http://www.riverbankcomputing.co.uk).

  * [StacklessNonblockModules](StacklessNonblockModules.md) - Socket and file nonblocking modules
  * [StacklessThreads](StacklessThreads.md) - Examples integrating stackless with python threads
  * [StacklessNetworking](StacklessNetworking.md) - Examples using socket via nonblocking stacklesssocket module.
  * [StacklessWSGI](StacklessWSGI.md) - Examples implementing a [WSGI](http://www.python.org/dev/peps/pep-0333/) compliant server and applications.
  * [StacklessTwisted](StacklessTwisted.md) - Twisted integration with stackless
  * [StacklessGUI](StacklessGUI.md) - GUI integration (PyQt, etc)

### Factorial ###

Factorial example using stackless to break Python's recursion limit of 1000

**factorial.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/factorial.py)

### Producer - Consumer ###

This example illustrates a producer - consumer chain where each agent runs on its tasklet.
We a tasklet that take care of sleep calls.

**producerConsumerTextmode.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/producerConsumerTextmode.py)

There is also a version of producer/consumer example based on BeNice and alternative schedule approach (See below).

**producerConsumerAlternativeSched.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/producerConsumerAlternativeSched.py)

### Tasklet Pickling ###

Tasklets can be pickled to a string or file and then unpickled to have its state restored even in another machine.

**pickleChannels.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/pickleChannels.py)

### Channel With Timeout ###

The channel implemented here can have a timeout so the tasklets that are waiting on it receives an exception when its timeout expires.

**channelWithReceiveTimeout.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/channelWithReceiveTimeout.py)

### Normal Scheduling ###

This example shows the basic usage of Stackless and shows a function that combined with its manager handles sleeping tasklets.

**scheduleNormal.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/scheduleNormal.py)

### Alternative Scheduling ###

Here there is an alternative approach on scheduling:

Benefits of this approach:

- It lends itself well to embedding, if implemented in C or C++.
- It allows more precise control.

Limitations of this approach:

- The expectation is that the scheduler will be empty because of this
> will exit pretty much immediately.  So anything which calls to
> 'stackless.schedule' rather than using 'BeNice' or 'Sleep' will
> break this scheduling model and prevent it from working as
> expected.  After all, if there are tasklets in the scheduler it
> continues to run and does not exit.

> Ideally 'stackless.schedule' should be patched to call BeNice.  Or
> calls to it just avoided completely.

**scheduleAlternative.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/scheduleAlternative.py)

### Alternative Sleeping (threaded) ###

Here is a module that implements 'sleep' and 'wake' functions.

This implementation doesn't busy wait, as other examples shown in this wiki, by
using another system thread to run the sleeping tasklets manager.

_**sleeping.py** -
[Download](https://bitbucket.org/nettok/useless/src/tip/useless/_sleeping.py)_

## Experimenting with New Stackless Features ##

**stackless.py** -
[Download](http://stacklessexamples.googlecode.com/svn/trunk/sandbox/select/stackless.py)

PyPy stackless.py is a python based implementation of Stackless Python. stackless.py is not a full implementation of Stackless Python. Since stackless.py is written in Python and implements the API, it makes a great testbed for prototyping new features. This modified version of stackless.py implements a stackless.select() that is similar to Newsqueak/Go's select, albeit not a language feature. Please see the Santa Claus example to see how stackless.select() can be used [Download](http://stacklessexamples.googlecode.com/svn/trunk/sandbox/select/simpleSanta.py)