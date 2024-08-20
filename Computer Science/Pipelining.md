HTTP 1.1. Included [[Persistent Connections]] and Pipelining to avoid the high overhead associated with having to open and close TCP connections. 

Pipelining allows the client to send a bunch of requests, without waiting for a response to each. The server then sends a bunch of responses, *in the same order as their corresponding requests*, allowing client to match response to request.

However, the mere order doesn't allow the client to tell where one response ends and the other begins. A TCP connection is like a conveyor belt of packets going from server to client. How do we tell which packets belong to which request?

One solution would be to insert a delimiter, like the stick you put at the conveyor belt at a supermarket till. However, that delimiter would have to be composed of ASCII (e.g. a blank line)- how do we tell this sequence of ASCII symbols is a delimiter and not part of the data?

How about this instead: let's attach a label to the first packet on the belt saying how many packets after it belong to one group with it. That's the `Content-Length` header. It allows client to tell where one response payload starts and the next begins.

It works in reverse too: client requests which have a body (e.g. form data) carry `Content-Length` header for the same reason. 

NB: You can have [Persistent Connections] without Pipelining- you just wait for a response to each request before sending the next one. You can't have Pipelining without Persistent Connections though.

This strategy only works when the server knows the length of the data it is sending. What if data is generated dyunamically? 
