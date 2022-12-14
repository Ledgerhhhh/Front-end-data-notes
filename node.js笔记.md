# node.js笔记
## 回顾与思考
浏览器中的JavaScript的组成部分

<img src='img/回顾与思考1.jpg'>


思考:为什么JavaScript可以操作DOM 和BOM
每个浏览器都内置了DOM、BOM这样的API函数，因此，浏览器中的JavaScript 才可以调用它们.

<img src='img/回顾与思考2.jpg'>

浏览器中的JavaScript运行环境
运行环境指的是代码正常运行所需要的必要环境(解析引擎和内置API不可或缺)

<img src='img/回顾与思考3.jpg'>

tip：
1.v8引擎负责解析和执行JavaScript代码
2.内置API是由运行环境提供的特殊接口，只能在所属的环境中被调用

JavaScript 能否做后端开发
可以！使用node.js

##  Node.js简介
```html
1.什么是Node.js
Node.jsRis a JavaScript runtime built on Chrome's V8 JavaScript engine.
Node.js 是一个基于Chrome V8引擎的JavaScript运行环境。(非浏览器)
2.Node.js 中的JavaScript运行环境
注意:
1.浏览器是JavaScript的前端运行环境。
2.Node.,js 是 JavaScript 的后端运行环境。
3.Node.js 中无法调用DOM和BOM等浏览器内置API。

```
<img src='img/node.js运行环境.jpg'>

