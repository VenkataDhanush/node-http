node http

1.create nodeJs folder
2.create node-http sub folder
3.create public sub folder
4. in cmd in node-http === npm init
5.in package.json
{
  "name": "node-http",
  "version": "1.0.0",
  "description": "Node HTTP Module Example",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index"
  },
  "author": "dhanush",
  "license": "ISC"
}
6.create index.js
const http = require('http');

const hostname= 'localhost';
const port = 3000;

SERVING HTML FILE

7. in public folder create index.html

<html>
<title>This is index.html</title>
<body>
<h1>Index.html</h1>
<p>This is the contents of this file</p>
</body>
</html>

8. in public folder create abouts.html

<html>
<title>This is aboutus.html</title>
<body>
<h1>Aboutus.html</h1>
<p>This is the contents of the aboutus.html file</p>
</body>
</html>

9.update index.js

. . .

const fs = require('fs');
const path = require('path');

. . .

const server = http.createServer((req, res) => {
  console.log('Request for ' + req.url + ' by method ' + req.method);

  if (req.method == 'GET') {
    var fileUrl;
    if (req.url == '/') fileUrl = '/index.html';
    else fileUrl = req.url;

    var filePath = path.resolve('./public'+fileUrl);
    const fileExt = path.extname(filePath);
    if (fileExt == '.html') {
      fs.exists(filePath, (exists) => {
        if (!exists) {
          res.statusCode = 404;
          res.setHeader('Content-Type', 'text/html');
          res.end('<html><body><h1>Error 404: ' + fileUrl + 
                      ' not found</h1></body></html>');
          return;
        }
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        fs.createReadStream(filePath).pipe(res);
      });
    }
    else {
      res.statusCode = 404;
      res.setHeader('Content-Type', 'text/html');
      res.end('<html><body><h1>Error 404: ' + fileUrl + 
              ' not a HTML file</h1></body></html>');
    }
  }
  else {
      res.statusCode = 404;
      res.setHeader('Content-Type', 'text/html');
      res.end('<html><body><h1>Error 404: ' + req.method + 
              ' not supported</h1></body></html>');
  }
})

. . .
const server=http.createServer((req,res) =>{
    console.log(req.headers);

    res.statusCode= 200;
    res.setHeader('Content-Type','text/html');
    res.end('<html><body><h1>Hello, World!</h1></body></html>');
})

server.listen(port, hostname, () =>{
    console.log(`Server running at http://${hostname}:${port}`)
})

// to run server === npm start