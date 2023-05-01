//Este script cuenta el número de lineas de un archivo

```bash
#!/bin/bash

contador=1

while read line; do
	echo "Linea $contador: $line"
	let contador+=1
done < /etc/passwd
```


POR TERMINAL:

```bash
contador=1; strings data.txt | grep "===" | while read line; do echo "Línea $contador:"$line; let contador+=1; done
```