## Node.js 环境的安装
```
如果希望通过Node.js 来运行Javascript代码，则必须在计算机上安装Node.js环境才行。
安装包可以从Node.js的官网首页直接下载，进入到Node.js的官网首页(https://nodejs.org/en/)，点击绿色的按钮，下载所需的版本后，双击直接安装即可。

1.区分LTS版本和Current版本的不同
LTS为长期稳定版，对于追求稳定性的企业级项目来说，推荐安装LTS版本的Node.js。
Current为新特性尝鲜版，对热衷于尝试新特性的用户来说，推荐安装Current版本的 Node.js。但是，Current版本中可
能存在隐藏的Bug 或安全性漏洞，因此不推荐在企业级项目中使用Current版本的Node.js.

2.查看已安装的Node.js的版本号
打开终端，在终端输入命令node -v后，按下回车键，即可查看已安装的Node.,js的版本号。
Windows系统快速打开终端的方式:
使用快捷键(Windows徽标键＋R)打开运行面板，输入cmd后直接回车，即可打开终端。

3.什么是终端
终端(英文: Terminal)是专门为开发人员设计的，用于实现人机交互的一种方式。
作为一名合格的程序员，我们有必要识记一些常用的终端命令，来辅助我们更好的操作与使用计算机。

4在Node.js环境中执行JavaScript代码
4.1
打开终端(win+r输入cmd)
输入cd <路径>
输入node <js文件名>

4.2
打开终端(在要运行的js文件夹中，长按shift不放，然后左键点击在此处打开powershell窗口)
输入node <js文件名>

1.终端中的快捷键

在Windows的powershell或cmd终端中，我们可以通过如下快捷键，来提高终端的操作效率:

1.使用↑键，可以快速定位到上一次执行的命令
2.使用tab键,能够快速补全路径
3.使用esc健，可以快速清空当前终端的内容
4.输入cls，可以快速清除终端

```
## 什么是fs 文件系统模块
```html
fs模块是Node.js官方提供的、用来操作文件的模块。它提供了一系列的方法和属性，用来满足用户对文件的操作需求。例如:
fs.readFile()方法，用来读取指定文件中的内容fs.writeFile()方法，用来向指定的文件中写入内容
如果要在JavaScript 代码中，使用fs模块来操作文件，则需要使用如下的方式先导入它:
const fs=require('fs')

```
## 读取指定文件内容
```html
fs.readFile()的语法格式
<script>
fs.readFile(path[,options],callback)
</script>

参数解读:
参数1:必选参数，字符串，表示文件的路径。
参数2:可选参数，表示以什么编码格式来读取文件。
参数3:必选参数，文件读取完成后，通过回调函数拿到读取的结果。

<script>
    //1.导入fs模块，来操作文件
const fs = require('fs');

//2.调用fs.readFile()方法来读取文件
//参数1：读取文件读取路径
//参数2：读取文件是采用的编码格式
//参数3：回调函数，拿到读取失败和成功的结果 err dataStr
fs.readFile('./files/1.txt', 'utf8', function(err, dataStr) {
    //打印的结果
    //读取成功 则err的值为null dataStr为执行读取
    //读取失败则 err的值为错误对象 dataStr的值为undefined
    console.log(err);
    console.log('----------');
    console.log(dataStr);
})
</script>
```
## 向指定的文件写入内容
```html
1. fs.writeFile()的语法格式
使用fs.writeFile(方法，可以向指定的文件中写入内容，语法格式如下:

fs.writeFile(file, data[,options], callback)

参数解读:
参数1:必选参数，需要指定一个文件路径的字符串，表示文件的存放路径。
参数2:必选参数，表示要写入的内容。
参数3:可选参数，表示以什么格式写入文件内容，默认值是utf8。
参数4:必选参数，文件写入完成后的回调函数。

<script>
const fs = require('fs')
//调用fs.writrFile()方法，写入文件内容
//参数1：表示文件存放路径
//参数2：表示要写入的内容
//参数3：回调函数
fs.writeFile('./files/1.txt', '我是帅哥', function(err) {
    //如果写入成功，则err为null
    //如果写入失败，则err为一个 错误对象
    console.log(err);
})</script>
```
## 案例写入考试成绩到另一个文件
```html
<script>
    const fs = require('fs')
    fs.readFile('./files/成绩.txt', 'utf8', function(err, dataStr) {
    if (err) {
        return console.log(err);
    }
    // console.log('读取文件成功' + dataStr);
    let arrold = dataStr.split(' ');
    let arr0 = [];
    arrold.forEach(item => {
        arr0.push(item.replace('=', ':'))
    });
    let newstr = arr0.join('\n');
    console.log(newstr);
    fs.writeFile('./files/成绩ok.txt', newstr, function(err) {
        if (err) {
            return err
        }
        console.log('写入成功');
    })
})</script>
```
## fs-处理路径问题
```html
在使用fs模块操作文件时，如果提供的操作路径是以/或../开头的相对路径时，很容易出现路径动态拼接错误的问题。
原因:代码在运行的时候，会以执行node命令时所处的目录，动态拼接出被操作文件的完整路径.

解决方案:在使用fs模块操作文件时，直接提供完整的路径，不要提供/或../开头的相对路径，从而防止路径动态拼接的问题
1.提供绝对路径
<script>
    const fs = require('fs')
    //绝对路径移植性非常差，不利于维护
    fs.readFile('C:\\Users\\ASUS\\Desktop\\node.js\\files\\1.txt', 'utf8', (err, dataStr) => {
    if (err) {
        return alert(err)
    }
    console.log(dataStr);
})
</script>
2.使用__dirname
<script>
    console.log(__dirname);
    const fs = require('fs')
    //__dirname表示当前文件所处的目录
    fs.readFile(__dirname + '/files/1.txt', 'utf8', (err, dataStr) => {
    if (err) {
        return alert(err);
    }
    console.log(dataStr);
})
</script>
```
## 什么是path路径模块
```html
path模块是Node,js 官方提供的、用来处理路径的模块。它提供了一系列的方法和属性，用来满足用户对路径的处理需求
例如:
path.join(方法，用来将多个路径片段拼接成一个完整的路径字符串path.basename(方法，用来从路径字符串中，将文件名解析出来
下
如果要在JavaScript 代码中，使用path模块来处理路径，则需要使用如下的方式先导入它:
<script>
const path = require('path')
</script>

2. path.join()的代码示例
使用path.join())方法，可以把多个路径片段拼接为完整的路径字符串:
<script>
    const pathStr = path.join( '/a','/b/c','../','./d','e')
    console.log(pathstr)//输出\a\b\d\e
    const pathStr2 = path.join( __dirname,'./files/1.txt')
    console.log(pathstr2)//输出当前文件所处目录\files\1.txt
</script>

注意:今后凡是涉及到路径拼接的操作，都要使用path.join()方法进行处理。不要直接使用＋进行字符串的拼接。该方法可以自动过滤掉(./)

<script>
console.log(__dirname);
const fs = require('fs')
const path = require('path')
    //__dirname表示当前文件所处的目录
fs.readFile(path.join(__dirname, './files/1.txt'), 'utf8', (err, dataStr) => {
    if (err) {
        return alert(err)
    }
    console.log(dataStr);
})
</script>

3.path.basename()的语法格式
使用path.basename()方法，可以获取路径中的最后一部分，经常通过这个方法获取路径中的文件名，语法格式如下:
<script>
path.basename(path[,ext])
</script>
参数解读:
path (字符串)必选参数，表示一个路径的字符串
ext (字符串)可选参数，表示文件扩展名(加上后返回结果不带该扩展名)
返回:(字符串)表示路径中的最后部分
<script>

const path = require('path');

const pathStr = '/a/aa/aaa/index.html'

const fullName = path.basename(pathStr)
console.log(fullName); //输出index.html

const fullName2 = path.basename(pathStr, '.html')
console.log(fullName2); //输出index
</script>

4.path.extname()的代码示例
使用path.extname(方法，可以获取路径中的扩展名部分:
<script>
const path = require('path')

const pathStr = '/a/aa/aaa/index.html';

console.log(path.extname(pathStr)); //输出.html
</script>
```
## 案例之拆分html(源码)
```html
<script>
    const fs = require('fs');
const path = require('path');

//匹配style的正则表达式
const regStyle = /<style>([\s\S]*)<\/style>/;
//匹配script的正则表达式
const regScript = /<script>([\s\S]*)<\/script>/;

//处理css
function resolveCSS(htmlStr) {
    const newCSS = regStyle.exec(htmlStr)[1];
    fs.writeFile(path.join(__dirname, './拆分文件/index.css'), newCSS, (err) => {
        if (err) {
            console.log('写入css失败');
        }
        console.log('写入css成功');
    })
}
//处理js
function resolveScript(htmlStr) {
    const newScript = regScript.exec(htmlStr)[1];
    fs.writeFile(path.join(__dirname, './拆分文件/index.js'), newScript, (err) => {
        if (err) {
            return console.log('写入js失败');
        }
        console.log('写入js成功');
    })
}
//处理html文件
function resolveHTML(htmlStr) {
    newHtml = htmlStr.replace(regStyle.exec(htmlStr)[0], '<link rel="StyleSheet" href="./index.css" />').replace(regScript.exec(htmlStr)[0], '<script src="./index.js"></script>');
    fs.writeFile(path.join(__dirname, './拆分文件/index.html'), newHtml, (err) => {
        if (err) {
            return console.log('写入html失败');
        }
        console.log('写入html成功');
    })
}
fs.readFile(path.join(__dirname, './拆分文件/index.html'), 'utf8', (err, dataStr) => {
    if (err) {
        return console.log('读取文件失败');
    }
    // console.log(dataStr);
    resolveCSS(dataStr);
    resolveScript(dataStr);
    resolveHTML(dataStr);
})
</script>

案例的两个注意点
1.fs.writeFile()方法只能用来创建文件，不能用来创建路径(不会新建一个文件夹放入指定文件，而是报错)
2.重复调用fs.writeFile(写入同一个文件，新写入的内容会覆盖之前的旧内容)

```
## 什么是http模块
```html
回顾:什么是客户端、什么是服务器?
在网络节点中，负责消费资源的电脑，叫做客户端;负责对外提供网络资源的电脑，叫做服务器。

http模块是Node.js官方提供的、用来创建web服务器的模块。通过 http模块提供的 http.createServer()方法，就能方便的把一台普通的电脑，变成一台Web服务器，从而对外提供Web资源服务。

如果要希望使用http模块创建Web 服务器，则需要先导入它:
<script>
const http = require("http")
</script>

```
## 服务器相关概念
```html
1.IР地址
IP地址就是互联网上每台计算机的唯一地址，因此IP地址具有唯一性。如果把“个人电脑”比作“一台电话”，那么“IP地址”就相当于“电话号码”，只有在知道对方IP地址的前提下，才能与对应的电脑之间进行数据通信。
IP地址的格式:通常用“点分十进制”表示成(a.b.c.d)的形式，其中，ab,c,d都是0~255之间的十进制整数。例如:用点分十进表示的IP地址(192.168.1.1)

注意:
互联网中每台Web服务器，都有自己的IP地址，例如:大家可以在Windows的终端中运行ping www.baidu.com命令，即可查看到百度服务器的IP地址。
在开发期间，自己的电脑既是一台服务器，也是一个客户端，为了方便测试，可以在自己的浏览器中输入127.0.0.1这个IP地址，就能把自己的电脑当做一台服务器进行访问了。

2.域名和域名服务器
尽管IРP地址能够唯一地标记网络上的计算机，但IP地址是一长串数字，不直观，而且不便于记忆，于是人们又发明了另一套字符型的地址方案，即所谓的域名(Domain Name)地址。
IP地址和域名是一—对应的关系，这份对应关系存放在一种叫做域名服务器(DNS，Domain name server)的电脑中。使用者只需通过好记的域名访问对应的服务器即可，对应的转换工作由域名服务器实现。因此，域名服务器就是提供IР地址和域名之间的转换服务的服务器。

注意:
单纯使用IP地址，互联网中的电脑也能够正常工作。但是有了域名的加持，能让互联网的世界变得更加方便。
在开发测试期间，127.0.0.1对应的域名是localhost，它们都代表我们自己的这台电脑，在使用效果上没有任何区别。

3.端口号
计算机中的端口号，就好像是现实生活中的门牌号一样。通过门牌号，外卖小哥可以在整栋大楼众多的房间中，准确把外卖送到你的手中。
同样的道理，在一台电脑中，可以运行成百上千个web服务。每个web服务都对应一个唯一的端口号。客户端发送过来的网络请求，通过端口号，可以被准确地交给对应的 web服务进行处理。

注意:
每个端口号不能同时被多个web服务占用。②在实际应用中，URL中的80端口可以被省略。

```
## 创建最基本的web服务器
```html
步骤1–导入http模块
如果希望在自己的电脑上创建一个web服务器，从而对外提供web 服务，则需要导入http模块:
<script>
    const http = require('http')
</script>

步骤2–创建web 服务器实例
调用http.createServer()方法，即可快速创建一个web 服务器实例:
<script>
    const server =http.createServer()
</script>

步骤3–为服务器实例绑定request事件
为服务器实例绑定request事件，即可监听客户端发送过来的网络请求:
<script>
    //使用服务器实例的.on()方法，为服务器绑定一个request事件，监听客户的请求
    server.on( "request", (req, res) => {
    //只要有客户端来请求我们自己的服务器，就会触发request 事件，从而调用这个事件处理函数
    console.log( 'Someone visit our web server.')
 })
</script>

步骤4–启动服务器
调用服务器实例的.listen(方法，即可启动当前的web 服务器实例:
<script>
//调用server.listen(端口号，cb回调）方法，即可启动 web服务器
server.listen(80，() => {
console.log('http server running at http://127.0.0.1')
})
</script>
注意：ctrl+c可以停止服务器
```
## req请求对象，res相应对象

