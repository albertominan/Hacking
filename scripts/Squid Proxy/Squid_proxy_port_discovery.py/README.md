//Este script identifica los puertos que hay detrás de un squid proxy.

```python
#!/usr/bin/python3

import sys, signal, requests

def def_handler(sig, frame);
	print("\n\n[!] Saliendo...\n")
	sys.exit(1)
	
# Ctrl+C
signal.signal(signal.SIGINT, def_handler)

main_url = "http://127.0.0.1" # Nuestra IP 
squid_proxy = {'http': 'http://192.168.111.39:3128'} # IP y puerto donde se aloja el squid proxy

def portDiscovery():
	
	common_tcp_ports = { 20, 21, 22, 23, 25, 53, 80, 110, 119, 123, 143, 161, 194, 443, 465, 514, 515, 587, 993, 995, 1080, 1521, 1723, 2082, 2083, 2086, 2087, 2095, 2096, 3306, 3389, 5432, 5632, 5900, 5901, 8080, 8443, 10000, 10050, 10051, 11000, 20000, 30000, 49152, 49153, 49154, 49155, 49156, 49157 }
	
	for tcp_port in common_tcp_ports:
		
		r = requests.get(main_url + ':' + str(tcp_port), proxies=squid_proxy)
		
		if r.status_code != 503:
			print("\n[+] Port " + str(tcp_port) + " - OPEN")
	
	
if __name__ == '__main__':
	
	portDiscovery()
```
