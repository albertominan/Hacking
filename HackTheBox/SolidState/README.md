# Hack The Box
    
  

  ![](https://github.com/albertominan/Hacking/blob/ae7ed668126890fe4058de412d714b248012c4fd/HackTheBox/SolidState/Capturas/SolidState.png)
  
  
## Máquina SolidState

  



### Solución
    
    USER FLAG: user.txt 56634f6417c0600ec6cde7553631d629

    
    ROOT FLAG: root.txt 5a541606443357581172dd0a8aba791e
    
  
  
### Enumeración

Descubrimos los puertos 22 ssh, 25 smtp, 80 http, 110 pop3, 119 nntp, y 4555 rsip abiertos.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EscaneoInicial.png)

Hacemos otro escaneo mas especifico para los puertos encontrados.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EscaneoTargets.png)

### Port 80

Entramos en una página la cual no presenta a primera vista nada relevante asi que tratamos de recopilar información de ella, comprobamos con whatweb que es como wappalyzer pero por terminal.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/WhatWeb.png)

Tiramos también de launchpad para identificar contra que nos estamos enfrentando y sacar el codename de la máquina.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/Launchpad.png)

### Port 4555

Nos conectamos con netcat a lo que parece una herramienta de administracion de correo la cual nos pide usuario y contraseña.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/Nc4555login.png)

Tras unas pruebas de contraseñas comunes busco credenciales por defecto...

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/DefaultPasswords4555.png)

Estamos dentro y listamos los comandos que podemos ejecutar.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/NcRoot.png)

Tras listar usuarios disponibles y no tener ninguna credencial conocida aún, la forma más facil como somos root es resetear las contraseñas de todos los usuarios para poder entrar en su sesión después sin ninguna complicación.  

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/NcPasswordReset.png)

En este punto sabemos que estamos ante un servicio de correo.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ServicioCorreo.png)

Nos conectamos con nc por primera vez al puerto 110 pero es mejor hacerlo con telnet ya que da menos problemas.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/UserJames110.png)

Comprobamos la bandeja de correo del usuario James y vemos que está vacía.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/CorreoJamesVacio.png)

Comprobando todos los usuarios encontramos este email en la bandeja de John el cual el admin le pide que restrinja el acceso a mindy hasta que se registre en el programa.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EmailAdmin2John.png)

Nos vamos a la bandeja de Mindy y vemos 1 correo con la password temporal que le proporcionó john.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EmailMindy1.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EmailMindy2.png)


### Port 22

Algo me dice que mindy no ha cambiado la contraseña que le dieron y efectivamente, al momento nos damos cuenta de que estamos dentro de una restricted bash la cual nos permite solo utilizar algunos pocos comandos.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/SSHLoginRbashwhoami.png)

los comandos que nos permite son los alojados en el directorio que nos indica el PATH.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/RbashCommands.png)

Intenté exportar mi PATH a mindy pero no deja asi qué probamos a meterle con sshpass un comando que si la rbash está mal configurada, este se ejecutará antes de que salga la bash.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/BashShell.png)

Como estamos dentro del contexto de sshpass nos dá conflicto para estabilizar la shell así que entramos por ssh normal. 

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EstabilizandoShell.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EstabilizandoShell1.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EstabilizandoShell2.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EstabilizandoShell3.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/EstabilizandoShell4.png)

A pesar de tener una bash estabilizada las proporciones aún no son las correctas, vamos a tratar de ponerlas igual que una terminal propia de nuestra máquina.

![](https://github.com/albertominan/Hacking/blob/3781f82847bb9340d3b840bc7bacfcf73102bba7/HackTheBox/SolidState/Capturas/ProporcionesSHELL.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ProporcionesSHELL1.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ProporcionesSHELL2.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ProporcionesSHELL3.png)

### Escalada de privilegios

Identificamos el kernel.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/uname-a.png)

Checkeamos a ver si hay contenedores.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ComprobandoContenedores.png)

Comprobamos que el codename y distribución de linux coinciden con el launchpad que vimos antes.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/lsb_release.png)

Buscamos privilegios SUID para ver que archivos tienen propietario root para poder aprovecharnos de ellos pero no vemos nada relevante a simple vista.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/PrivilegiosSUID.png)

Listamos capabilities para buscar vias potenciales pero nada relevante.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ListadoCapabilities.png)

Creación de script que busca tareas de cron que se estén ejecutando.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ScriptCronfinder.png)

Ahora podemos exportar nuestro PATH para acceder a mas rutas.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ScriptCronfinder1.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ScriptCronfinder2.png)

Ejecutamos nuestro script y encontramos un .py.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ResultadoScript.png)

listamos los permisos de este tmp.py.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/PrivilegiosScriptTMP.png)

Entramos para ver el script y vemos que lo podemos modificar a nuestro favor para cambiar los permisos de nuestra bash.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ScriptTMPModificacion.png)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/ScriptTMPFinal.png)

### ROOT

Con el comando watch estamos ejecutando el comando dado cada segundo para ver los cambios en vivo, nuestra bash pasará a tener el permiso s.

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/Root.png)

![](https://github.com/albertominan/Hacking/blob/7736054cfb555db9ecebccf26d586859c05139e9/HackTheBox/SolidState/Capturas/giphy.webp)

![](https://github.com/albertominan/Hacking/blob/55c54df668c89914067c4d2c996a592be8039f68/HackTheBox/SolidState/Capturas/Pwned.png)


**Autor:** [AlbertoMiñan](https://github.com/albertominan)