```html
res请求对象
只要服务器接收到了客户端的请求，就会调用通过server.on()为服务器绑定的 request事件处理函数。如果想在事件处理函数中，访问与客户端相关的数据或属性，可以使用如下的方式:

res响应对象
在服务器的request事件处理函数中，如果想访问与服务器相关的数据或属性，可以使用如下的方式:

<script>
    const http = require('http')

    const serve = http.createServer();

    serve.on('request', (req,res) => {
    //req 是请求对象，他包含了与客户端相关的数据和属性
    //reg.url 是客户端请求的url地址(只有IP地址后面的字符)
    //req.method 是客户端的method请求类型
    const url = req.url;
    const method = req.method;
    const str = `Your request url is ${url},and request method is ${method}`
    console.log(str);
    //调用res.end方法，向客户端相应一些内容
    res.end(str)
})

    serve.listen(50, () => {
    console.log('server running at http://127.0.0.1:50');
})
    </script>
```
## 解决中文乱码问题
```html
当调用res.end()方法，向客户端发送中文内容的时候，会出现乱码问题，此时，需要手动设置内容的编码格式:
<script>
 serve.on('request', (req,res) => {
    const url = req.url;
    const method = req.method;
    const str = `请求地址是 ${url},请求方式是 ${method}`
    //调用res.setHeader('Content-Type','text/html;chartset=utf-8')这是固定格式
    res.setHeader('Content-Type', 'text/html; charset=utf-8');
    res.end(str)
})
    </script>

```

## 根据不同的url响应不同的html内容
```html
核心实现步骤
1.获取请求的url地址
2.设置默认的响应内容为404 Not found判断用户请求的是否为/或/index.html首页
3.判断用户请求的是否为/about.html关于页面
4.设置Content-Type响应头，防止中文乱码
5.使用res.end(把内容响应给客户端)
<script>
const http = require('http');
const server = http.createServer();
server.on('request', (req, res) => {
    const url = req.url;
    let content = '<h1>404 Not Found?</h1>';
    if (url === '/' || url === '/index.html') {
        content = '<h1>首页</h1>'
    } else if (url === '/about.html') {
        content = '<h1>关于</h1>'
    }
    res.setHeader('Content-Type', 'text/html; charset=utf-8');
    res.end(content);
});
server.listen(50, () => {
    console.log('server running http://127.0.0.1:50');
})
    </script>
```

## 4.6案例–实现网页的web服务器

<img src='img/网页web服务器的核心思路.jpg'>

```html
实现步骤
1.导入需要的模块
2.创建基本的web 服务器
3.将资源的请求url地址映射为文件的存放路径
4.读取文件内容并响应给客户端
5.优化资源的请求路径
<script>
    const http = require('http');
    const fs = require('fs');
    const path = require('path');

    const server = http.createServer();

server.on('request', (req, res) => {
    const url = req.url;
    // let fpath = path.join(__dirname, url);
    //优化路径
    let fpath = '';
    if (url === '/') {
        //127.0.0.1:50直接进入
        fpath = path.join(__dirname, '/click/index.html');
    } else {
        //127.0.0.1:50/index.html直接进入
        fpath = path.join(__dirname, '/click', url);
    }
    fs.readFile(fpath, 'utf8', (err, dataStr) => {
        if (err) {
            return res.end('404 not found');
        }
        res.end(dataStr);
    })
})

server.listen(50, () => {
    console.log('server running at http://127.0.0.1:50');
})
    </script>
```

## 模块化
```html
1.什么是模块化
复杂的文件拆分成好几个

2.编程领域中的模块化
编程领域中的模块化，就是遵守固定的规则，把一个大文件拆成独立并互相依赖的多个小模块。

把代码进行模块化拆分的好处:

1.提高了代码的复用性
2.提高了代码的可维护性
3.可以实现按需加载

1.2模块化规范
模块化规范就是对代码进行模块化的拆分与组合时，需要遵守的那些规则。

例如:
●使用什么样的语法格式来引用模块
●在模块中使用什么样的语法格式向外暴露成员

模块化规范的好处:大家都遵守同样的模块化规范写代码，降低了沟通的成本，极大方便了各个模块之间的相互调用，利人利己。

```
## Node.js中的模块化
```html
1 Node.js中模块的分类

Node.js 中根据模块来源的不同，将模块分为了3大类，分别是:
内置模块 (内置模块是由Node.js 官方提供的，例如fs、path、http等)
自定义模块（用户创建的每个.js文件，都是自定义模块)
第三方模块（由第三方开发出来的模块，并非官方提供的内置模块，也不是用户创建的自定义模块，使用前需要先下载)

```
## 加载模块
```html
使用强大的require(方法，可以加载需要的内置模块、用户自定义模块、第三方模块进行使用。例如:
<script>
//加载内置的fs模块
const fs =require('fs')
//加载用户的自定义模块(会立马执行custom.js的所有代码，custom是一个空对象，省略.js的后缀名也可以加载模块)
const custom = require('./custom.js');
//加载第三方模块(关于第三方模块的下载和使用，会在后面的课程中进行专门的讲解)
const moment =require('moment');

```

