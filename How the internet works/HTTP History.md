## HTTP 0.9

- Request: only GET method, followed by URI. No headers
```
GET /index.html
```

- Response: Only the response body. Only HTML. No headers
```
(response body)
(connection closed)
```

## HTTP 1.0
### What's new
- New methods (POST, HEAD)
- Headers added - support for authorisation, caching, content encoding etc.
- More content types (video, image, plain text)
### Drawbacks
- Only single-request connections. Each connection required new [TCP 3-way handshake](TCP.md#Opening%20connection%203-way%20handshake)
## HTTP 1.1
### What's new
- [[Persistent connections]] 
- [[Pipelining]]
- [[Chunked transfers]]
- Even more methods (PUT, PATCH, OPTIONS, DELETE)
- Client cookies
- Enhanced compression, caching etc.

### Drawbacks
- **Head-of-line blocking** - even with pipelining, requests are fulfilled sequentially. Even though next request can be sent without waiting for the previous one to receive a response, responses still must be received and processed in order. Thus, even though requests 1, 2 and 3 can be sent one after the other, if response 2 is taking a long time to get to client, it'll block response 3. 
## HTTP 2.0
- Binary Protocol (instead of Textual) and  [[Multiplexing]]
- Header compression using [HPACK](HPACK.md)
- [[Server Push]]
- **Request prioritisation** - client can decide which streams are to be fulfilled first by the server. Client can also change this priority at any moment. For instance, HTML is more important to the client than CSS. 
- [TLS](SSL%20and%20TLS.md) - whilst not mandatory in theory, in practice most clients demand that the protocol use security- HTTPS
## HTTP 3.0
- Uses [UDP and not TCP](UDP.md)

