# Hack The Box
    
  

  ![](https://github.com/albertominan/Hacking/blob/f63690c6aef5ced0b87134b8e856197a3477d8aa/HackTheBox/Knife/Fotos/knife.png)
  
## Máquina Knife

  



### Solución
    
    USER FLAG: "james" >> /home/james/user.txt >> 
    
    ROOT FLAG: "root" >> /root/root.txt >> 
    
  
  
### Escaneo nmap

![](nmap.png)

### Añadimos el dominio al etc/hosts

![](redirect.png)

### Abrimos la página

![](1.png)

### Testeamos sus funciones con la url

![](2.png)

### Abriendo server en python

El server tiene un servicio que convierte páginas web en pdf, para ello necesitamos tener un servidor ejecutándose en nuestra máquina.

![](3.png)

### Descarga y análisis del pdf

Analizando los metadatos vemos que el pdf fué creado con pdfkit v0.8.6 el cual tiene un CVE-2022-25765 el cual nos dice que una app podría ser vulnerable si intenta representar una URL que tiene parámetros de cadena de consulta con la entrada del usuario.


![](4.png)

![](5.png)

![](6.png)

![](7.png)

### Reverse shell

Abriremos un oyente con netcat e introducimos nuestra reverse shell dentro de las comillas del código anterior, una vez hecho esto tendremos una shell.

![](8.png)

![](9.png)

![](10ng)

### Capturando la flag

Navegando entre directorios encontramos en el /home/henry un archivo llamado user.txt el cual no nos dejará acceder con los permisos actuales, en el archivo .bundle encontramos una password del usuario henry y ya podemos leer nuestra flag

![](11.png)

![](12.png)

![](13.png)

### Escalada de privilegios a ROOT

Haciendo sudo -l listamos lo que podemos ejecutar desde esta cuenta de usuario y que descubrimos henry puede ejecutar como root el archivo /opt/update_dependecies.rb el cual tras un vistazo al código vemos que usa YAML.LOAD que es vulnerable al ataque de deserialización, para esto necesitamos crear una carga dentro de un archivo llamado dependencies.yml.

![](14.png)

![](15.png)

![](16.png)

Para hacer esto decidí cambiar a una shell de bash y estabilizarla por comodidad.

![](18.png)

Cargamos con un echo "--- nuestra carga para modificar el archivo dependencies.yml.

![](17.png)

![](19.png)

Comprobamos los cambios y utilizamos la función update_dependencies.rb para que lea nuestra carga y abrimos shell de ROOT.

![](20.png)

![](21.png)

Pwned!

![](22.png)


![](pwned.png)

**Autor:** [AlbertoMiñan](https://github.com/albertominan)
