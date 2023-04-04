#!/bin/bash

function ctrl_c(){
	echo -e "\n\n[!] Saliendo...\n"
	tput cnorm; exit 1
}

# Ctrl+C 
trap ctrl_c INT

tput civis

old_process="$(ps -eo command)"

while true; do
	new_process="$(ps -eo command)"
	diff <(echo "$old_process") <(echo "$new_process") | grep "[\>\<]" | grep -vE "command|procmon|kworker"
	old_process=$new_process
done
