#### Http?
##### What it is?
- HTTP stands for Hypertext Transfer Protocol.
- It's a language that allows web clients and servers to communicate with each other.
- HTTP is a request-response protocol.
- HTTP is a stateless protocol, which means that the server does not keep any data (state) between two requests.

##### Http 0.9
- HTTP 0.9 was the first version of HTTP protocol.
- It was a simple protocol that allowed clients to request content a server.
- It has single method called `GET`.
```angular2html
GET /index.html
```
```angular2html
(response)
(connection closed)
```

##### Http 1.0
- HTTP 1.0 was the second version of HTTP protocol.
- It was enhanced version of HTTP 0.9, which supports other HTTP methods like `POST`, `PUT`, `DELETE`, etc.
- It supports of sending images, video files in response.
- `headers` added to both request/response.
- It supports `status codes`, `caching`, `character set support`, `authorization` etc.
- The drawback was that `It opens a new connection for each request/response pair`, and it is also `Stateless`.
```angular2html
GET / HTTP/1.0
Host: cs.fyi
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*
```
```angular2html
HTTP/1.0 200 OK 
Content-Type: text/plain
Content-Length: 137582
Expires: Thu, 05 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 5 August 1996 15:55:28 GMT
Server: Apache 0.84

(response body)
(connection closed)
```
###### 3-Way Handshake
- It's a procedure which is used to establish a connection between client and server.
- It sends some dummy data to make a communication channel between client and server before exchanging the actual data.
- It's a 3-step process.
    - `SYN`, `SYN-ACK`, `ACK`


##### Http 1.1
- The improvements are:
  - New Http methods like `PUT`, `PATCH`, `OPTIONS` and `DELETE`.
  - Hostname identification header 
  - `Persistent connections`: Solved the problem of Http 1.0, where it opens a new connection for each request/response pair.
     For closing the connection, header `Connection: close` is used.
  - `Pipelining`: It allows multiple requests to be sent at a time without waiting for the response of the previous request, 
    and server had to send the response in same order as the requests were received.
  - `Chunked transfer encoding`: It allows the server to send the response in chunks, without having to know the size of the response in advance.
  - Includes `Digest, Proxy Authentication` and `Range Requests`, `Caching` etc.

- The drawbacks
  - `Head-of-line blocking`: It means that if a request is taking too long to process, then all the subsequent requests will be blocked.
  - `Security`: It does not support encryption by default.
  - `Header size`: It does not compress the headers, which increases the size of the request/response.

##### Http 2.0
- The improvements are:
  - `Binary Protocol` instead of text protocol.
  - `Multiplexing`: It allows multiple requests to be sent at a time without waiting for the response of the previous request.
  - `Header Compression`
  - `Security`
  - `Request Prioritization`: It allows the client to specify the priority of each request.

- For more details, Refer: [Http Evolutions](https://cs.fyi/guide/http-in-depth)
