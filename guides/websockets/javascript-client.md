# JavaScript Client

## Example Usage

For use with web based applications, a JavaScript library \(`maze.js`\) is included.

### Create a single connection to the server

```javascript
let socket = new Maze.Socket('/chat')
socket.connect() # returns a promise
  .then(() => {})
```

### Join a channel

```javascript
let channel = socket.channel('chat_room:123')
channel.join()
```

### Subscribe to events / messages

```javascript
channel.on('message_new', (message) => {
  // handle new message here
})

channel.on('user_join', (message) => {})
```

### Send events / messages

```javascript
channel.push('message_new', { message: 'maze websockets is the bomb diggity!' })
```

