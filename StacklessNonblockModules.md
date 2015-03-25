# Nonblocking Stackless Modules #

These modules allow seamless integration to sockets and fileIO in a nonblocking fashion. They can be used substituting the original python modules.

### Stackless compatible socket module using asyncore ###

The existing socket module is not usable naturally in a blocking manner with Stackless because of the way that the tasklets share a thread. If a tasklet blocks in the sense that whatever it has done blocks the thread, then this blocks all the tasklets until the operation is complete. Using the standard asyncore module allows asynchronous socket usage, and by adding a minor amount of support code using channels to block calls to it until an error or a result happens, a functionally equivalent socket module replacement can be created.

This replacement module when used allows socket operations which only block the current tasklet, allowing any other tasklets which are scheduled to continue to run while the current tasklet's network operation is handled asynchronously. What was the current tasklet continues running with the result when the operation is complete. If this module is installed in place of the built-in socket module, then all existing code (whether in the standard library or provided by yourself) which uses the built-in version should inherit this behaviour allowing that existing code to be executable in parallel through the use of tasklets.

**stacklesssocket.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/stacklesssocket.py)

### Stackless compatible socket module using libevent / pyevent ###

This is based on stacklesssocket.py, but replaces asyncore with libevent (via pyevent), aiming for higher performance. Includes basic SSL support.

**socketlibevent.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/socketlibevent.py)

### Stackless compatible file module using Windows IOCP ###

This is an asynchronous file class in order to have a file module replacement that uses channels and a windows async API to allow its methods to block just the calling tasklet not the entire interpreter.

**stacklessfileIOCP.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/fileIO/stacklessfileIOCP.py)


### Stackless compatible file module using a ThreadPool ###

This module wraps the file class in order to have a file module replacement that uses channels and a threadpool to allow calls to it to block just the calling tasklet until a delayed event occurs.

Not all methods of the file module are wrapped as unblocking by this file.
Examples of it in use can be seen at the bottom of it.

**stacklessfileThreadPool.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/fileIO/stacklessfileThreadPool.py)