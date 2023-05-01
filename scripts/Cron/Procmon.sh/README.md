//Este script detecta tareas cron ejecutándose en el sistema en vivo 

```bash
#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo...\n"
	tput cnorm; exit 1
}

#Ctrl+C
trap ctrl_ SIGINT

old_process=$(ps -eo user,command)

while true; do
	new_process=$(ps -eo user,command)
	diff <(echo "$old_process") <(echo "$new_process") | grep "[\>\>]" | grep -vE "command|kworker|procmon"
	old_process=$new_process
done
```
