---
title: Socket.io发送消息含义
date: 2016-04-19 18:05:36
tags: NodeJs
---

仅作收藏:转自博客园 若相忆;

```javascript

// send to current request socket client
socket.emit('message', "this is a test");

// sending to all clients, include sender
io.sockets.emit('message', "this is a test");

// sending to all clients except sender
socket.broadcast.emit('message', "this is a test");

// sending to all clients in 'game' room(channel) except sender
socket.broadcast.to('game').emit('message', 'nice game');

// sending to all clients in 'game' room(channel), include sender
io.sockets.in('game').emit('message', 'cool game');

// sending to individual socketid
io.sockets.socket(socketid).emit('message', 'for your eyes only');

// 进入一个房间
socket.join('room');
// 离开一个房间
socket.leave('room');

```
订阅发布模式

```javascript

//前端触发订阅/退订事件
socket.emit('subscribe',{"room" : "room_name"};
socket.emit('unsubscribe',{"room" : "room_name"};

//后台处理订阅/退订事件
socket.on('subscribe', function(data) {
    socket.join(data.room);
})
socket.on('unsubscribe', function(data) {
    socket.leave(data.room);
})
```

####浏览器的全局属性 window.WebSocket
![](http://images2015.cnblogs.com/blog/921378/201603/921378-20160330100043051-1238532091.jpg)