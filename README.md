### node 学习总结

### 目录

* [**node安装**](#node安装)
* [**第一个demo**](#第一个demo)
* [**nodeAPI**](#node接口)


#### node 安装

本人屌丝一个，故安装只在window下，有朝一日买下Mac，会补上

故：下载node与本机响应版本，傻瓜安装即可

	1. 注意32位还是64位，windows还是其他的系统
	2. 注意安装之后，可以打来cmd 输入node -v 查看安装node版本
	3. 如果node 安装了 蛋死，node -v 不管用 可以去 windows的高级系统设置里面的环境变量里面的path里面添加node的安装路径
	4. node 和 npm  是一起安装的 不用再安装npm（包管理工具）
	5. cmd 使用不习惯可以用 GIT bash 代替  还可以用cmder 等软件，当然激励推荐git

### 第一个demo

* 新建一个文件夹demo 里面新建一个index.js
* 打开index.js文件 编写下面的内容

```javascript
//demo1
const http =require('http'); //加载http模块

const hostname='127.0.0.1'; //host域名

const port =8080; // 端口  
const server = http.createServer((req,res)=>{
	res.ststusCode=200;
	res.setHeader('content-Type','text/plain');
	res.end('hello ,node\n');
})

server.listen(port,hostname,()=>{
	console.log(`服务器运行在 http:// ${hostname} : ${port} 之上`); 
})

``` 

```javascript
//demo2
var http=require('http');

http.createServer(function(req,res){
	res.writeHead('200', {'content-type': 'text/plain'});
	res.write('hello my name is mps');
	res.end('okay');
}).listen('1338','127.0.0.1');

console.log('success!');
```

* 然后在demo文件夹里面 点击右键 选择git bash here 
* 然后 执行 node index.js 会看到console的内容
* 打开网页，输入127.0.0.1：响应端口就可以展示相应文字

这两种方式都可以得到同样的结果

	1.第一个demo console.log();里面为了让变量得以解析，采用了 ` 这个标示 就是在tab上面的那个键

### node接口

node提供的这些API比如url 可以在 git里面输入node 回车之后输入url 查看相关参数

```node
> url
{ parse: [Function: urlParse],
  resolve: [Function: urlResolve],
  resolveObject: [Function: urlResolveObject],
  format: [Function: urlFormat],
  Url: [Function: Url] }

```
