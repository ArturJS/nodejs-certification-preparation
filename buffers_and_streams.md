# 6. Buffers and Streams 9%

<hr>

Two data handling approaches offered by nodejs.

1. Buffered Approach:

using buffered approach only when whole data is written to the buffer, it can read by the receiver, but this kind of approach violates our asynchronous paradigm.

2. Streamed Approach:

data arrives in chunks and is read as chunks, a chunk can even be of the whole data or a part of data.

### Streams

Streams are objects that lets you read data from a source or write data to the destination in a continuous fashion.

**Used In:**

-   HTTP request & responses
-   Standard input/output(stdin & stdout)
-   File reads and write

**Types**

-   Readable Stream

Readable Stream is used for read operations.

```js
const fs = require('fs');
let data = '';

// Create a readable stream
let readableStream = fs.createReadStream('input.txt');

// Set the encoding to be utf8.
readerStream.setEncoding('UTF8');

// Handle stream events --> data, end,
readableStream.on('data', function(chunk) {
    data += chunk;
});

readableStream.on('end', function() {
    console.log(data);
});
```

-   **Writable Stream**:
    Writable Stream is used for write operations.
    process.stdout.write('A Simple Message \n');

-   **Duplex Streams**:
    These streams are a hybrid of Readable and Writable streams.

-   **Transform Stream**:
    A type of duplex stream where the output is computed based on input.

**Piping** is a process in which we provide the output of one stream as the input to another stream.

```js
const fs = require('fs');

// Create a readable stream
let readableStream = fs.createReadStream('input.txt');

// Create a writable stream
let writeableStream = fs.createWriteStream('output.txt');

// Pipe the read and write operations
// read input.txt and write data to output.txt
readerStream.pipe(writerStream);
```

Все потоки являются экземплярами EventEmitter, то есть можно генерировать события `StreamClass.emit('eventName', data)`, и обрабатывать их `StreamClass.on('eventName', (data) => {});`

Потоки хранят данные в своем внутреннем буфере. Размер буфера можно указать через параметр highWaterMark, который можно задать в конструкторе класса.

```js
new StreamObject({
    objectMode: false,
    highWaterMark: // кол-во байт
}); //по умолчанию 16384 (16kb)
new StreamObject({
    objectMode: true,
    highWaterMark: // кол-во объектов
});//по умолчанию 16
```

В `Readable` потоке данные буферизируются, когда над ним вызвается метод `push(data)`, и остаются в буфере до тех пор, пока их не прочитают, через `read()`. Когда общий размер внутреннего буфера Readable потока достигнет порогового значения(highWaterMark), поток временно прекратит чтение данных.

#### flowing/paused потока Readable

**flowing** — данные поступают непрерывно и как можно быстро для процесса, который их считывает;
**paused** — режим по умолчанию для всех типов потоков, данные передаются только если их явно запросили — явный вызов метода `read()` (метод `read()` неявно вызывается «внутри» метода `pipe()`).

**flowing === true — автоматически:**

-   данные передаются другим потокам через метод `pipe()`;
-   и/или у него есть обработчик события 'data';
-   и/или над ним вызван метод `resume()`.

**flowing === false:**
если «разорвем» связь между источником данных и их потребителем (`Readable.pipe(Writable); Readable.unpipe(Writable)`), и/или удалим обработчик события 'data';
или вызовем метод `Readable.pause()`.

### Buffer

`Buffer` is class which provides instances to store raw data.
A buffer has traditionally been used between devices with speed mis-match so that they can keep on operating at their respective speeds without loss of data.

**create**

```js
//create an uninitiated Buffer of 10 octets
let bufferOne = new Buffer(10);
//create a Buffer from a given array
let bufferTwo = new Buffer([10, 20, 30, 40, 50]);
//create a Buffer from a given string
let bufferThree = new Buffer('Simply Easy Learning');
```

**write**

```js
buf.write(string[, offset][, length][, encoding])
```

-   `string` — это строковые данные, которые должны быть записаны в буфер.
    `offset` — это индекс буфера, с которого начинается запись. Значение по умолчанию — 0.
    `length` — это количество байтов для записи. По умолчанию — `buffer.length`.
    encoding – используемая кодировка. ‘utf8′ — это кодировка по умолчанию.
    Возвращаемое значение
    Этот метод возвращает количество записанных октетов. Если в буфере недостаточно места для размещения всей строки, будет записана часть строки.

**read**

```js
buf.toString([encoding][, start][, end])
```

`encoding` – используемая кодировка. ‘utf8′ — это кодировка по умолчанию.
`start` — индекс, с которого начинается считывание данных, по умолчанию — 0.
`end` –индекс на котором заканчивается считывание из буфера, по умолчанию – окончание буфера.

**toJSON**
`buf.toJSON()`

**concat**
`Buffer.concat(list[, totalLength])`

**compare**
`buf.compare(otherBuffer);`
Возвращаемое значение:
Возвращает число, указывающее насколько второй буфер превосходит либо меньше, либо соответствует buf.

**copy**
`buf.copy(targetBuffer[, targetStart][, sourcestart][, sourceEnd])`
`targetBuffer` — объект буфера который будет скопирован в буфер.
targetStart — число, необязательный, по умолчанию: 0
`sourceStart` — число, необязательный, по умолчанию: 0
`sourceEnd` — число, необязательный, по умолчанию: `buffer.length`

**slice**
`buf.slice([start][, end])`

Other:

-   `Buffer.isEncoding(encoding)` — Возвращает true, если кодировка является допустимым аргументом кодировки, иначе false.
-   `Buffer.isBuffer(obj)` — Проверяет является ли obj буфером.
-   `Buffer.byteLength(string[, encoding])` — Возвращает фактическую длину строки в байтах. Кодировка по умолчанию — ‘utf8′. Это не то же самое, что и String.prototype.length, поскольку String.prototype.length возвращает количество символов в строке.
-   `Buffer.concat(list[, totalLength])` — Возвращает буфер, который является результатом объединения всех буферов в списке.
-   `Buffer.compare(buf1, buf2)` — То же, что и `buf1.compare(buf2)`. Может быть использован с целью сортировки массивов буферов. Например:

```js
const buf1 = Buffer.from('1234');
const buf2 = Buffer.from('0123');
const arr = [buf1, buf2];

console.log(arr.sort(Buffer.compare));
// Prints: [ <Buffer 30 31 32 33>, <Buffer 31 32 33 34> ]
// (This result is equal to: [buf2, buf1].)
```
