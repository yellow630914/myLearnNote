# Learn Node.Js



## Modules

代表宣告一個node.js的http模塊

`var http = require('http');`  

宣告模塊後,創造一個Server,在本地8080回傳"Hello World!"

`http.createServer(function (req, res) {
 	res.writeHead(200, {'Content-Type': 'text/html'});
 	res.end('Hello World!');
}).listen(8080);`

***

創造一個內容如下的js檔案,並命名為myModule.js 

`exports.myDateTime = function () {
 	return Date();
};`

接著在app.js中宣告自己的模塊

`var myModule = require('./myModule'); `

然後就可以在app中調用myModule中的函式了,如:

`http.createServer(function (req, res) {
 	res.writeHead(200, {'Content-Type': 'text/html'});
 	res.write("The date and time are currently: " + myModule.myDateTime());
 	res.end();
}).listen(8080);`





## HTTP Module











