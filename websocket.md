[почитать доку](https://learn.javascript.ru/websocket)  
  
В общем виде механизм веб-сокета работает так:  
  
1. Веб-страница или приложение создает скрипт **с тремя коллбэками** (функциями обратного вызова):
   первый и третий сообщают об установке и закрытии соединения, а второй срабатывает каждый раз, когда клиент получает новые данные от сервера.
  
3. Клиент подключается к серверу по протоколу TCP и подает запрос:
```
  GET /demo HTTP/1.1
  Upgrade: WebSocket
  Connection: Upgrade
  Host: site.com
  Origin: http://site.com
```
  
3. Сервер с поддержкой веб-сокетов отвечает:
```
  HTTP/1.1 101 Web Socket Protocol Handshake
  Upgrade: WebSocket
  Connection: Upgrade
  WebSocket-Origin: http://site.com
  WebSocket-Location: ws://site.com/demo
```
  
4. Клиент оставляет соединение открытым — канал готов. Далее при любом обмене информацией между ним и сервером будет срабатывать второй коллбэк скрипта, установленного страницей или веб-приложением.
  
**+**  
  HTTP требует до 2000 байтов накладных расходов, тогда как веб-сокет — всего 2 байта.  
  Протокол позволяет работать в асинхронном режиме вместо привычной для веба работы «Запрос-ответ».  
  У клиента и сервера равноправные роли в процессе обмена данными, и они действуют автономно.  

  **–**  
  Молчаливый отвал соединения.  
  При отправке пакета в WebSocket вы не узнаете о том, доставлен ли он или нет, пока не пройдёт время таймаута — по умолчанию 75 секунд.  
  Зачастую приходится вводить дополнительные механизмы общения между клиентом и сервером, чтобы быстро понять, отвечает ли клиент.  

  **Базовое использование на фронте**
Для использования WebSocket на фронте, нужно создать объект WebSocket, указав адрес сервера WebSocket, к которому вы хотите подключиться. Затем вы можете добавить обработчики событий onopen, onmessage, onclose и onerror для управления соединением и обменом данными.  
  
  ```javascript

  const socket = new WebSocket('ws://localhost:8080');
  
  socket.onopen = function() {
    console.log('Соединение установлено');
  };
  
  socket.onmessage = function(event) {
    console.log(`Получено сообщение: ${event.data}`);
  };
  
  socket.onclose = function(event) {
    console.log('Соединение закрыто');
  };
  
  socket.onerror = function(error) {
    console.log(`Ошибка: ${error.message}`);
  };

```

  **Базовое использование на сервере:**  
    
  Для использования WebSocket на сервере с помощью node.js нужно установить пакет ws и создать экземпляр WebSocket-сервера, указав порт, на котором он будет слушать входящие соединения. Затем вы можете добавить обработчики событий on('connection'), on('message'), on('close') и on('error') для управления соединением и обменом данными.  
  
```javascript

const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', function connection(ws) {
  console.log('Соединение установлено');

  ws.on('message', function incoming(message) {
    console.log(`Получено сообщение: ${message}`);
  });

  ws.on('close', function close() {
    console.log('Соединение закрыто');
  });
});

```
  
   
на клиенте:  
<img src="https://github.com/Highflyingexpress/fe-themes/assets/107925514/8493542c-079f-4334-b710-a7819638b777" width=700 alt="client">

на сервере:  
![image](https://github.com/Highflyingexpress/fe-themes/assets/107925514/d4aafad7-c618-41b1-9b60-de5e6ffbd5ed)

[почитать еще](https://habr.com/ru/articles/727696/)


     
