# OpenSockit

A simple library for real-time messaging between clients on the same domain.

## Connect

```javascript
import opensockit from 'https://opensockit.onrender.com/opensockit.js';

const sockit = new opensockit();
await sockit.connect();
console.log('Connected!');
```

## Send Messages

```javascript
// Send a message to all other connected clients on your domain
sockit.send('Hello, world!');
```

## Receive Messages

```javascript
// Listen for incoming messages
sockit.getSocket().on('message', (msg) => {
  console.log('Received:', msg);
});
```

## Basic Chat Example

```html
<!DOCTYPE html>
<html>
<body>
  <div id="messages"></div>
  <input type="text" id="input">
  <button onclick="send()">Send</button>

  <script type="module">
    import opensockit from 'https://opensockit.onrender.com/opensockit.js';
    const sockit = new opensockit();

    sockit.connect().then(() => {
      console.log('Connected!');
    });

    sockit.getSocket().on('message', (msg) => {
      document.getElementById('messages').innerHTML += '<p>' + msg + '</p>';
    });

    window.send = () => {
      const msg = document.getElementById('input').value;
      sockit.send(msg);
      document.getElementById('input').value = '';
    };
  </script>
</body>
</html>
```

## API

- `new opensockit(url)` - Create instance (optional server URL)
- `connect()` - Connect to server (Promise)
- `send(message)` - Send message to other clients on same domain
- `getSocket()` - Get Socket.IO socket for advanced usage
- `disconnect()` - Disconnect from server

Messages are automatically isolated by domain - only clients from the same website can communicate.
