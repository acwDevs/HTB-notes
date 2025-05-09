HEAD

Determine request options allowed
```shell-session
curl -i -X OPTIONS http://SERVER_IP:PORT/
```


Using HEAD request instead of GET
	Most notably the `HEAD` method, which is identical to a `GET` request but does not return the body in the HTTP response


We can use the same concept of changing the request method in order to bypass content filters
	Can be done by changing request method during interception on burp
