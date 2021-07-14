# Learn Node.Js



## Modules

代表宣告一個node.js的http模塊

```javascript
var http = require('http');
```

var http = require('http');

宣告模塊後,創造一個Server,在本地8080回傳"Hello World!"

```javascript
http.createServer(function (req, res) {
 	res.writeHead(200, {'Content-Type': 'text/html'});
 	res.end('Hello World!');
}).listen(8080);
```

***

創造一個內容如下的js檔案,並命名為myModule.js 

```javascript
exports.myDateTime = function () {
 	return Date();
};
```

接著在app.js中宣告自己的模塊

```javascript
var myModule = require('./myModule'); 
```

然後就可以在app中調用myModule中的函式了,如:

```javascript
http.createServer(function (req, res) {
 	res.writeHead(200, {'Content-Type': 'text/html'});
 	res.write("The date and time are currently: " + myModule.myDateTime());
 	res.end();
}).listen(8080);
```

***



## HTTP Module

```javascript
res.writeHead(200, {'Content-Type' : 'text/html'})
```



此行代碼指http標頭,200一切正常

```javascript
res.writeHead(200, {'Content-Type' : 'text/html'})
```



此行代碼會顯示客戶端的`url`,`req`是客戶端的請求,而`url`是客戶端域名後的部分網址,如:`http://localhost:8080/summer`中的 `/summer`就是`req.url`的部分



***



## File System Module

File System是node.js內建的模塊,可用`var fs = require('fs')`來宣告,fs中有`readFile()`方法可以讀取檔案並回傳function

```javascript
var http = require('http');
var fs = require('fs');

http.createServer(function (req, res) {
  fs.readFile('demofile1.html', function(err, data) {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);
    return res.end();
  });
}).listen(port);
```

`fs.appenedFile()`方法可以將指定內容加入文件,若文件不存在則創建文件,第一個參數是文件名,第二個是插入的內容,第三個則是回傳的function,內容將會添加到文件的末尾,如:

```javascript
fs.appendFile('mynewfile1.txt', 'Hello content!', function (err) {
  if (err) throw err;
  console.log('Saved!');
});
```

`fs.open()`在第二個參數為`'w'`時代表寫入,指打開指定文件寫入,若文件不存在,則創建文件,如:

```javascript
fs.open('mynewfile2.txt', 'w', function (err, file) {
  if (err) throw err;
  console.log('Saved!');
});
```

`fs.writeFile()`方法可替換文件與內容,若不存在則創建文件,如:

```javascript
fs.writeFile('mynewfile3.txt', 'Hello content!', function (err) {
  if (err) throw err;
  console.log('Saved!');
});
```

`fs.unlink()`可以刪除文件,如:

```javascript
fs.unlink('mynewfile2.txt', function (err) {
  if (err) throw err;
  console.log('File deleted!');
});
```

`fs.rename`可以將文件重新命名,以第二個參數取代第一個參數,如:

```javascript
fs.rename('mynewfile1.txt', 'myrenamedfile.txt', function (err) {
  if (err) throw err;
  console.log('File Renamed!');
});
```



***



## URL Module

`url`也是一個node.js的建模塊,可用於分析操作網址,可用`var url = require('url')`宣告為url模塊,其中`url.parse()`可解析網址,分出網址中的各屬性,如:

```javascript
var url = require('url');
var adr = 'http://localhost:1337/default.htm?year=2017&month=february';  //此為範例網址
var q = url.parse(adr, true);  //第一個參數為網址,第二個決定是否處理查詢字串

console.log(q.host); //回傳 'localhost:1337' 部分
console.log(q.pathname); //回傳 '/default.htm' 部分
console.log(q.search); //回傳 '?year=2017&month=february' 部分

var qdata = q.query; //回傳一個物件: { year: 2017, month: 'february' }
console.log(qdata.month); //回傳物件中的month屬性 'february'
```

接著可以配合`fs`模塊將網頁導流至想要的文件,如:

```javascript
var http = require('http');
var url = require('url');
var fs = require('fs');

http.createServer(function (req, res) {
  var q = url.parse(req.url, true);     //先解析網址
  var filename = "./html" + q.pathname;   //將網址的pathname指向filename
  fs.readFile(filename, function(err, data) {   //讀取filename並指定特定文件為網頁
    if (err) {               //如果出錯則呈現此頁面
      res.writeHead(404, {'Content-Type': 'text/html'});
      return res.end("404 Not Found");
    } 
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write(data);         //如果成功則呈現文件
    return res.end();
  });
}).listen(port);
```



***



## EVENT

node.js中也可觸發事件,例如creatStream是在檔案開關時觸發的事件,如:

```javascript
var fs = require('fs');
var rs = fs.createReadStream('./demofile.txt');    //宣告rs為demofile.txt的事件obeject
rs.on('open', function () {         //當文件開啟時執行function
  console.log('The file is open');
});
```

node.js也有一個`event`模塊,在其中妳可以創建自己的事件,如:

```javascript
var events = require('events');     //require event模塊
var eventEmitter = new events.EventEmitter();   //EventEmitter是一種觸發器

//創造一個觸發時執行程序
var myEventHandler = function () {
  console.log('I hear a scream!');
}

//將一個觸發器命名為scream,並與觸發程序連接
eventEmitter.on('scream', myEventHandler);

//觸發scream事件
eventEmitter.emit('scream');

```









