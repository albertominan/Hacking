## POST-EXPLOTACION

Cierra la sesión y borra todo el historial de comandos del bash history sin registrar exit al salir

``echo "" > ~/.bash_history && history -c && exit`` 

Borra toda la maquina, hacer solo en caso de emergencia

``(rm -rf /*) 2>/dev/null``


![](https://github.com/albertominan/Hacking/blob/d4831942c722cb529ce0f17d41798cfeedee8c5e/TOOLS/Borrado%20de%20historial%20linux/2023-03-31_024346.png)
