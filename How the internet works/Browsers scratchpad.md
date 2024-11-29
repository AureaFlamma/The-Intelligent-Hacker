- TTFB - Time To First Byte
- TCP slow start
- DOM vs CSSOM
- critical rendering path
- Preload scanner

Steps to load:
- navigation
- DNS lookup
- TCP handshake
- TLS negotiation
- Response:
	- Time to First Byte
	- Congestion control/TCP slow start
		- Congestion window
- Parsing
	- DOM
		- Preload scanner.
	- CSSOM
- JS Compilation
	- abstract suntax tree
- Accessibility parsing
	- accessibility object model
- Style
	- Combining DOM and CSSOM into a render tree. 
- Layout
	- Assignes each DOM element its position and size
	- Layout = initial layout, reflow = any layout computation after initial, e.g. when an image whose dimensions we've not specified is finally fetched after a felay.
- Paint
	- first Meaningful Paint.
	- Layers
		- Compositing
- Interactivity
	- Time to Interactive.

Things that slow down page:
- Bad HTML structure which slows down parsing
- scripts block parsing (images and CSS sheets don't), especially if they are async.
- Parsing CSS is super fast and there's no point optimising here. 
- Not specifying image dimensions, which often necessitates reflow, repaint and re-compose. 


- Time to Interactive
- First Meaningful Paint
- Fist Contentful Paint

LEFT OFF AT RENDER