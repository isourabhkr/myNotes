# Proxy

A proxy or a forward proxy is a server/application that sits in-front of client machines and controls how and what the
clients interact with other servers/services on other networks. like a middleman.

On the other hand reverse proxy sits in-front of multiple servers which controls the incoming clint requests, in terms
of which internal server process the request. The response from the internal servers are intercepted by the 
reverse-proxy server and it then interacts with the original server. Reasons to do it:
* Load balancing
* Protection from attacks
* Caching
* SSL Termination