## Node.js模块作用域
```html
1.什么是模块作用域
和函数作用域类似，在自定义模块中定义的变量、方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域。

作用：防治全局变量污染问题

2.向外共享模块作用域中的成员
module对象
在每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息，打印如下:
Module {
  id: '.',
  path: 'C:\\Users\\ASUS\\Desktop\\node.js',
  exports: {},
  filename: 'C:\\Users\\ASUS\\Desktop\\node.js\\15-演示module对象.js',
  loaded: false,
  children: [],
  paths: [
    'C:\\Users\\ASUS\\Desktop\\node.js\\node_modules',
    'C:\\Users\\ASUS\\Desktop\\node_modules',
    'C:\\Users\\ASUS\\node_modules',
    'C:\\Users\\node_modules',
    'C:\\node_modules'
  ]
}

```
## module.exports对象
```
在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用。
外界用require()方法导入自定义模块时,得到的就是 module.exports所指向的对象。

共享成员时的注意点:
使用require()方法导入模块时，导入的结果，永远以module.exports指向的对象为准。(让module.exports指向一个全新的对象，则之前的属性会被新属性覆盖)

exports对象
由于module.exports 单词写起来比较复杂，为了简化向外共享成员的代码，Node 提供了exports对象。默认情况下，exports和module.exports 指向同一个对象。最终共享的结果，还是以module.exports指向的对象为准。

exports和module.exports的使用误区
时刻谨记,require()模块时，得到的永远是 module.exports指向的对象(简单理解就是两个最开始指向的是同一个对象，如果两者有一个新赋值为一个新对象，则以module.exports指向的对象为主)

注意:为了防止混乱，建议大家不要在同一个模块中同时使用exports和module.exports
```
## Node.js遵循了CommonJS模块化规范
```
CommonJS规定了模块的特性和各模块之间如何相互依赖.
 
CommonJS规定:
每个模块内部，module变量代表当前模块。
module变量是一个对象，它的exports属性(即 module.exports）是对外的接口.加载某个模块，其实是加载该模块的module.exports属性。require()方法用于加载模块。
```
## 包
```
包的来源
1.什么是包
Node.js 中的第三方模块又叫做包。
就像电脑和计算机指的是相同的东西。第三方模块和包指的是同一个概念。只不过叫法不同。

2.从哪里下载包
国外有一家IT公司，叫做npm, Inc.这家公司旗下有一个非常著名的网站: https//www.npmjs.com/，它是全球最大的包共享平台，你可以从这个网站上搜索到任何你需要的包，只要你有足够的耐心!
到目前位置，全球约1100多万的开发人员，通过这个包共享平台，开发并共享了超过120多万个包供我们使用.npm, Inc.公司提供了一个地址为 https/registry.npmjs.orgl的服务器，来对外共享所有的包，我们可以从这个服务器上下载自己所需要的包.

注意:从https://www.npmjs.com/网站上搜索自己所需要的包,从https://registry.npmjs.orgl服务器上下载自己需要的包

3.如何下载包
npm, Inc.公司提供了一个包管理工具，我们可以使用这个包管理工具，从https://registry.npmjs.org/ 服务器把需要的包下载到本地使用。
这个包管理工具的名字叫做Node Package Manager(简称npm包管理工具)，这个包管理工具随着Node.js的安装包一起被安装到了用户的电脑上。
大家可以在终端中执行npm -v命令，来查看自己电脑上所安装的npm包管理工具的版本号:

```
## npm初体验
```html
在项目中安装包的命令
如果想在项目中安装指定名称的包，需要运行如下的命令:
<script>
npm install 包的完整名称
或者
npm i 包的完整名称
</script>

1.初次装包后多了哪些文件
初次装包完成后，在项目文件夹下多一个叫做node_modules的文件夹和package-lock.json的配置文件。
其中:
node_modules 文件夹用来存放所有已安装到项目中的包。require()导入第三方包时，就是从这个目录中查找并加载包。
package-lockjson配置文件用来记录node modules目录下的每一个包的下载信息，例怏包的名字、版本号、下载地址等。

注意:程序员不要手动修改node_modules或 package-lockjson文件中的任何代码，npm包管理工具会自动维护它们.

2.安装指定版本的包
默认情况下，使用npm install 命令安装包的时候，会自动安装最新版本的包。如果需要安装指定版本的包，可以在包名之后，通过@符号指定具体的版本，例如:
<script>
npm install 包的完整名称@1.2.2
或者
npm i 包的完整名称@1.2.2
</script>

3.包的语义化版本规范
包的版本号是以“点分十进制”形式进行定义的，总共有三位数字，例如2.24.0其中每一位数字所代表的的含义如下:
第1位数字:大版本
第2位数字:功能版本第3位数字:Bug修复版本
```
## 包管理配置文件
```
1.npm规定，在项目根目录中，必须提供一个叫做 package.json的包管理配置文件。用来记录与项目有关的一些配置信息。例如:
1.项目的名称、版本号、描述等
2.项目中都用到了哪些包
3.哪些包只在开发期间会用到
4.那些包在开发和部署时都需要用到

注意:今后在项目开发中，一定要把node_modules文件夹，添加到.gitignore忽略文件中。

2.快速创建package.json
npm包管理工具提供了一个快捷命令，可以在执行命令时所处的目录中，快速创建package.json这个包管理配置文件:

<script>
   //作用:在执行命令所处的目录中，快速新建package.json文件
    npm init-y
</script>
注意:
1.上述命令只能在英文的目录下成功运行!所以，项目文件夹的名称一定要使用英文命名，不要使用中文，不能出现空格。
2.运行npm install命令安装包的时候，npm包管理工具会自动把包的名称和版本号，记录到package.json 中。

3.dependencies节点
package.json文性中，有一个dependencies节点。专门用来记录您使用npm install命令安装了哪些包。
长
```

## 一次性安装所有的包
```html
当我们拿到一个剔除了node_modules的项目之后。需要先把所有的包下载到项目中，才能将项目运行起来。否则会报类似于下面的错误:
Error: Cannot find module 'moment'

可以运行npm install命令(或npm i)一次性安装所有的依赖包:
<script>
    npm i
</script>

```
## 卸载包
```html
可以运行npm uninstall 命令，来卸载指定的包:
<script>
    //使用npm uninstall具体的包名来卸载包
    npm uninstall moment
</script>
注意: npm uninstall 命令执行成功后，会把卸载的包，自动从package.json的dependencies 中移除掉。

7.devDependencies节点
如果某些包只在项目开发阶段会用到，在项目上线之后不会用到，则建议把这些包记录到devDependencies节点中。
与之对应的，如果某些包在开发和项目上线之后都需要用到，则建议把这些包记录到dependencies节点中。

您可以使用如下的命令，将包记录到devDependencies节点中:
<script>
    //安装指定的包，并记录到devDependencies节点中(前后顺序不重要)
    npm i 包名 -D
    //注意:上述命令是简写形式。等价于下面完整的写法:
    npm install 包名--save-dev
</script>

```
## 淘宝NPM镜像服务器
```
淘宝在国内搭建了—个服务器，专门把国外官方服务器上的包同步到国内的服务器，然后在国内提供下包的服务。从而极大的提高了下包的速度。

扩展:
镜像(Mirroring)是一种文件存储形式，一个磁盘上的数据在另一个磁盘上存在一个完全相同的副本即为镜像。

切换npm的下包镜像源
下包的镜像源，指的就是下包的服务器地址。

1 # 查看当前的下包镜像源
2 npm config get registry
3 # 将下包的晚像源切换为淘宝镜像源
4 npm config set registry=https://lregistry.npm.taobao.org/
5 # 检查镜像源是否下载成功
6 npm config get registry

nrm
为了更方便的切换下包的镜像源，我们可以安装nrm这个小工具，利用nrm提供的终端命令，可以快速查看和切换下包的镜像源。

1 # 通过npm包管理器，将nrm安装为全局可用的工具
2 npm i nrm -g
3 #查看所有可用的镜像源
4 nrm ls
5#将下包的镜像源切换为taobao镜像
6 nrm use taobao
```
## 包的分类
```html
1.项目包
那些被安装到项目的node_modules目录中的包,都是项目包。
项目包又分为两类。分别是:
开发依赖包（被记录到devDependencies节点中的包，只在开发期间会用到)
核心依赖包（被记录到dependencies节点中的包，在开发期间和项目上线之后都会用到)

<script>
    npm i 包名 -D //开发依赖包（被记录到devDependencies节点中的包)
    npm i 包名 //核心依赖包（被记录到dependencies节点中的包)
</script>

2.全局包

在执行npm install命令时，如果提供了-g参数，则会把包安装为全局包。
全局包会被安装到C\Users\用户目录VAppData\Roaming\npm\node_modules目录下。


npm i 包名-g  #全局安装指定的包
npm uninstall 包名 -g  #卸载全局安装的包

注意:
1.只有工具性质的包，才有全局安装的必要性。因为它们提供了好用的终端命令。
2.判断某个包是否需要全局安装后才能使用，可以参考官方提供的使用说明即可。

3.i5ting_toc

i5ting_toc是一个可以把 md文档转为 html页面的小工具，使用步骤如下:

# 将i5ting toc安装为全局包
npm install -g i5ting toc
# 调用i5ting toc，轻松实现 md转html的功能

```

