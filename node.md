# node

## 1. node服务崩溃处理方法

- #### 使用uncaughtException

  uncaughtException来全局捕获未捕获的Error，同时你还可以将此函数的调用栈打印出来，捕获之后可以有效防止node进程退出，如： 

  ```
  process.on('uncaughtException', function (err) {
    //打印出错误
    console.log(err);
    //打印出错误的调用栈方便调试
    console.log(err.stack)；
  });
  ```

  这相当于在node进程内部进行守护， 但这种方法很多人都是不提倡的，说明你还不能完全掌控Node.JS的异常。 

- #### 使用 try/catch

  我们还可以在回调前加try/catch，同样确保线程的安全。 

  ```
  var http = require('http');
  
  http.createServer(function(req, res) {
    try {
      handler(req, res);
    } catch(e) {
      console.log('\r\n', e, '\r\n', e.stack);
      try {
        res.end(e.stack);
      } catch(e) { }
    }
  }).listen(8080, '127.0.0.1');
  
  console.log('Server running at http://127.0.0.1:8080/');
  
  var handler = function (req, res) {
    //Error Popuped
    var name = req.params.name;
  
    res.writeHead(200, {'Content-Type': 'text/plain'});
    res.end('Hello ' + name);
  };
  ```

  这种方案的好处是，可以将错误和调用栈直接输出到当前发生的网页上。 

  ### 详情请参考:

  http://www.oschina.net/question/433035_171960

  ## 2.node操作数据库

  - #### 首先通过npm命令安装[MySQL](http://lib.csdn.net/base/mysql)模块 

  ```jsx
  var mysql  = require('mysql');  //调用MySQL模块
  //创建一个connection
  var connection = mysql.createConnection({    
      host     : '127.0.0.1',       //主机
      user     : 'root',            //MySQL认证用户名
      password:'12345',
      port:   '3306',
      database: 'node'
  });
  //创建一个connection
  connection.connect(function(err){
      if(err){       
          console.log('[query] - :'+err);
          return;
      }
      console.log('[connection connect]  succeed!');
  }); 
  //执行SQL语句
  connection.query('SELECT 1 + 1 AS solution', function(err, rows, fields) {
      if (err) {
          console.log('[query] - :'+err);
          return;
      }
      console.log('The solution is: ', rows[0].solution); 
  }); 
  //关闭connection
  connection.end(function(err){
      if(err){       
          return;
      }
      console.log('[connection end] succeed!');
  });
  ```

### 详情请参考:

http://blog.csdn.net/zxc123e/article/details/53232409

## 3.node介绍

- #### Node.js优点：

　　1、采用事件驱动、异步编程，为网络服务而设计。其实Javascript的匿名函数和闭包特性非常适合事件驱动、异步编程。而且JavaScript也简单易学，很多前端设计人员可以很快上手做后端设计。
　　2、Node.js非阻塞模式的IO处理给Node.js带来在相对低系统资源耗用下的高性能与出众的负载能力，非常适合用作依赖其它IO资源的中间层服务。

　　3、Node.js轻量高效，可以认为是数据密集型分布式部署环境下的实时应用系统的完美解决方案。Node非常适合如下情况：在响应客户端之前，您预计可能有很高的流量，但所需的服务器端逻辑和处理不一定很多。

- #### Node.js缺点：

　　1、可靠性低
　　2、单进程，单线程，只支持单核CPU，不能充分的利用多核CPU服务器。一旦这个进程崩掉，那么整个web服务就崩掉了。

```jsx
var server = http.createServer()
server.on('request', function (req, res) {
  // 3.1.通过 req.url 拿到当前请求路径
  var url = req.url
  // 3.2根据不同的请求路径，处理不同的响应
  if (url === '/') {
    // res.writeHead(响应状态码, 响应头对象)
    res.writeHead(200, {
      'Content-Type': 'text/html'
    })
    fs.readFile('./data/index.html', 'utf8', function (err, data) {
      if (err) {
        throw err
      }
      res.end(data)		// 在发送数据完毕之后，主动结束响应
    })
  } else if (url === '/login') {
    res.writeHead(200, {
      'Content-Type': 'text/html'
    })
    fs.readFile('./data/login.html', 'utf8', function (err, data) {
      if (err) {
        throw err
      }
      res.end(data)
    })
  } else {
    fs.readFile('./data/404.html', 'utf8', function (err, data) {
      if (err) {
        throw err
      }
      res.end(data)
    })
  }
})
server.listen(3000, function () {
  console.log('running...')
})
```

### 详情请参考:

http://www.cnblogs.com/GumpYan/p/5940368.html

## 4.Node读取多个文件处理

https://www.cnblogs.com/ysk123/p/9836985.html

## 简答题

- ```
  setTimeout(() => {
    console.log(1);
  }, 0);
  new Promise((resolve, reject) => {
    console.log(2);
    setTimeout(() => {
      resolve()
    }, 0);
  }).then(() => {
    console.log(3);
  }).then(() => {
    console.log(4);
  });
  process.nextTick(() => {
    console.log(5);
  });
  console.log(6);
  // 2 6 5 1 3 4
  // process.nextTick(callback)
  //功能：在事件循环的下一次循环中调用 callback 回调函数。效果是将一个函数推迟到代码书写的下一个同步方
  //法执行完毕时或异步方法的事件回调函数开始执行时；与setTimeout(fn, 0) 函数的功能类似，
  //但它的效率高多了。
  ```

- 