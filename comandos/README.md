## Gestión de entornos y sistemas:

    $0 (variable de entorno que se ejecuta en entornos de shells conflictivas como puede ser que nos conviertan todo en mayusculas o no nos deje introducir comandos, lo que hace es spawnear una shell de bash)
    
    lsb_release -a (lista la distribución de linux que se está ejecutando)
    
    uname -a (lista la version del kernel)
    
    echo $PATH (lista el path del usuario actual)

## Gestión de archivos y directorios:
    
    mktemp -d (crea un directorio temporal en la ruta /tmp)
    
    cd /dev/shm (directorio como /tmp)
    
    grep -E "^user|^root" (filtra por el parametro que empieza por user y root )
    
    grep -v root (quita la linea con el parametro root)
    
    cat ejemplo.txt | wc -l (lista las lineas totales que tiene un archivo)
    
    diff passwords.new passwords.old (busca diferencias entre dos archivos)
    
    cat /etc/shells (lista las shells que existen en el sistema)
    
    lsattr ejemplo.txt (lista permisos especiales de un archivo)
    
    chattr -i -V ejemplo.txt (ejemplo de cambio de permisos especiales) 
    
    find -perm -4000 2>/dev/null (busca permisos SUID)
    
    find . (lista todos los archivos de la ruta actual)
    
    find . -type f -printf "%f\t%p\t%u\t%g\t%m\n" | column -t (busca archivos en la ruta actual lo lista de forma tabulada y lo ordena en columnas)
    
    find . -name .hidden (busca un archivo de nombre .hidden)
    
    find . -name .hidden | xargs cat (busca un archivo de nombre .hidden y le aplica un cat)
    
    find . -name .hidden | xargs grep "leaving" (busca un archivo de nombre .hidden y le aplica un grep por la palabra leaving)
    
    find . -type f -readable ! -executable -size 1033c | xargs cat (busca archivos que sean readable no executables de peso 1033 c(bytes) y le hace un cat al output)
    
    find / -user bandit7 -group bandit6 -size 33c 2>/dev/null (busca en la raiz un archivo que sea propio de un usuario y un grupo y tenga x peso y borra los errores que de el stdout)
    
    cat $(find . -name -file07) (aplica el cat al comando a nivel de sistema)

## Gestión de procesos y privilegios:

    lsof -i:80 (lista los procesos que estan corriendo en el puerto especificado)
    
    pwdx 39609 (muestra la ruta del proceso con el pid dado)
    
    export PATH=<PATH> (podemos exportar nuestro PATH a la maquina actual, cuanto mas amplio mejor para acceder a mas binarios)
    
    watch -n 1 ls -l /bin/bash (para monitorizar la salida de este comando cada 1 seg)
    
    bash -p (lanza la bash con el parametro -p de privilege)
    
    disown 
    disown -a (convierte el proceso en proceso padre por separado eliminando proceso hijo que es dependiente de la consola, abrir firefox desde consola si cierras la pagina se cierra consola y viceversa, con este comando ambos son procesos padres)
    
    firefox > /dev/null 2>&1 & (abre firefox y elimina el stdin molesto que va apareciendo en consola)
    
    getcap -r / 2>/dev/null (lista las capabilities)

## Gestión de texto y datos:
    
    2>/dev/null (elimina los errores que de el stdout)
    
    awk '/ejemplo/' ejemplo.txt | awk '{print $1}' (muestra la linea donde está la palabra ejemplo del archivo ejemplo.txt y luego imprime el primer argumento)
    
    grep "millionth" data.txt -n (imprime el numero de linea donde está el elemento en el archivo)
    
    awk 'NR==1994' ejemplo.txt (lista los elementos de la linea 1994 del archivo ejemplo.txt)
    
    awk 'NF{print $NF}' (imprime el ultimo argumento)
    
    cat data.txt | sort | uniq -u (lista elementos,los ordena y saca la linea que solo está una vez en el archivo)
    
    strings data.txt | grep "===" | tail -n 1 (busca strings en el archivo y luego busca elementos que contengan los valores del grep y saca la última linea)
    
    tr ' ' '\n' (convierte los espacios en saltos de linea)
    
    tr 'r' 'o' (convierte las r en o)
    
    cat data.txt | tr '[G-ZA-Fg-za-f]' '[T-ZA-St-za-s]'  (aplica un rot13 desde donde empieza el primer argumento hasta 13 posiciones G-ZA-F en mayusculas y minusculas y donde T es la 13 posicion desde G)
Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi >> The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv

    echo "Hola que tal" | xxd (muestra la cadena hexadecimal del argumento echo)
    
    echo "Hola que tal" | xxd -ps (muestra la cadena hexadecimal del argumento echo y se queda solo con los valores hexadecimales sin 
espacios)

    echo '' > /dev/tcp/127.0.0.1/30000 (manda una cadena vacía al puerto especificado "refused: puerto cerrado" "echo $? 0 exitoso")
    
    echo "fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq" | nc localhost 30000 (manda la cadena entre " " por nc en el puerto X)
    
    echo $? 0 (codigo de estado exitoso)
    
    echo $? 1 (codigo de estado no exitoso)
    
    echo -n 'my-string' | base64
    
    echo -n 'bXktc3RyaW5n' | base64 --decode
    
## Compresión de archivos:

    7z l archivo.gzip (lista los elementos de dentro del .gzip sin descomprimirlo como si fuera un ls)
    
    7z x data.gzip (descomprime el .gzip)
    
    7z l data.gzip | grep "Name" -A 2 (lista los elementos dentro del .gzip y grepea por el parametro Name y lista 2 lineas por debajo)
    
    7z l data.gzip | grep "Name" -B 2 (lista los elementos dentro del .gzip y grepea por el parametro Name y lista 2 lineas por encima)
    
    7z l data.gzip | grep "Name" -C 2 (lista los elementos dentro del .gzip y grepea por el parametro Name y lista 2 lineas por encima y por debajo)
    
    
