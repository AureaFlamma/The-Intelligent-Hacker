- TLS/SSL handshake as output in terminal
- fetch API
-
- Man-in-the-middle attack
- SSL
- _origin constraint_
- server-sent events api
- Quic
- UDP
- Quic is an alternative to TCP

- Common status codes to remember

## Anatomy of a request

### Example
🟪 *Status line*
🟫 *Header*
🟨 *Body*
#### Example request
```
POST /submit-form HTTP/1.1  🟪
Host: www.example.com   🟫
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:91.0) Gecko/20100101 Firefox/91.0 🟫
Content-Type: application/x-www-form-urlencoded 🟫
Content-Length: 27 🟫
Connection: keep-alive 🟫

name=John+Doe&age=30  🟨
```

### Example response
```
HTTP/1.1 200 OK 🟪
Date: Thu, 27 Jun 2024 14:10:00 GMT 🟫
Server: Apache/2.4.41 (Ubuntu) 🟫
Content-Type: text/html; charset=UTF-8 🟫
Content-Length: 138 🟫
Connection: keep-alive 🟫

<!DOCTYPE html> 🟨
<html>
<head>
    <title>Submission Result</title>
</head>
<body>
    <h1>Form submitted successfully!</h1>
</body>
</html>

```
### Status line
1. Requests
	- HTTP Method
	- Request URI
	- HTTP Version
2. Responses
	- HTTP Version
	- Status Code
	- Reason Phrase
### HTTP Methods
Found on requests
- **GET** - clients requests data from server
- **POST** - client adds data to server
- **PUT** - client replaces data on server
- **DELETE** - client deletes data from server
### Status codes
Found on responses
- **1xx** Informational
- **2xx** Success
- **3xx** Redirect
- **4xx** Client Error
- **5xx** Server Error
#### Common status codes
- 200 OK
- 201 OK created
- 301 Moved to new URL
- 304 Not modified (Cached version)
- 400 Bad request
- 401 Unauthorised
- 404 Not found
- 500 Internal server error
### Headers
[List of all HTTP headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
#### Request
- `Cookie` - contains stored HTTP cookies associated with the server (i.e. previously sent by the server with the `Set-Cookie` header or set in JavaScript using `Document.cookie`).
- `Accept` - Specifies the media type that the client is willing to receive from the server. Part of [[content negotiation]]
- `Accept-Encoding` - Indicates the content encoding method (e.g. gzip, deflate) the client can understand. Part of [[content negotiation]]
- `Accept-Language` - Specifies preference for a natural language. Part of [[content negotiation]]. You can set the preference in your browser settings. Usually browsers will include in this header a list of languages with decreasing `q` values, indicating order of preference for languages. E.g.
```
Accept-Language: fr,la;q=0.8,en-GB;q=0.5,en;q=0.3
```
  It reads: Latin, then French at 0.8 importance, then British english at 0.5 importance, then English at 0.3 importance.
  - 
#### Response
- `Accept-CH`
#### Representation
#### Payload


## History

## TLS vs UDP

## Encryption - HTTPS