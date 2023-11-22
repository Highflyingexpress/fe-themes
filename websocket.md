В общем виде механизм веб-сокета работает так:  
  
1. Веб-страница или приложение создает скрипт с тремя коллбэками (функциями обратного вызова): первый и третий сообщают об установке и закрытии соединения, а второй срабатывает каждый раз, когда клиент получает новые данные от сервера.
  
2. Клиент подключается к серверу по протоколу TCP и подает запрос:
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
  Протокол позволяет работать в асинхронном режиме вместо привычной для веба работы «Запрос-ответ». Так, у клиента и сервера равноправные роли в процессе обмена данными, и они действуют автономно.  
  **–**
  Молчаливый отвал соединения. При отправке пакета в WebSocket вы не узнаете о том, доставлен ли он или нет, пока не пройдёт время таймаута — по умолчанию 75 секунд.  
  Зачастую приходится вводить дополнительные механизмы общения между клиентом и сервером, чтобы быстро понять, отвечает ли клиент.
     