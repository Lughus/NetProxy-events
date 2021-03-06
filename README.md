# NetProxy - Events

Example of use with events from node

## Getting started

- install `npm i @lug/netproxy-events`
- use it 
```js
const {NetClientProxyEmitter, NetServerProxyEmitter} = require('@lug/netproxy')

const client = new NetClientProxyEmitter()
const server = new NetServerProxyEmitter()

server.listen(9999)

server.ev.on('socket.data',(socket, data)=>{
  server.send(socket, `I received your message : """${data}"""`)
})

client.connect('localhost',9999)

client.send('Hey srv its me')

client.disconnect()

server.stop()
```

## Methods

At the end you will have this

- Server
  - listen(port)
  - stop()
  - send(socket,data)
- Client
  - connect(ip,port)
  - disconnect()
  - send(data)

and some events that are triggered when it needs to

## Events

An event is fired with `this.ev.emit('event'[,arg])`

### Server

| event             | arg          | type        | description                     |
| ----------------- | ------------ | ----------- | ------------------------------- |
| error             | error        | any         | when an error happen            |
| start             | -            | -           | when the server start listening |
| stop              | -            | -           | when the server stop            |
| socket.connect    | socket       | socket      | when a client connect           |
| socket.disconnect | socket       | socket      | when a client disconnect        |
| socket.data       | socket, data | socket, any | when a client send data         |

### Client

| event             | arg    | type        | description                       |
| ----------------- | ------ | ----------- | --------------------------------- |
| error             | error  | any         | when an error happen              |
| connect           | -      | -           | when the client is connecting     |
| connected         | socket | socket      | when the client is connected stop |
| disconnect        | -      | -           | when a client disconnect          |
| destroy           | -      | -           | when a client is destroyed        |
| data              | data   | any         | when a client recieve data        |


