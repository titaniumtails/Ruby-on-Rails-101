# Server Request-Response handling

Whereas `http-server` gives you the requested files (e.g. the local files, it gets the specific files and folders). It's dumb. Everything is visible via the public folder.  First, the web server will look inside the projects public directory, for any file whose path name exactly match the request that came in. If it finds that file, we will return that file to the browser, and never access the rails framework. That makes sense. There's no reason to use the framework when the request is for a self contained, static HTML page or image. And it really speeds things up when the server is gathering images, style sheets, or other static assets to send back to the browser. It makes page loads as quick as possible. It will satisfy the request within the public directory before it goes to the rails framework. Image assets also can be placed here so it doesn't have to bother the Rails framework, and be loaded quickly as possible.

But, whenever the web server doesn't find the matching file, next, it ask the Rails Framework to handle the request. The request goes to Rails **routing**.  Its about Routes. Routing parses the url to determine which controller and action to use. It will then execute the controller action. Make request to the Model as needed and then finally render our View, just like we saw with the MVC architecture.


![MVC Rails in Detail](https://www.dropbox.com/s/igh8ow0ejl93vu1/MVC%20Rails%20in%20detail.tiff "MVC Rails in detail")
