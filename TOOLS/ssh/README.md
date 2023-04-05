# Conexión por ssh con clave pública generada.

modificamos el fichero ``/etc/ssh/sshd_config`` y descomentamos el parámetro PermitRootLogin YES, restauramos service ssh restart y comprobamos que esté activo con ``service ssh status``.

dentro del directorio `` /.ssh`` creamos con ``h-keygen`` un par de claves sin contraseña, nos creará dos archivos, ``id_rsa`` clave privada y ``id_rsa.pub`` clave pública la cual la vamos a meter dentro del directorio ``.ssh`` del usuario que nos queremos autenticar sin contraseña pero con el nombre ``authorized_keys``, una vez hecho esto nos logueamos con ssh ``usuario"@localhost`` y entramos sin contraseña. Si borramos el archivo ``authorized_keys`` nos pedirá contraseña de nuevo.


# Conexión por ssh con clave privada.

con la clave privada ``id_rsa`` y el comando ``ssh-copy-id -i id_rsa "usuario"@localhost`` convertiremos el fichero de clave en uno de identidad autorizada.

ahora tendremos que pasarle este fichero autorizado a un usuario para que haciendo uso de esta clave se pueda conectar al equipo sin contraseña con este comando ``ssh -i id_rsa "usuario"@localhost``

Conexión por openssl

con el comando ``openssl s_client -connect 127.0.0.1:30001`` nos conectamos como cliente al equipo local por el puerto dado para ver el tráfico encriptado ssl

