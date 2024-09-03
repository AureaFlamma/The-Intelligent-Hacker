In HTTP/1.x, a lot of headers would be sent repeatedly (e.g. cookies, `User-Agent` etc.). HPACK is a technique implemented in HTTP/2.0 to avoid this. Here's how it works:
-  server and client maintain a static table of most common headers
- server and client have a dynamic table of recently used headers
- If the header which is about to be sent is already in either table, its index is sent instead.
- If the header isn't in either table, it is sent entirely and entered into the dynamic table.
- If the header is in a table, but its value is slightly changed (e.g. only one part of a cookie) from what is in the table, an update is sent.
- If the header is in a table, but its value is significantly changed, the whole header is sent and the table is updated.

For those headers which are actually sent (rather than those which are referred to by indexes), [[Huffman encoding]] is used to compress them. 

