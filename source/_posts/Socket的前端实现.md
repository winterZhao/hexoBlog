layout: 轮询、长轮询与web
title: Socket的前端实现
date: 2016-04-19 17:33:12
tags: NodeJs
---

## Web Socket
  应用场景:实现即时通讯:如股票交易行情分析、聊天室、在线游戏等，替代轮询和长轮询

### 轮询
> 轮询是在特定的的时间间隔（如每1秒），由浏览器对服务器发出HTTP request，然后由服务器返回最新的数据给客户端的浏览器。这种传统的HTTP request 的模式带来很明显的缺点 – 浏览器需要不断的向服务器发出请求，然而HTTP request 的header是非常长的，里面包含的有用数据可能只是一个很小的值，这样会占用很多的带宽。
```javascript
var xhr = new XMLHttpRequest();
    setInterval(function(){
        xhr.open('GET','/user');
        xhr.onreadystatechange = function(){

        };
        xhr.send();
    },1000)

```

### 长轮询:
   ajax实现:在发送ajax后,服务器端会阻塞请求直到有数据传递或超时才返回。 客户端JavaScript响应处理函数会在处理完服务器返回的信息后，再次发出请求，重新建立连接。
```javascript

    function ajax(){
        var xhr = new XMLHttpRequest();
        xhr.open('GET','/user');
        xhr.onreadystatechange = function(){
              ajax();
        };
        xhr.send();
    }

```
### Web Socket:
    轮询与长轮询都是基于HTTP的，两者本身存在着缺陷:轮询需要更快的处理速度；长轮询则更要求处理并发的能力;两者都是“被动型服务器”的体现:服务器不会主动推送信息，而是在客户端发送ajax请求后进行返回的响应。而理想的模型是"在服务器端数据有了变化后，可以主动推送给客户端",这种"主动型"服务器是解决这类问题的很好的方案。Web Sockets就是这样的方案。

```javascript
//需要先npm install ws

//服务器端
var Server = require('ws').Server;
var wss = new Server({
    port:2000
});
wss.on('connection',function(ws){
    ws.on('message',function(data){
        ws.send('你好,客户端,我是服务器!');
        console.log(data);
    })
});

//node客户端

var WebSocket = require('ws');
var socket = new WebSocket('ws://localhost:2000/');
socket.on('open',function(){
    socket.send('你好，服务器,我是客户端');
});
socket.on('message',function(event){
    console.log(event);
})

//html客户端(注:浏览器客户端与node客户端只需要一种)

<script>
    var socket = new WebSocket('ws://localhost:2000/');
    socket.onopen = function(){

    };
    socket.onmessage = function(event){
        console.log(event.data)
    }
</script>


```