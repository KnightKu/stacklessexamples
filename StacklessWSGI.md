# -- WSGI -- #

For details on the WSGI specification, see [PEP-333](http://www.python.org/dev/peps/pep-0333/)

### Stackless WSGI Server ###

Commonly, web servers server HTTP requests by dispatching processing to a thread from a thread pool (there are many other models of course). In this example, a WSGI compliant web server is implemented, that dispatches requests to WSGI applications running in a dedicated tasklet.

The server uses the asyncore module for network communcation. The HTTP part, i.e. parsing of HTTP requests etc. are borrowed from [CherryPy's](http://www.cherrypy.org/) WSGI server.

**stacklesswsgi.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/wsgi/stacklesswsgi.py)

### WSGI Application with long-polling ###

Long-polling is a technique (also known as [Comet](http://en.wikipedia.org/wiki/Comet_%28programming%29)) to simulate server-push, where a HTTP server pushes data in real time to the client. HTTP requests can span a long time, several seconds and even longer. This does not scale well with threaded web-servers and usually calls for some sort of asynchronous event-based solutions.

This small example shows how that is achieved with Stackless' microthreads.

**app\_comet.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/wsgi/app_comet.py)

### _Sessionless_ web applications ###

Since HTTP is by nature stateless, web application developers must often resort to techniques like cookies, server-side sessions etc. to keep persistent state in a web application. This example shows how tasklets allow us to suspend the web-application execution between requests, effectively eliminating such state-keeping measures since state is stored in local variables inside the tasklet.

**app\_sessionless.py** - [Download](http://stacklessexamples.googlecode.com/svn/trunk/examples/networking/wsgi/app_sessionless.py)