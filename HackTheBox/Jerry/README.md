# Hack The Box
    
  

  ![](1.png)
  
## Máquina Jerry

  


### Solución
    
    USER FLAG: 
               user.txt 7004dbcef0f854e0fb401875f26ebd00
    
    ROOT FLAG: 
               root.txt 04a8b36e1545a455393d067e772fe90e
    
   

### Escaneo nmap

![](2.png)

### Usamos whatweb modo lammer

![](3.png)

### Abrimos la página

![](14.png)

### Intentamos entrar en manager app

Nos pide credenciales las cuales vienen por defecto en el mensaje de error que nos sale.

![](4.png)

### Probamos Credenciales por defecto

![](5.png)

![](6.png)

### Sacando credenciales por defecto 2

Existen dos maneras de sacar las credenciales por defecto en este caso. 1 con un payload en msfdb y otra con hydra.

#### msfdb

![](9.png)

![](10.png)

![](11.png)

#### hydra

![](hydra.png)

### Investigando la página

Vemos que tiene una función la cual nos permite subir archivos .war que nos permitirá tener una reverse shell de varias formas.

![](8.png)

Probamos también a ver si es vulnerable al CVE-2017-12617 sin éxito

![](7.png)

![](6.png)

![](7.png)

### Reverse shell

Con msfdb y el exploit/multi/http/tomcat_mgr_upload podemos conseguir una shell en el sistema una vez tengamos credenciales validas.

![](12.png)

![](13.png)

### Reverse shell 2

La otra forma de conseguir una reverse shell sería cargando un archivo .war malicioso previamente creado manualmente.

![](war1.png)

![](war2.png)

![](war3.png)

Este script nos creará una ruta en la aplicación que deberemos de pinchar para que nos dé la conexion de vuelta y así tener una shell en el sistema.

![](war4.png)

### Capturando la flag

Navegando entre directorios encontramos en el \home\Users\Administrator\Desktop\flags un archivo llamado 2 for the price of 1.txt.

![](15.png)

![](16.png)

### Pwned!

![](pwned.png)

**Autor:** [AlbertoMiñan](https://github.com/albertominan)
