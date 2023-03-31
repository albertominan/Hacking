# Como estabilizar una SHELL de Linux.

### Una vez ganemos acceso debemos introducir esta serie de comandos para estabilizarla y poder hacer uso de CTRL + C sin perder la sesión, así como tabular y CTRL + L y además tenerla en las mismas proporciones que en nuestra máquina atacante.

``script /dev/null -c bash`` 

Suspenderemos la sesión actual.

``CTRL + Z `` 

Este comando configura primero la terminal para que se ejecute en modo crudo y desactiva el eco, y luego trae al primer plano el último proceso detenido o en segundo plano que se estaba ejecutando en la terminal.

``stty raw -echo; fg``

Reseteamos.

``reset xterm``

En este punto ya podemos hacer uso de CTRL + C sin perder la sesión pero necesitamos una SHELL mas funcional.

``export TERM=xterm`` 

En el caso de encontrarnos con una rbash podemos exportar una /bin/bash.

``export SHELL=/bin/bash``

En este punto nuestra SHELL es funcional pero necesitamos no tener problemas de proporciones, así que listamos las proporciones actuales en la SHELL estabilizada y en una terminal de nuestra máquina expandida para saber los límites máximos de nuestra pantalla.

``stty size``

Ya solo nos queda este último y tenemos una SHELL 100% operativa y funcional.

``stty rows 53 columns 115

