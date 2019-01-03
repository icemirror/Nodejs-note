## Your first nodejs

- 创建一个first.js文件: 

```
> cd ~/desktop
> touch first-node.js
> vi first-node.js
```
- 向first-node.js中写入如下的代码:
```
// 引入http模块
const http = require('http');

// 定义域名hostname和端口号
const hostname = '127.0.0.1'
const port = 2333

// 创建一个http server
http.createServer((req, res) => {
  // 设置状态码
  res.statusCode = 200
  // 设置请求头
  res.setHeader('Content-Type', 'text/plain')
  // 请求响应的数据
  res.end('Hello World\n')
}).listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
})
```
- 运行:

```
> node first-node.js
```
此时, 用浏览器打开 ```http://127.0.0.1:2333```, 就可以看到"Hello World".