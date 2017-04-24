### node 学习总结

### 目录

* [**node安装**](#node安装)
* [**第一个demo**](#第一个demo)
* [**nodeAPI**](#node接口)
	*  [**assert**](#assert)
	*  [**HTTP**](#HTTP)
	*  [**HTTPS**](#HTTPS)
	

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
```node
> url.parse('https://github.com/Front-end-engineer-load/node/blob/master/README.
md#node%E6%8E%A5%E5%8F%A3')
Url {
  protocol: 'https:',
  slashes: true,
  auth: null,
  host: 'github.com',
  port: null,
  hostname: 'github.com',
  hash: '#node%E6%8E%A5%E5%8F%A3',
  search: null,
  query: null,
  pathname: '/Front-end-engineer-load/node/blob/master/README.md',
  path: '/Front-end-engineer-load/node/blob/master/README.md',
  href: 'https://github.com/Front-end-engineer-load/node/blob/master/README.md#n
ode%E6%8E%A5%E5%8F%A3' }
```
这就是API的使用接下来我们就过一遍node的全部API。
学习文档node.js v6.10.2文档

### assert

	assert(断言) 模块提供了一组简单的断言测试集合，可被用于测试不变量。

* assert(value,[,message])
	
	assert.ok() 的别名 

```node
const assert =require('assert');

assert('10');

assert(true);
assert(1);
//assert(false);
assert(0);

assert('10');
//assert(false,'不是真值');
//报错如下

assert.js:85
  throw new assert.AssertionError({
  ^
AssertionError: 0 == true
    at Object.<anonymous> (D:\node-demo\node-demo1\assert.js:8:1)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)
    at Function.Module._load (module.js:438:3)
    at Module.runMain (module.js:604:10)
    at run (bootstrap_node.js:394:7)
    at startup (bootstrap_node.js:149:9)
    at bootstrap_node.js:509:3

```
关于这个API 感觉像是前面定义一个 true 后面如果不是出现了变化就会报错 还可以接受一个参数提示出来
不知道这个的作用

* assert.deepEqual(actual,expected[',message'])

测试 actual 参数与 expected 参数是否深度相等。 原始值使用相等运算符（==）比较。

只比较可枚举的自身属性。 deepEqual() 不比较对象的原型、连接符、或不可枚举的属性。 这可能会导致一些意料之外的结果。 例如，下面的例子不会抛出 AssertionError，因为 Error 对象的属性是不可枚举的：

		// 注意：这不会抛出 AssertionError！
		assert.deepEqual(Error('a'), Error('b'));

```node
const assert =require('assert');
const obj1={
	a:{
		b:1
	}
}
const obj2={
	a:{
		b:2
	}
}
const obj3={
	a:{
		b:1
	}
}
const obj4=Object.create(obj1);
assert.deepEqual(obj1,obj1,'相同的object是相同的吗');
//相同
assert.deepEqual(obj1,obj2,'obj1和obj2是相同的吗');
//不相同，因为里面的值不相等
assert.deepEqual(obj1,obj3,'obj1和obj3是相同的吗');
//相等
assert.deepEqual(obj1,obj4,'obj1和obj4是相同的吗');
//不相等 原型被忽略了
```
* assert.deepStrictEqual(actual,expected[,message])

大多数情况下与 assert.deepEqual() 一样，但有两个例外。 首先，原始值使用全等运算符（===）比较。 其次，对象的比较包括检查它们的原型是否全等。

```node
const assert = require('assert');
assert.deepEqual({a:1}, {a:'1'});
// 通过，因为 1 == '1'
assert.deepStrictEqual({a:1}, {a:'1'});
// 抛出 AssertionError: { a: 1 } deepStrictEqual { a: '1' }
// 因为 1 !== '1' 使用全等运算符
//接着上面的例子 
const obj4=Object.create(obj1);
const obj5=Object.create(obj1);
assert.deepEqual(obj1,obj1,'相同的object是相同的吗');
//相同
assert.deepStrictEqual(obj1,obj3,'deepStrictEqual，obj1和obj2是相同的吗');
//通过了  
assert.deepStrictEqual(obj5,obj4,'deepStrictEqual，obj1和obj4是相同的吗');
//通过

```
感觉就是检测两个值是不是相等

* assert.doesNotThrow(block[, error][, message])

	断言 `block` 函数不会抛出错误。

### HTTP

使用http服务器和客户端必须require（'http'）

Node.js 中的 HTTP 接口被设计为支持以往较难使用的协议的许多特性。 比如，大块编码的消息。 该接口从不缓存整个请求或响应，所以用户能够流化数据。

HTTP 消息头由类似以下的对象表示：

```javascript
{ 'content-length': '123',
  'content-type': 'text/plain',
  'connection': 'keep-alive',
  'host': 'mysite.com',
  'accept': '*/*' }
```
键名是小写的，值是不能修改的。

为了支持全部可能的 HTTP 应用，Node.js 的 HTTP API 是非常底层的。 它只涉及流处理和消息解析。 它把一个消息解析成头部和主体，但它不解析具体的头部或主体。

`收到的原始消息头`保存在 `rawHeaders` 属性中，它是一个 [key, value, key2, value2, ...] 的数组。 例如，上面的消息头对象可能有一个类似以下的 rawHeaders 列表：

```javascript
[ 'ConTent-Length', '123456',
  'content-LENGTH', '123',
  'content-type', 'text/plain',
  'CONNECTION', 'keep-alive',
  'Host', 'mysite.com',
  'accepT', '*/*' ]
```


