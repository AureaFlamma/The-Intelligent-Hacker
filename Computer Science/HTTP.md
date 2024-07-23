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
- **HEAD** - clients requests only the headers that would be returned if the request was `GET`. Useful for seeing if the resource which is about to be sent is a large one (by looking at `Content-Length` response header)
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
  - `Authorization` Contains the credentials to authenticate a user agent with a server. Usually client sends first request without `Authorisation` header, server replies with `401 Unauthorized` and `WWW-Authenticate` header. 
  - `Cache-Control` holds directives (instructions) that control caching in browser and middleware (Proxies, CDNs). Present in both Request and Response headers.
  - `Connection` indicates whether the client wants the connection to stay open (`Connection: keep alive`) or be closed (`Connection: close`) after the current transaction. Rarely used in HTTP/2 and HTTP/3.
  - `Host` specifies the host and TCP port number of the server to which the request is being sent. Port number can be ommited, in which case the default port is implied (e.g., `443` for an HTTPS URL, and `80` for an HTTP URL).
  - **`If-Modified-Since`** request HTTP header makes the request conditional: the server sends back the requested resource, with a `200` status, only if it has been last modified after the given date. If the resource has not been modified since, the response is a `304` without any body.
  - `If-None-Match` makes the request conditional. For `GET` and `HEAD` methods, the server will return the requested resource, with a `200` status, only if it doesn't have an `ETag` matching the given ones. For other methods, the request will be processed only if the eventually existing resource's `ETag` doesn't match any of the values listed.
  - `Referer` (sic) contains the URL of the website from which the request was made. Unlike `Origin`, which contains only protocol and domain name, `Referer` contains protocol, domain, port (sometimes), path and query string.
  - `Origin` contains domain from which request was made
```
// Let's say we are visiting example.com and clicking a link that takes us to example2.com. The request sent to example2.com's server will be:
    
Referer: https://example.com/page1.html?query=123
Origin: https://example.com
```
- `User-Agent` contains info about browser and OS:
```
User-Agent Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:128.0) Gecko/20100101 Firefox/128.0
```

#### Response
- `Accept-CH`
- `WWW-Authenticate` contains a list of authentication methods ("challenges") which might be used to gain access to a protected resource. 
- `Cache-Control` holds directives (instructions) that control caching in browser and middleware (Proxies, CDNs). Present in both Request and Response headers
- `Set-Cookie`
- `ETag` Specifies the version of the resource. Requested with `If-None-Match` request header. Useful for not sending the same data multiple times (`GET`) and for version control (`PUT`, `PATCH`, `DELETE`)
#### Representation
#### Payload


## History

## TLS vs UDP

## Encryption - HTTPS

## Authorisation 
Might be same as encryption

## Caching

## Etag
and resource updating

## Referer

## CORS