## 规范的包结构
```
在清楚了包的概念、以及如何下载和使用包之后，接下来，我们深入了解一下包的内部结构。一个规范的包，它的组成结构，必须符合以下3点要求:
1.包必须以单独的目录而存在
2.包的顶级目录下要必须包含package.json这个包管理配置文件
3.package.json 中必须包含name，version，main这三个属性，分别代表包的名字、版本号、包的入口。

```
## 开发自己的包
```html
初始化包的基本结构
新建itheima-tools文件夹，作为包的根目录在itheima-tools文件夹中，新建如下三个文件:
·package.json(包管理配置文件)
·index.js(包的入口文件)
·README.md(包的说明文档)

tip:require()方法导入包的话，只导入包的名称，系统会根据包里的json文件的main属性找到包的入口文件

json:
{
    "name": "yb",
    "version": "1.0.0",
    "main": "index.js",
    "description": "格式化时间,HTMLEscape的功能",
    "keywords": ["yb", "dataFormat", "escape"],
    "license": "ISC"
}
js:
<script>
    function dateFormat(date) {
    const newDate = new Date(date);
    const y = newDate.getFullYear();
    const m = padZero(newDate.getMonth() + 1);
    const d = padZero(newDate.getDate());
    const hh = padZero(newDate.getHours());
    const mm = padZero(newDate.getMinutes());
    const ss = padZero(newDate.getSeconds());
    return `${y}-${m}-${d}  ${hh}:${mm}:${ss}`
}

function padZero(n) {
    n = n > 9 ? n : '0' + n;
    return n
}
//替换特殊字符识别其成为html格式
function HTMLEscape(htmlStr) {
    htmlStr = htmlStr.replace(/<|>|&|"/g, match => {
        switch (match) {
            case '<':
                return '&lt;';
            case '>':
                return '&gt;';
            case '"':
                return '&quot;';
            case '&':
                return '&amp;';
        }
    })
    return htmlStr;
}
</script>
tips：
实际开发中，会把不同功能的js模块放在不同的js中，分别放进dataFormat.js文件和htmlEscape.js文件，再在其内部暴露出来，index.js再去用require()方法引用dataFormat.js文件和htmlEscape.js文件

编写包的说明文档
包根目录中的README.md文件，是包的使用说明文档。通过它，我们可以事先把包的使用说明，以 markdown的格式写出来，方便用户参考。
README文件中具体写什么内容，没有强制性的要求;只要能够清晰地把包的作用、用法、注意事项等描述清楚即可.我们所创建的这个包的README.md文档中，会包含以下6项

内容:
安装方式、导入方式、格式化时间、转义HTML中的特殊字符、还原HTML 中的特殊字符、开源协议

```
README.md:
## 安装
```
npm install mypackage
```
## 导入
```js
const mypackage=require('mypackage')
```
## 格式化时间
```js
//调用dateFormat对时间进行格式化
const date=new Date()
const dtStr=mypackage.dateFormat(date)
//输出结果 2022-05-03 12:03:05
console.log(dtStr)
```
## 转义html中的特殊字符
```js
//输入一个待转换的字符
const str = '<h1>你好</h1>';
//使用HTMLEscape方法进行转换
const newstr = mypackage.HTMLEscape(str);
//输出结果
console.log(newstr);

```
## j还原html中的字符
```js
//输入一个待转换的字符
newstr2 = mypackage.HTMLUnEscape(newstr);
//输出结果
console.log(newstr2);
```
## 开源协议
ISC
 
