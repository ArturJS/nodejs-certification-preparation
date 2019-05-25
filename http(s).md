# 3. http(s) TCP 11%

<hr>

## NODEJS AND SOCKETS

There are three main implementations of sockets in Nodejs

-   UDP: User Datagram Protocol
-   TCP: Transmission Control Protocol
-   UNIX domain

TCP is a standard that defines how network connection is established and maintained between two hosts. TCP and IP (internet protocol) defines how computer sends packets of data to each other. One of the huge difference between TCP and UDP protocol is that with TCP data integrity is guaranteed.

## Net модуль

net — это специальный сетевой модуль, он используется для создания как серверов так и клиентов. Этот модуль предоставляет асинхронную сетевую оболочку.

### Методы

-   `net.createServer ([options][, connectionlistener])` — Создает новый TCP-сервер. Аргумент connectionListener автоматически устанавливается как прослушиватель для события «connection».
-   `net.connect(options[, connectionListener])` — Метод Фабрики, который возвращает новый «net.Socket» и подключается к указанному адресу и порту.

```js
const { createServer } = require('net');
const server = createServer();

server.listen(3000);
```

net socket is that it's a duplex stream, meaning it implements both readable and writeable, and it's also an event emitter.

```js
const server = createServer();

server.on('connection', socket => {
    socket.write('A client has connected\n');
});

server.listen(3000);
```

**Read stream data**

```js
socket.on('data', data => {
    Object.entries(sockets).forEach(([key, cs]) => {
        if (sockets.id != key) {
            cs.write(data);
        }
    });
});
```

**set encoding to socket**

```js
socket.setEncoding('utf8');
```

## HTTP

Node.js has a built-in module called HTTP, which allows Node.js to transfer data over the Hyper Text Transfer Protocol (HTTP).
The HTTP interfaces in Node.js are designed to support many features of the protocol which have been traditionally difficult to use. In particular, large, possibly chunk-encoded, messages
HTTP never buffers entire requests or responses — the user is able to stream data

**HTTP message headers**

```js
{
    'content-length': '123',
    'content-type': 'text/plain',
    'connection': 'keep-alive',
    'host': 'mysite.com',
    'accept': '_/_'
}
```

lowercased and not modified.

It deals with stream handling and message parsing only. It parses a message into headers and body but it does not parse the actual headers or the body.

The HTTP module can create an HTTP server that listens to server ports and gives a response back to the client.
Use the **createServer()** method

```js
http.createServer(function(req, res) {
    res.write('Hello World!'); //write a response to the client
    res.end(); //end the response
}).listen(8080);
```

**add header to res**

```js
res.writeHead(200, { 'Content-Type': 'text/html' });
```

three main properties of req - Http.serverRequest Object :

-   Method - This contains the HTTP method used on the request.
-   URL - The url is the full URL without the server, protocol or port. does not contain the schema, hostname, or port, but it contains everything after that
-   Headers - This contains an object with a property for every HTTP header on the request.

res - Http.serverResponse Object :

**Setting a Header :**
We can set or change header of response object by setHeader.

```js
response.setHeader('Content-Type', 'application/json');
```

**Writing a Header :**
To write a header, use response.writeHead(status, headers), where headers is an optional argument with an object containing a property for every header you want to send.

```js
response.writeHead(200, {
    'Content-Type': 'text/plain',
    'Cache-Control': 'max-age=3600'
});
```

**Removing a Header :**
calling response.removeHeader and providing the header name:

```js
response.removeHeader('Content-Type');
```

**Request Body :**

The request object that's passed in to a handler implements the ReadableStream interface. This stream can be listened to or piped elsewhere just like any other stream. We can grab the data right out of the stream by listening to the stream's 'data' and 'end' events.

**Response Body :**
the response object is a WritableStream, writing a response body out to the client is just a matter of using the usual stream methods.

```js
response.write('<html>');
response.write('<body>');
```

## HTTPS

HTTPS is the HTTP protocol over TLS/SSL. In Node.js this is implemented as a separate module.

**https.Server**
This class is a subclass of tls.Server and emits events same as http.Server

create https server with

```
https.createServer([options][, requestlistener])
```

[options] - {
key: key,
cert: cert,
ca: ca
};

[options] - {
pfx: fs.readFileSync('test/fixtures/test_cert.pfx'),
passphrase: 'sample'
};

```js
const https = require('https');
const fs = require('fs');

const options = {
    key: fs.readFileSync('test/fixtures/keys/agent2-key.pem'),
    cert: fs.readFileSync('test/fixtures/keys/agent2-cert.pem')
};

https
    .createServer(options, (req, res) => {
        res.writeHead(200);
        res.end('hello world\n');
    })
    .listen(8000);
```

**create a request with https**

```js
https.get(url[, options][, callback])
```

```js
https.get('https://encrypted.google.com/', res => {
    console.log('statusCode:', res.statusCode);
});
```

or requst to secure web server

```js
https.request(url[, options][, callback])
```

options <Object> | <string> | <URL> Accepts all options from http.request(), with some differences in default values:

**Options**
protocol Default: 'https:'
port Default: 443
agent Default: https.globalAgent
callback <Function>
Makes a request to a secure web server.

The following additional options from `tls.connect()` are also accepted:
ca, cert, ciphers, clientCertEngine, crl, dhparam, ecdhCurve, honorCipherOrder, key, passphrase, pfx, rejectUnauthorized, secureOptions, secureProtocol, servername, sessionIdContext.
