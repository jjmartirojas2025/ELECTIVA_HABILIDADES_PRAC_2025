<h1 align="center"><img width="1280" height="720" alt="image" src="https://github.com/user-attachments/assets/b69288c3-8b6b-4fcb-87f3-067a0a9dbc10" /></h1> 
<h1 align="center">:rotating_light::bulb:TALLE EN CLASE CACHOPO – RESOLUCIÓN DE MÁQUINA:bulb::rotating_light:</h1> 

# :eight_spoked_asterisk: **Rubén Contreras Caballero** :anchor:
# :eight_spoked_asterisk: **Johan Martínez Rojas** :anchor:
# :eight_spoked_asterisk: **Mauricio Gómez Rodríguez** :tent:


## :one: Descripción General del Reto
El presente documento describe el proceso de resolución de la máquina CTF "CACHOPO", un entorno vulnerable diseñado para simular escenarios reales de ciberseguridad ofensiva en sistemas Linux. La máquina contiene múltiples vectores de ataque, entre ellos una instancia de WordPress vulnerable, archivos con información oculta mediante esteganografía y configuraciones débiles de privilegios en el sistema operativo.
El objetivo del ejercicio es comprometer completamente la máquina, obteniendo acceso inicial al sistema, escalando privilegios hasta nivel root y finalmente capturando la flag ubicada en el directorio /root. Para ello, se emplean herramientas como nmap, wpscan, sqlmap, stegcracker, hydra y john.

## :two: Enumeración y Detección de Servicios
La fase de enumeración permite identificar los servicios y puertos abiertos en la máquina objetivo. Para ello, se utilizó la herramienta nmap, ejecutando un escaneo completo sobre todos los puertos TCP.

| Comando ejecutado:            | `nmap -p- -sS -sC -sV -T4 -Pn 10.0.2.30`                                 |
|-------------------------------|---------------------------------------------------------------------------|
| Parámetros explicados:        |  **-p-**: escanea los 65,535 puertos                                     |
|                               |  **-sS**: escaneo SYN (rápido y sigiloso)                                |
|                               |  **-sC**: ejecuta scripts NSE por defecto                                |
|                               |  **-sV**: detecta versiones de servicios                                 |
|                               |  **-T4**: velocidad agresiva                                             |
|                               |  **-Pn**: omite detección de host                                        |

Se detecta un servidor web en el puerto 80 y un servicio SSH en el puerto 22. El análisis se centra inicialmente en el servicio web, por ser un punto frecuente de entrada en pruebas de penetración
<h1 align="center"><img width="889" height="197" alt="image" src="https://github.com/user-attachments/assets/063eba77-35cb-4529-9a7a-c95b1b67bf65" /></h1> 
La fase inicial se enfocó en descubrir los servicios expuestos en la máquina objetivo 10.0.2.30. Para ello, se utilizó nmap, realizando un escaneo intensivo de todos los puertos TCP y aplicando scripts de detección automática.

| Resultado destacado                                                                                                                                                                                                 |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Nmap scan report for 10.0.2.30**<br>Host is up (0.0020s latency).<br><br>Not shown: 65,533 closed ports<br><br>**PORT** | **STATE** | **SERVICE**    | **VERSION**                 <br>22/tcp      | open    | ssh             | OpenSSH 8.9p1 Debian            <br>80/tcp      | open    | http            | Apache httpd 2.4.54 ((Debian)) |

| Puerto  | Estado | Servicio | Versión                        |
|---------|--------|----------|--------------------------------|
| 22/tcp  | open   | ssh      | OpenSSH 8.9p1 Debian           |
| 80/tcp  | open   | http     | Apache httpd 2.4.54 ((Debian)) |

