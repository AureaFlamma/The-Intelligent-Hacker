# The Browser

## Critical Rendering Path

### 1. Navigation
- [DNS Lookup](DNS.md)
- [TCP Handshake](TCP.md#Opening%20connection%203-way%20handshake)
- [SSL/TLS Handshake](SSL%20and%20TLS.md#SSL/TLS%20Handshake)
### 2. Parsing
- HTML gets parsed into [[Document Object Model (DOM)]]
- CSS gets parsed into [[Cascading Style Sheets Object Model (CSSOM)]]
- JS gets parsed into [[abstract syntax tree]]
- All the above and ARIA get parsed into [[Accessibility Object Model]]
### 3. Render
- DOM and CSSOM get combined into a [[render tree]]
- Layout is established (position and size of elements)
	- Layout = initial layout
	- Reflow =  any layout computation after initial, e.g. when an image whose dimensions we've not specified is finally fetched after a delay.
- Paint - actual rendition of pixels on screen
- Layers might sometimes be necessary (e.g. when). If so, Compositing will also be needed.
### 4. Interactivity


## Further resources
[MDM web docs](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work)
[Youtube video](https://www.youtube.com/watch?v=5rLFYtXHo9s)