## 发布包
```
1.注册一个npm账户
2.登录npm账号
npm账号注册完成后，可以在终端中执行npm login命令，依次输入用户名、密码、邮箱后，即可登录成功。
3.把包发布到npm 上
将终端切换到包的根目录之后，运行npm publish 命令，即可将包发布到npm上(注意:包名不能雷同)。
4.删除已发布的包
运行npm unpublish包名 --force命令，即可从npm删除已发布的包。
注意:
1.npm unpublish命令只能删除72小时以内发布的包
2.npm unpublish 删除的包，在24小时内不允许重复发布
3.发布包的时候要慎重，尽量不要往npm上发布没有意义的包!
```
## 优先从缓存中加载
```
模块在第一次加载后会被缓存。这也意味着多次调用require()不会导致模块的代码被执行多次。
注意:不论是内置模块、用户自定义模块、还是第三方模块，它们都会优先从缓存中加载，从而提高模块的加载效率。

内置模块是由Node.js官方提供的模块，内置模块的加载优先级最高。
例如，require('fs')始终返回内置的fs模块，即使在node modules目录下有名字相同的包也叫做fs。

自定义模块的加载机制
使用require()加载自定义模块时，必须指定以./或../开头的路径标识符。在加载自定义模块时，如果没有指定./或../这样的路径标识符，则node会把它当作内置模块或第三方模块进行加载。

同时，在使用require()导入自定义模块时，如果省略了文件的扩展名，则 Node.js 会按顺序分别尝试加载以下的文件:
1.按照确切的文件名进行加载
2.补全.js扩展名进行加载
3.补全.json扩展名进行加载
4.补全.node扩展名进行加载
5.加载失败，终端报错
```
## 第三方模块的加载机制
```
如果传递给require()的模块标识符不是一个内置模块，也没有以‘./”或‘./”’开头，则 Node,js会从当前模块的父目录开始。尝试从/node_modules文件夹中加载第三方模块。
如果没有找到对应的第三方模块，则移动到再上一层父目录中，进行加载，直到文件系统的根目录。
例如，假设在'C:\Users\itheima\project\foo.js'文件里调用了require(tools')，则 Node.js 会按以下顺序查找:
C\Users\itheima\project\node_modulestools
C\Users\itheima\node_modules\tools
C\Users\node_modules\tools
C:\node_modules\tools

目录作为模块后
当把目录作为模块标识符，传递给require()进行加载的时候，有三种加载方式:
1.在被加载的目录下查找一个叫做package.json的文件，并寻找 main属性，作为require()加载的入口
2.如果目录里没有package.json文件，或者main 入口不存在或无法解析，则 Node,js将会试图加载目录下的 index.js 文件。
3.如果以上两步都失败了，则Node.js 会在终端打印错误消息，报告模块的缺失:Error.Cannot find module 'xxx'

```
## express
```
1.什么是 Express
官方给出的概念: Express是基于Node.js 平台，快速、开放、极简的Web开发框架。
通俗的理解: Express的作用和Node.js内置的 http模块类似，是专门用来创建Web 服务器的。Express的本质:就是一个npmg上的第三方包，提供了快速创建Web 服务器的便捷方法。
```
[Express的中文官网](http://www.expressjs.com.cn/)

## Express能做什么
```
对于前端程序员来说，最常见的两种服务器，分别是:
·Web 网站服务器:专门对外提供 Web 网页资源的服务器。
·API接口服务器:专门对外提供API接口的服务器。
使用Express，我们可以方便、快速的创建Web网站的服务器或API接口的服务器。
```
## 监听get,post请求
```html
通过app.get()方法，可以监听客户端的GET请求，具体的语法格式如下:
<script>
app.get('请求URL', function(req,res) {/*处理函数*/})
//通过app.post()方法，可以监听客户端的GET请求，具体的语法格式如下:
app.post('请求URL', function(req,res) {/*处理函数*/})
//把内容响应给客户端
</script>
<script>
//通过res.send()方法，可以把处理好的内容，发送给客户端:
app.get('/user', (req. res) =>{
    //向客户端发送JSON对象
res.send({ name: 'zs ', age: 20，gender: '男'})

app.post('/user',(req,res)=>{
    //向客户端发送文本内容
res.send('请求成功')})
</script>

```
## 获取URL中携带的查询参数
```html
通过req.query对象，可以访问到客户端通过查询字符串的形式，发送到服务器的参数:
<script>
app.get('/', (req,res)=>{
    //req.query默认是一个空对象
    //客户端使用name=zs&age=20这种查询字符串形式，发送到服务器的参数,
    //可以通过req.query对象访问到，例如:
    // req.query.name  req.query.age
    console.log(req.query)})
</script>

```
## 获取URL中的动态参数
```html
通过req.params对象，可以访问到URL中，通过:匹配到的动态参数:

<script>
    // URL地址中可以通过:参数名的形式，匹配动态参数值
app.get('/user/:id/:name',(req，res) =>{//id不是固定写法，冒号是固定写法
//req.params默认是一个空对象
//里面存放着通过:动态匹配到的参数值
console.log(req.params)；
res.send(req.params)
//http://127.0.0.1/user/9  res返回Json格式的{id=9,name:'zs'}
})
</script>

```
## express.static()
```html
express提供了一个非常好用的函数，叫做express.static()，通过它，我们可以非常方便地创建一个静态资源服务器
例如，通过如下代码就可以将public目录下的图片、CSS文件、JavaScript 文件对外开放访问了:
<script>
app.use(express.static('public'))

// 现在，你就可以访问public目录中的所有文件了
// http://localhost:3000/images/bg.jpg
// http://localhost:3000/css/style.css
// http://localhost:3000/js/login.js

// 注意:Express在指定的静态目录中查找文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在 URL中。

</script>
```
## 托管多个静态资源目录
```
如果要托管多个静态资源目录，请多次调用express.static()函数:
app.use(express.static('public'))
app.use(express.static('files'))

访问静态资源文件时，express.static()函数会根据目录的添加顺序查找所需的文件。找到了就不会找下一个静态资源目录
```
## 挂载路径前缀
```html
如果希望在托管的静态资源访问路径之前，挂载路径前缀，则可以使用如下的方式:
<script>
app. use('/public',express.static('public'))
</script>
现在，你就可以通过带有/public前缀地址来访问public 目录中的文件了:
http://localhost:3000/public/images/kitten.jpg
http://localhost:3000/public/css/style.css
http://localhost:3000/publicljs/app.js

```
## nodemon
```
使用nodemon
当基于Nodejs编写了一个网站应用的时候,传统的方式，是运行node app.,js命令来启动项目。这样做的坏处是:代码被修改之后，需要手动重启项目。
现在，我们可以将node命令替换为nodemon命令,使用nodemon app.js来启动项目。这样做的好处是:代码被修改之后，会被nodemon 监听到，从而实现自动重启项目的效果。

node app.js
#将上面的终瑞命令，替换为下面的终端命令，即可实现自动重启项目的效果nodemon app.js

```
## Express 中的路由
```html
在Express中，路由指的是客户端的请求与服务器处理函数之间的映射关系。
Express 中的路由分3部分组成，分别是请求的类型、请求的URL地址、处理函数，格式如下:
<script>
    const express = require('express');
    const app = express();
    app.use('/clicks', express.static('./click'));
    app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
})

</script>
```
## 路由的匹配过程
```html
每当一个请求到达服务器之后，需要先经过路由的匹配，只有匹配成功之后，才会调用对应的处理函数。
在匹配时，会按照路由的顺序进行匹配，如果请求类型和请求的URL同时匹配成功，则 Express 会将这次请求，转交给对应的function函数进行处理。

1.最简单的用法(用的不多，代码越多挂载越多，文件体积过大)
在Express 中使用路由最简单的方式，就是把路由挂载到app 上，示例代码如下:
<script>
    app.get('/',(req,res)=>{
        fn()
    })
</script>
```
## 模块化路由
```
为了方便对路由进行模块化的管理，Express 不建议将路由直接挂载到app上，而是推荐将路由抽离为单独的模块。将路由抽离为单独模块的步骤如下:
1.创建路由模块对应的.js 文件
2.调用express.Router()
3.函数创建路由对象向路由对象上挂载具体的路由
4.读用module.exports向外共享路由对象
5.使用app.use()函数注册路由模块
```
## 创建路由模块
```html
<script>
var express = require('express')
//1．导入express
var rcter = express.Router()
//2、创建路由对象,是对象
router.get( '/user/list', function (req,res) 
{ //3．挂载获取用户列表的路由
res.send( 'Get user list.')}
)
router.post('/user/add',function (req，res) 
{//4、挂载添加用户的路由
res.send('Add new user.')}
)
module.exports = router;
//5、向外导出路由对象
</script>

<script>
const express = require('express')
const app = express();
//导入路由
const router = require('./23-模块化路由')
//注册路由
app.use(router)
//app.use函数就是用来注册全局中间件
app.listen(80, () => {
    console.log('express server running at http://127.0.0.1');
})
</script>
```
## 为路由模块添加前缀
```html
类似于托管静态资源时，为静态资源统一挂载访问前缀一样，路由模块添加前缀的方式也非常简单:
<script>
app.use('/api',router)
</script>

```
## Express中间件
```html
Express中间件的调用流程
当一个请求到达Express的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

Express中间件的格式
Express的中间件，本质上就是一个function处理函数，Express中间件的格式如下:
<script>
    app.get('/',(req,res,next)=>{
        next()
    })
</script>
注意:中间件函数的形参列表中，必须包含next 参数。而路由处理函数中只包含req和res,

全局生效的中间件
客户端发起的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件。
通过调用app.use(中间件函数)，即可定义一个全局生效的中间件，示例代码如下:

<script>
const mw = (req, res, next) => {
    console.log('中间件路由');
    next();
}
app.use(mw)//将mv定义成全局中间件(每次发起请求都要经过mv函数处理数据)
</script>
或者
<script>
app.use((req, res, next) => {
    console.log('最简单的中间件函数');
    next();
})//将mv定义成全局中间件(每次发起请求都要经过mv函数处理数据)
</script>

中间件的作用
多个中间件之间，共享同一份req和res。基于这样的特性，我们可以在上游的中间件中，统一为req或res对象添加自定义的属性或方法，供下游的中间件或路由进行使用。

5.定义多个全局中间件
可以使用app.use()连续定义多个全局中间件。客户端请求到达服务器之后，会按照中间件定义的先后顺序依次进行调用，示例代码如下:
<script>
app.use((req, res, next) => {
    console.log('定义第一个中间件');
    next();
})
app.use((req, res, next) => {
    console.log('定义第二个中间件');
    next();
})
</script>

局部生效的中间件
不使用app.use()定义的中间件，叫做局部生效中间件
<script>
const mw = (req, res, next) => {
    console.log('中间件路由');
    next();
}
app.get('/',mw,(req,res)=>{
    res.send('get successfully')
})
</script>

定义多个局部中间件
可以在路由中，通过如下两种等价的方式，使用多个局部中间件:
<script>
app.get('/',mw,mw1,mw2,(req,res)=>{
    res.send('get successfully')
})
//或者是
app.get('/',[mw,mw1,mw2],(req,res)=>{
    res.send('get successfully')
})
</script>
```
## 使用中间件的注意事项
```
·一定要在路由之前注册中间件
·客户端发送过来的请求，可以连续调用多个中间件进行处理
·执行完中间件的业务代码之后，不要忘记调用next()函数
·为了防止代码逻辑混乱，调用next()，函数后不要再写额外的代码
·连续调用多个中间件时，多个中间件之间，共享req和res 对象

```
## 中间件的分类
```html
1.应用级别的中间件
通过app.use()或app.get()或 app.post()，绑定到app实例上的中间件，叫做应用级别的中间件，代码示例如下:

<script>
//应用级别的中间件(全局中间件)
app. use((req. res, next)=>{
next()
})

//应用级别的中间件(局部中间件)
app.get('/',mw1,(req,res) =>{
res.send('Home page.')})
</script>

2.路由级别的中间件
绑定到express.Router()实例上的中间件，叫做路由级别的中间件。它的用法和应用级别中间件没有任何区别。只不过，应用级别中间件是绑定到app实例上，路由级别中间件绑定到router实例上，代码示例如下;
<script>
var app = expresso
var router =express.Router()

router.use((req,res,next)=>{
next()
})

app.use('/',router)
</script>

错误级别的中间件
错误级别中间件的作用:专门用来捕获整个项目中发生的异常错误，从而防止项目异常崩溃的问题。
格式:错误级别中间件的function处理函数中，必须有4个形参，形参顺序从前到后，分别是(err, req, res, next)。
<script>
   
      app.get('/', function (req，res) {
      throw new Error('服务器内部发生了错误!')//路由的报错消息，会传给错误中间件
      res.send('Home Page.')}
    ) 
       //设置错误中间件(一定要在所有路由之后)
        app.use(function (err,req,res,next){
       //错误中间件会收到路由报错然后执行
        console.log('发生了错误:' + err.message)
        res.send( "Error! " + err.message)}
    )

</script>

Express内置的中间件
自Express 4.16.0版本开始，Express 内置了3个常用的中间件，极大的提高了Express项目的开发效率和体骏
·express.static快速托管静态资源的内置中间件，例如:HTML文件、图片、CSS样式等(无兼容性)
·express.json解析JSON格式的请求体数据(有兼容性，仅在4.16.0+版本中可用)
·express.urlencoded解析URL-encoded格式的请求体数据(有兼容性，仅在4.16.0+版本中可用)

tip:postman 里面需要传给服务器数据，选择body>raw>的text中选择json文件格式
<script>
//配置解析applicationljson格式数据的内置中问件
app.use(express.json())
//配置解析application/x-ww-form-urlencoded 格式数据的内置中间件
app.use(express.urlencoded({ extended: false}))
</script>

第三方的中间件
非Express官方内置的，而是由第三方开发出来的中间件，叫做第三方中间件。在项目中，大家可以按需下载并配置第三方中间件，从而提高项目的开发效率。
例如:在express@4.16.0之前的版本中，经常使用body-parser这个第三方中间件，来解析请求体数据。使用步骤如下:
1.运行 npm install body-parser安装中间件
2.使用require 导入中间件
3.调用app.use(注册并使用中间件)
<script>
const express = require("express");
const parser = require('body-parser')
const app = express();
//用法和express()类似
app.use(parser.urlencoded({ extended: false }));
//用法和express()类似
app.use(parser.json());

app.post('/', (req, res) => {
    console.log(req.body);
})
app.listen(80, () => {
    console.log('http://127.0.0.1');
})
</script>
```
## 自定义中间件
```html
1.需求描述与实现步骤
自己手动模拟一个类似于express.urlencoded这样的中间件，来解析POST提交到服务器的表单数据。
实现步骤:
1.定义中间件
2.监听req的 data事件
3.监听req的end 事件
4.使用querystring模块解析请求体数据
5.将解析出来的数据对象挂载为req.body
6.将自定义中间件封装为模块

3.监听req的data 事件
在中间件中，需要监听req对象的data事件，来获取客户端发送到服务器的数据。
如果数据量比较大，无法一次性发送完毕，则客户端会把数据切割后，分批发送到服务器。所以data事件可能会触发多次，每一次触发data 事件时，获取到数据只是完整数据的一部分，需要手动对接收到的数据进行拼接。
<script>
//定义变量，用来存储客户端发送过来的请求体数据
let dataStr = ''
//监听req对象的 data 事件(客户端发送过来的新的请求体数据)
//数据过长，则需要拼接数据字串
req.on( 'data', (chunk) =>{
//拼接请求体数据，隐式转换为字符串
dataStr += chunk
})
</script>

4.监听req的end事件
当请求体数据接收完毕之后，会自动触发req的end事件。
因此，我们可以在req的end事件中，拿到并处理完整的请求体数据。示例代码如下:
<script>
    req.on('end',()=>{
        req.on('end',()=>{
        console.log(dataStr);
    })
    })
</script>
5.使用querystring模块解析请求体数据
Nodejs 内置了一个querystring 模块，专门用来处理查询字符串。通过这个模块提供的parse()函数，可以轻松把查询字符串，解析成对象的格式。示例代码如下:
<script>
//导入处理querystring 的 Node.js内置模块
const qs = require('node:querystring')
//调用qs.parse()方法，把查询字符串解析为对象
const body = qs.parse(str)
</script>
6.将解析出来的数据对象挂载为req.body
上游的中间件和下游的中间件及路由之间，共享同一份req和res。因此，我们可以将解析出来的数据，挂载为req的自定义属性，命名为req.body，供下游使用。示例代码如下:
<script>
req.on('end',()=>{
const body = qs.parse(str)
//调用qs.parse()方法，把查询字符串解析为对象
req.body = body
//将解析出来的请求体对象。挂载为req. body属性
next()
//最后，一定要调用next()函数，执行后续的业务逻辑
//tip!!!!!!next()一定要放在req.end的最后，不然变成异步处理了
})
</script>

7.将自定义中间件封装为模块
为了优化代码的结构，我们可以把自定义的中间件函数，封装为独立的模块，示例代码如下:
<script>
//custom-body-parser.js模块中的代码
const qs = require( " querystring ')
function bodyParser(req,res,next){ /*省略其它代码*/}
module.exports = bodyParser 
//向外导出解析请求体数据的中间件函数
----------------------------------------
//导入自定义的中间件模块
const myBodyParser = require('custom-body-parser')
//注册自定义的中间件模块
app.use(myBodyParser)
</script>
```
## 使用express写接口
```html
<script>
    const express = require('express')
const router = express.Router();

module.exports = {
    router
}
-----------------------------
const express = require('express')

const app = express();
const router = require('./33-用express创建路由模块')
//将路由看成是一个中间件
app.use('/api', router)
app.listen(80, () => {
    console.log('http://127.0.0.1');
})
</script>
```
## 接口的跨域问题
```
刚才编写的GET和POST接口，存在一个很严重的问题:不支持跨域请求。解决接口跨域问题的方案主要有两种:
CORS(主流的解决方案，推荐使用)
JSONP(有缺陷的解决方案:只支持GET请求)

使用cors 中间件解决跨域问题
cors 是 Express的一个第三方中间件。通过安装和配置cors 中间件，可以很方便地解决跨域问题。使用步骤分为如下3步:
1.运行 npm install cors安装中间件
2.使用const cors = require('cors')导入中间件
3.在路由之前调用app.use(cors())配置中间件

什么是CORS
cORS (Cross-Origin Resource Sharing，跨域资源共享）由一系列HTTP响应头组成，这些HTTP响应头决定浏览器是否阻止前端JS代码跨域获取资源。
浏览器的同源安全策略默认会阻止网页“跨域”获取资源。但如果接口服务器配置了CORS相关的 HTTP响应头，就可以解除浏览器端的跨域访问限制。

tips:
1.CORS主要在服务器端进行配置。客户端浏览器无须做任何额外的配置，即可请求开启了CORS的接口。
2.CORS在浏览器中有兼容性。只有支持XMLHttpRequest Level2的浏览器，才能正常访问开启了CORS的服
务端接门(例如:IE10+、Chrome4+、FireFox3.5+).

```
<img src='imgs/cors的原理.jpg'>

## CORS跨域资源共享
```html
CORS响应头部– Access-Control-Allow-Origin
响应头部中可以携带一个 Access-Control-Allow-Origin字段，其语法如下:

<script>
Access-Control-Allow-origin: <origin>|*
</script>

//其中，origin参数的值指定了允许访问该资源的外域URL。例如，下面的字段值将只允许来自http://itcast.cn的请求:
res.setHeader('Access-Control-Allow-Origin','http:/litcast.cn')
```
## CORS响应头部- Access-Control-Allow-Headers
```
默认情况下，CORS仅支持客户端向服务器发送如下的9个请求头:
Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width ,Content-Type (值仅限于text/plain、multipart/form-data、application/x-www-form-urlencoded三者之一)如果客户端向服务器发送了额外的请求头信息，则需要在服务器端，通过Access-Control-Allow-Headers 对额外的请求头进行声明，否则这次请求会失败!

res.setHeader('Access-Control-Allow-Headers','Content-Type','X-Custom-Header ')
```
## CORS响应头部–Access-Control-Allow-Methods
```html
默认情况下，CORS仅支持客户端发起GET、POST、HEAD请求。
如果客户端希望通过PUT、DELETE等方式请求服务器的资源，则需要在服务器端，通过Access-Control-Alow-Methods来指明实际请求所允许使用的 HTTP方法。
示例代码如下:
<script>
//只允许POST、GET、DELETE、HEAD请求方法
res.setHeader('Access-Control-Allow-Methods''POST，GET，DELETE，HEAD')
//允许所有的 HTTP请求方法
res.setHeader('Access-Control-Allow-Methods','*')
<script>
```
## CORS请求的分类
```
客户端在请求CORS接口时，根据请求方式和请求头的不同，可以将CORS的请求分为两大类，分别是:
简单请求
预检请求

简单请求
同时满足以下两大条件的请求，就属于简单请求:
请求方式:GET、POST、HEAD三者之一
HTTP头部信息不超过以下几种字段:无自定义头部字段、Accept、Accept-Language、Content-Language、DPR.
Downlink、Save-Data、Viewport-Width、Width .Content-Type (只有三个值application/x-www-form-
urlencoded、multipart/form-data、text/plain)

预检请求
只要符合以下任何一个条件的请求，都需要进行预检请求:
请求方式为GET、POST、HEAD之外的请求
Method类型请求头中包含自定义头部字段
向服务器发送了applicationljson格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送ОPTION请求进行预检，以获知服务器是否允许该实际请求，所以这-次的OPTION请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据。

```
## 回顾JSONP的概念与特点
```
概念:浏览器端通过<script>标签的src属性，请求服务器上的数据，同时，服务器返回一个函数的调用。这种请求数据的方式叫做JSONP。
特点:
JSONP不属于真正的Ajax请求，因为它没有使用XMLHttpRequest这个对象。JSONP仅支持GET请求，不支持POST、PUT、DELETE 等请求。
```
## JSONP接口
```
创建JSONP接口的注意事项
如果项目中已经配置了CORS跨域资源共享，为了防止冲突，必须在配置CORS中间件之前声明JSONP的接口。否则JSONP接口会被处理成开启了CORS的接口。示例代码如下:
//优先创建JSONP接口【这个接口不会被处理成CORS接口】
app.get('/api/jsonp',(req，res) => { })
//再配置 CORS中间件【后续的所有接口，都会被处理成CORS接口】
app.use(cors())
//这是一个开启了CORS的接口
app.get('/api/get',(req,res) =>{ })

app.get('/api/jsonp' , (req,res) =>{
    // 获取客户端发送过来的回调函数的名字
    const funcName = req.query.callback
    //得到要通过JSONP形式发送给客户端的数据
    const data = {name:'zs', age: 22 }
    //根据前两步得到的数据，拼接出一个函数调用的字符串
    const scriptStr = `${funcName}(JSON.stringify(data))`
    //把上一步拼接得到的字符串，响应给客户端的<script>标签进行解析执行
    res.send(scriptstr)
})

在网页中使用jQuery 发起JSONP请求
调用$.ajax()函数，提供JSONP的配置选项，从而发起JSONP请求，示例代码如下:

$ ('#btnJSONP').on('click',function () {
$.ajax({
method: 'GET'，
url: 'http://127.0.0.1/api/jsonp',
dataType: 'jsonp'，
//表示要发起JSONP的请
success: function (res) {
console.log(res)
}})

```


