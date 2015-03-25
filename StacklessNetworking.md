# -- Networking -- #

### Stackless compatible socket module using asyncore ###

The existing socket module is not usable naturally in a blocking manner with Stackless because of the way that the tasklets share a thread. If a tasklet blocks in the sense that whatever it has done blocks the thread, then this blocks all the tasklets until the operation is complete. Using the standard asyncore module allows asynchronous socket usage, and by adding a minor amount of support code using channels to block calls to it until an error or a result happens, a functionally equivalent socket module replacement can be created.

This replacement module when used allows socket operations which only block the current tasklet, allowing any other tasklets which are scheduled to continue to run while the current tasklet's network operation is handled asynchronously. What was the current tasklet continues running with the result when the operation is complete. If this module is installed in place of the built-in socket module, then all existing code (whether in the standard library or provided by yourself) which uses the built-in version should inherit this behaviour allowing that existing code to be executable in parallel through the use of tasklets.

**stacklesssocket.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/stacklesssocket.py)

### Stackless compatible socket module using libevent / pyevent ###

This module is based on stacklesssocket.py, but replaces asyncore with libevent (via pyevent), aiming for higher performance. Includes basic SSL support.

**socketlibevent.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/socketlibevent.py)

### Simple HTTP Server ###

An example which adapts the standard library module BaseHTTPServer to handle concurrent requests each on their own tasklet (as opposed to using the ThreadingMixIn from the SocketServer module).

**basicWebserver.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/basicWebserver.py)

### RPC layer ###

Using the Stackless compatible socket module, it is easy to write a layer that marshals remote procedure calls across a network connection.

**stacklessrpc** - [Browse](http://code.google.com/p/stacklessexamples/source/browse/#svn/trunk/examples/networking/stacklessrpc)

### MUD server ###

A simple MUD server written using the Stackless compatible socket module.

**mud.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/mud.py)

### Chat Server ###

An example that uses stacklesssocket to provide a chat like application.
The users connect via telnet to the IP:port of the server and type in any
text and all users connected receives it.
The server identifies an special character to close the connection and handle
the connected client list.

The example is based on mud.py but uses the standard dispatcher creating a
tasklet for each connected client.

**chatServer.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/chatServer.py)