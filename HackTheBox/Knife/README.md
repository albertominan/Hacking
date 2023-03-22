# Hack The Box
    
  

  ![](https://github.com/albertominan/Hacking/blob/f63690c6aef5ced0b87134b8e856197a3477d8aa/HackTheBox/Knife/Fotos/knife.png)
  
  
## Máquina Knife

  



### Solución
    
    USER FLAG: "james" >> /home/james/user.txt >> 0544c5446de79e55a9613f6146ad2fc2
    
    ROOT FLAG: "root" >> /root/root.txt >> 712a656036246259c140c222c4d41eef
    
  
  
### Escaneo nmap

Descubrimos los puertos 22 ssh y 80 http abiertos.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/nmap.png)

### Abrimos la página

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/web.png)

### Analizando

La página carece de funciónes accesibles ni botones clickables pero buscando por la versión que nos dice wappalyzer encontramos esto.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/php.png)

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/script.png)

PHP versión 8.1.0-dev se lanzó con una puerta trasera el 28 de marzo de 2021, pero la puerta trasera se descubrió y eliminó rápidamente. 
Si esta versión de PHP se ejecuta en un servidor, un atacante puede ejecutar código arbitrario enviando el encabezado User-Agentt. 

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/script1.png)

### Probando script

Conseguimos una shell y la estabilizamos para que nos sea mas cómoda y práctica.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/reverse-shell.png)

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/estabilizacionshell.png)

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/estabilizacionshell1.png)

### User Flag

Navegamos hasta la carpeta /home/james/user.txt y sacamos la primera flag.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/userflag.png)

### Escalada de privilegios a ROOT

Después de hacer reconocimiento con sudo -l vemos que nuestro usuario tiene un binario con permiso sudo llamado knife.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/sudo-l.png)

Nos vamos en este caso a gtfoBINS y encontramos el binario knife y nos dice que si este tiene permisos de sudo nos permitirá escalar privilegios.

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/gtfo.png)

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/gtfo1.png)

Metemos el comando y nos dá una shell de ROOT

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/root.png)

![](https://github.com/albertominan/Hacking/blob/50af74c925922445de40a7ba068491470ae57ee5/HackTheBox/Knife/Fotos/rootflag.png)

### Pwned!

![](https://github.com/albertominan/Hacking/blob/3db87a840a24e1a3cb94fabc985f04a246d37b69/HackTheBox/Knife/Fotos/pwned1.png)


### Alternativa reverse shell

Existe otra manera de conseguir una shell en la máquina victima aprovechandose de la funcionalidad del backdoor instalado.

![](https://github.com/albertominan/Hacking/blob/3db87a840a24e1a3cb94fabc985f04a246d37b69/HackTheBox/Knife/Fotos/curl.png)

Podemos introducir comandos mediante el header "User-agentt"

![](https://github.com/albertominan/Hacking/blob/3db87a840a24e1a3cb94fabc985f04a246d37b69/HackTheBox/Knife/Fotos/curl1.png)

Para simplificar la salida le pasamos un pipe seguido de html2text

![](https://github.com/albertominan/Hacking/blob/3db87a840a24e1a3cb94fabc985f04a246d37b69/HackTheBox/Knife/Fotos/curl2.png)

Mediante una reverse shell por comandos nos da el mismo resultado que con el script que vimos antes.

![](https://github.com/albertominan/Hacking/blob/3db87a840a24e1a3cb94fabc985f04a246d37b69/HackTheBox/Knife/Fotos/reverse-shell1.png)


**Autor:** [AlbertoMiñan](https://github.com/albertominan)
