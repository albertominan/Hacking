# Hack The Box
    
  

  ![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/LAME.png)
  
  
## Máquina Lame

  



### Solución
    
    USER FLAG: makis 1af24b37454a23543320d63527ff06b9


    
    ROOT FLAG: root ccee492718b9b2eb3326219037518e20
    
  
  
### Enumeración

Hacemos un ping para saber a que máquina nos enfrentamos a través del TTL 64 linux 128 windows.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/ttllinux.png)

Descubrimos los puertos 21, 22, 139, 445 y 3632 abiertos.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Ports.png)

Hacemos otro escaneo mas especifico para los puertos encontrados.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Targets.png)

### Port 21

Nos conectamos como usuario anonimo ya que vemos previamente que se encuentra habilitado, listamos y probamos comandos.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/FTPAnonymousLogin.png)

Buscamos algún exploit para la versión que encontramos.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SearchSploitVSFTPD.png)

Nos lo copiamos, cambiamos el nombre y analizamos su contenido.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SearchSploitVSFTPD1.png)

Vemos que el exploit utiliza una vulnerabilidad a la hora de hacer login cuando introducimos con el nombre de usuario la carita feliz :) y a su vez nos abre una shell.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SearchSploitVSFTPD2.png)

Hacemos un intento de login tal como dice el escript pero sin exito porque el puerto 6200 está cerrado.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/IntentoLoginNcTelnet.png)

### Port 445

Identificamos una versión de Samba.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SambaEnumeration.png)

Buscamos un exploit.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SambaEnumeration1.png)

Encontramos 1 relevante y analizamos su contenido.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Script.png)

Este script emplea una conexion al puerto 445 y se autentica como usuario con el payload entre comillas, el nohup se usa también cuando ejecutamos un comando en una reverse shell y nos mata la sesión.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Script1.png)

Antes de nada listaremos los recursos compartidos que existen a nivel de red empleando un NULL session.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/SMBclient.png)

Accedemos al directorio /tmp listando los comandos posibles y con logon vamos a usar la función de nohup para mandar un ping a nuestra máquina poniendonos a la escucha con tcpdump y si recibimos el paquete de vuelta quiere decir que podemos inyectar comandos.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/ReverseShell.png)

Recibimos la conexión desde la IP de la máquina víctima.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/PingTCPDUMP.png)

Probamos a meterle un whoami y que nos lo devuelva con nc a nuestra maquina por el puerto 443.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/InyeccionComandos.png)

Recibimos de nuevo la conexión y tenemos una shell de root directamente.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Reverse.png)

Tras estabilizar nuestra shell nos ponemos con la busqueda de las flags.

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/Flags.png)

![](https://github.com/albertominan/Hacking/blob/7736054cfb555db9ecebccf26d586859c05139e9/HackTheBox/SolidState/Capturas/giphy.webp)

![](https://github.com/albertominan/Hacking/blob/cc70219fba98c2fcfe6b18c1ae203d71bb1723ca/HackTheBox/Lame/Capturas/pwned.png)


**Autor:** [AlbertoMiñan](https://github.com/albertominan)
