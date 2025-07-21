# **<p align="center">:imp::rotating_light::skull:LABORATORIO AMOR - DOCKER LABS:skull::rotating_light::imp:</p>**
# **<p align="center">:warning: TALLER INDIVIDUAL. :warning:</p>**
# <p align="center">![DANIEL TORRES JARAMILLO](https://cdn.hashnode.com/res/hashnode/image/upload/v1721789878989/a33685bd-c727-4147-90b5-101ab06186a7.jpeg?w=1600&h=840&fit=crop&crop=entropy&auto=compress,format&format=webp)</p>

# <p align="center">DANIEL TORRES JARAMILLO
# <p align="center">:shipit::computer:**"LOVE" MACHINE**:computer::shipit: </p>

# <p align="LEFT">DESARROLLO

1.	Realizar una investigación individual de cada una de las herramientas empleadas. Sintetice el resultado mediante un cuadro que explique su definición, funcionalidad y casos de uso.
# <p align="LEFT">TOOLS
![Cyber](https://media4.giphy.com/media/v1.Y2lkPWVjZjA1ZTQ3MmNhM2t4ODdvcno4amdxaHpsZ2QwNjR4MHFiOGhna2QzcWFnOXF1OCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/3oKIPqsXYcdjcBcXL2/giphy.webp)


   

|      Herramienta     |      Definición                                                                                                       |      Funcionalidad principal                                                                            |      Casos de uso comunes                                                                                                                      |
|----------------------|-----------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
|     DOCKER           |     Plataforma de virtualización ligera basada en contenedores.                                                       |     Desplegar, gestionar y aislar aplicaciones   en entornos autocontenidos llamados contenedores.      | Crear laboratorios de ciberseguridad. Aislar   entornos de desarrollo. Automatizar despliegues.                         |
|     NETDISCOVER      |     Herramienta de descubrimiento de red en capa 2 (ARP).                                                             |     Detectar dispositivos activos en una red   local sin necesidad de escaneo activo.                   | Identificar hosts en redes desconocidas. Reconocimiento pasivo en pentesting. Crear   mapas de red.                      |
|     NMAP             |     Network Mapper: herramienta de escaneo y auditoría de red.                                                        |     Escanear puertos, descubrir servicios,   versiones y sistemas operativos de dispositivos en red.    | Enumeración de puertos abiertos. Auditorías de seguridad. Detección de vulnerabilidades.                               |
|     GOBUSTER         |     Herramienta de fuerza bruta para descubrir directorios y archivos   ocultos en servidores web.                    |     Enviar múltiples solicitudes HTTP para   descubrir rutas válidas en una aplicación web.             | Fuzzing   de directorios/archivos web. Enumeración en pruebas de penetración web. Descubrimiento de recursos ocultos.    |
|     HYDRA            |     Herramienta de ataque de fuerza bruta a servicios de autenticación   remota.                                      |     Probar combinaciones de usuarios/contraseñas   sobre servicios como SSH, FTP, HTTP, etc.            | Pentesting de credenciales. Auditoría de autenticación remota. Automatización de ataques por diccionario.              |
|     SCP              |     Herramienta basada en SSH para la transferencia segura de archivos.                                               |     Copiar archivos entre sistemas remotos o   locales de forma cifrada.                                | Transferencia de evidencias. Migrar   configuraciones o binarios. Automatizar copias seguras.
|     SSH              |     Protocolo de red seguro para acceso remoto a través de una consola.                                               |     Conexión a sistemas remotos de forma segura   mediante cifrado.                                     |     - Acceso   remoto a servidores.     -   Administración de sistemas Linux.     - Túneles   SSH para acceso seguro.                          ||
|     STEGHIDE         |     Herramienta de esteganografía para ocultar o extraer información   dentro de archivos (como imágenes o audio).    |     Inserta o recupera archivos secretos en   imágenes o sonidos.                                       | Ciberseguridad forense. CTFs   (Capture The Flag). Estudio   de técnicas de ocultación.                                         |
# COMPLEMENTO DEFINICIONES HERRAMIENTAS

# Docker
Docker es una plataforma de virtualización ligera que permite empaquetar aplicaciones y sus dependencias en contenedores. Un contenedor es una unidad ejecutable estandarizada que incluye todo lo necesario para ejecutar una aplicación: código, bibliotecas, entorno y configuración.
En ciberseguridad, Docker es ampliamente utilizado para crear entornos aislados, reproducibles y seguros para pruebas de herramientas, análisis de malware, prácticas de pentesting o despliegue de entornos CTF (Capture The Flag).

# Netdiscover
Netdiscover es una herramienta de reconocimiento pasivo o activo utilizada para descubrir direcciones IP activas y dispositivos conectados dentro de una red local (LAN).
Emplea técnicas ARP (Address Resolution Protocol) para mapear direcciones MAC con sus respectivas direcciones IP, lo que lo hace ideal en redes donde no se cuenta con un servidor DHCP.
Es útil para realizar un escaneo rápido de hosts vivos en una red interna antes de usar herramientas más profundas como nmap.

# Nmap
Nmap (Network Mapper) es una de las herramientas más potentes y conocidas en el ámbito del escaneo de redes y puertos. Permite descubrir hosts y servicios en una red mediante el envío de paquetes y el análisis de las respuestas.
Entre sus funciones están: detección de sistemas operativos, escaneo de puertos abiertos, identificación de servicios y versiones, detección de firewalls, etc.
Es esencial para la fase de reconocimiento activo durante un pentest.

# Gobuster
Gobuster es una herramienta de fuerza bruta para directorios y archivos ocultos en servidores web.
Utiliza diccionarios (wordlists) para enumerar rutas HTTP/HTTPS (como /admin, /login, etc.), subdominios o buckets en servicios como Amazon S3.
Es muy utilizada para encontrar recursos ocultos no listados que podrían exponer vulnerabilidades.

# Hydra (o THC-Hydra)
Hydra es una herramienta para realizar ataques de fuerza bruta o ataques de diccionario contra varios servicios que requieren autenticación.
Soporta múltiples protocolos como FTP, SSH, HTTP, RDP, SMB, Telnet, entre otros.
Es útil en pruebas de penetración para identificar credenciales débiles o por defecto en servicios expuestos.

# SCP (Secure Copy Protocol)
SCP es un protocolo basado en SSH que permite copiar archivos de manera segura entre un host local y uno remoto, o entre dos hosts remotos.
Usa cifrado SSH para proteger los datos en tránsito.
En ciberseguridad, se emplea para transferir herramientas o evidencias entre máquinas durante operaciones ofensivas o forenses.

# SSH (Secure Shell)
SSH es un protocolo criptográfico que permite establecer una conexión segura entre dos sistemas, normalmente para administrar sistemas remotos de forma segura mediante una consola de comandos.
También permite túneles cifrados, reenvío de puertos, copias de archivos (con scp o sftp) y ejecución remota de comandos.
Es clave en la administración segura de sistemas y también en la post-explotación cuando se obtiene acceso remoto a un servidor.

# Steghide
Steghide es una herramienta de esteganografía que permite ocultar archivos dentro de otros archivos portadores, como imágenes (JPEG/BMP) o archivos de audio (WAV).
Soporta cifrado y compresión, y requiere una frase de contraseña para incrustar o extraer la información.
Se usa tanto para ocultar datos como para extraer información oculta durante análisis forense o desafíos CTF.

2.	Explicar en detalle cada uno de los comandos empleados realizando un desglose del mismo y citando al menos tres alternativas (si aplica) de variantes del comando.

![Cyber](https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjAwM3Q5MTM4NXY2MXBlZm5taWx0bjRzajNsaGVmOWE5bzgyam5zMCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/HscDLzkO8EOTmgkhQP/giphy.webp)
![Cyber](https://media3.giphy.com/media/v1.Y2lkPTc5MGI3NjExMjAwM3Q5MTM4NXY2MXBlZm5taWx0bjRzajNsaGVmOWE5bzgyam5zMCZlcD12MV9naWZzX3NlYXJjaCZjdD1n/VTtANKl0beDFQRLDTh/giphy.webp)
![Cyber](https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExcmRuaWN4bzk3OWV5eWpiNTBiNTZkMXIzN3JzcWJ1Z2N0ZW50MG5zeSZlcD12MV9naWZzX3NlYXJjaCZjdD1n/bGgsc5mWoryfgKBx1u/giphy.webp)
![Cyber](https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExdWltM210ZGIyZGxzdW0ydjBmb2FuM2lzcGVvbmpmdXU5d2ltd3JuZyZlcD12MV9naWZzX3NlYXJjaCZjdD1n/l0IyeheChYxx2byDu/giphy.webp)





|                 Comando                 |                Función               |                         Desglose                        |              Variante 1              |         Variante 2         |     Variante 3     |
|:---------------------------------------:|:------------------------------------:|:-------------------------------------------------------:|:------------------------------------:|:--------------------------:|:------------------:|
| ip a                                    | Muestra interfaces y direcciones IP. | Utiliza el comando ip para mostrar interfaces.          | ifconfig                             | ip link                    | ip route           |
| netdiscover -i docker0 -r 172.17.0.0/24 | Descubre dispositivos en red.        | Especifica interfaz docker0 y rango IP.                 | arp-scan -l                          | netdiscover -r <IP>/24     | nmap -sn <IP>/24   |
| sudo nmap --min-rate 5000 -p- -sS -sV        | Escaneo de puertos y servicios.      | Escaneo SYN, todos los puertos, detección de servicios. | nmap -T4 -A                          | nmap -Pn -p 22,80          | nmap --script vuln |
| gobuster dir -u <url> -w <wordlist>     | Fuerza bruta de directorios web.     | Usa diccionario para buscar directorios.                | gobuster dns                         | gobuster fuzz              | dirb               |
| hydra -l user -P wordlist ssh://<IP>    | Fuerza bruta SSH.                    | Usuario fijo, diccionario, objetivo SSH.                | hydra -L users.txt -P pass.txt       | hydra -s 2222              | medusa             |
| ssh user@IP                             | Conexión remota segura.              | Conexión al host remoto con usuario.                    | ssh -p 2222                          | ssh -i key.pem             | sftp               |
| cd /ruta                                | Cambiar de directorio.               | Navega entre carpetas del sistema.                      | cd ~                                 | cd ..                      | cd -               |
| scp user@host:/ruta /destino            | Copiar archivos por SSH.             | Transferencia segura desde un host remoto.              | scp -P 2222                          | scp ./file user@host:/path | rsync -e ssh       |
| file archivo                            | Ver tipo de archivo.                 | Inspecciona metadatos del archivo.                      | file *                               | stat archivo               | exiftool archivo   |
| steghide --extract -sf archivo          | Extraer datos ocultos.               | Usa esteganografía para extraer datos.                  | steghide info archivo.jpg            | steghide embed             | zsteg archivo      |
| `echo                                   | base64 -d`                           | Decodificar base64.                                     | Convierte una cadena base64 a texto. | base64 archivo -d          | `echo texto        |
| su usuario                              | Cambiar de usuario.                  | Cambia a otra cuenta de usuario.                        | su - usuario                         | sudo su -                  | login usuario      |
| sudo -l                                 | Ver comandos permitidos.             | Muestra lo que el usuario puede hacer con sudo.         | sudo -u user comando                 | sudo -s                    | sudoedit archivo   |
| sudo ruby -e 'exec ...'                 | Escalada de privilegios.             | Ejecuta una shell como root usando Ruby.                | sudo /bin/sh                         | sudo python -c ...         | sudo perl -e ...   |
| whoami                                  | Mostrar usuario actual.              | Retorna el nombre del usuario actual.                   | id                                   | echo $USER                 | logname            |

# COMPLEMENTO EXPLICACIÓN COMANDOS EMPLEADOS LABORATORIO "AMOR" DOCKERLABS

# ip a
Descripción:
Muestra toda la información de red de las interfaces del sistema, incluyendo IPs, MACs y estados.
Explicación:Es un alias de ip address show, usado para identificar la IP asignada a cada interfaz de red (como eth0, docker0, lo, etc.).
Uso práctico:Identificar la IP propia o del contenedor para reconocimiento o configuración de red.
# netdiscover -i docker0 -r 172.17.0.0/24
Descripción: Descubre hosts activos en una red usando ARP.
Explicación: -i docker0: especifica la interfaz de red (docker0, propia de contenedores Docker).
             -r 172.17.0.0/24: define el rango de IPs a escanear (clase C).
Uso práctico: Listar dispositivos conectados en la red interna de Docker.}

# sudo nmap --min-rate 5000 -p- -sS -sV
Descripción: Escaneo rápido de todos los puertos y servicios de una IP objetivo.
Explicación de flags: --min-rate 5000: aumenta la velocidad del escaneo (mínimo 5000 paquetes por segundo).
                      -p-: escanea todos los 65535 puertos.
                      -sS: escaneo SYN (stealth scan).
                      -sV: identifica versiones de servicios.
Uso práctico: Encontrar servicios abiertos, como SSH, HTTP, etc., para explotación.

# gobuster dir -u <URL> -w <diccionario>
Descripción: Fuerza bruta de directorios en un servidor web.
Explicación: -u: URL objetivo.
            -w: archivo de diccionario con posibles nombres de directorio (por ejemplo, common.txt).
Uso práctico: Descubrir rutas ocultas como /admin, /login, /secret.

# hydra -l user -P wordlist ssh://<IP>
Descripción: Ataque de fuerza bruta contra servicio SSH.
Explicación: -l user: nombre de usuario fijo.
            -P wordlist: lista de contraseñas a probar.
            ssh://<IP>: protocolo y objetivo.
Uso práctico: Descubrir credenciales válidas para acceso remoto.

# ssh user@IP
Descripción: Establece una sesión remota segura hacia un servidor.
Explicación: Autenticación vía contraseña o clave pública.
Uso práctico: Ingresar al sistema objetivo si se tiene usuario y clave válidos.

# cd /ruta
Descripción: Cambia el directorio actual de trabajo.
Explicación: Navega entre carpetas del sistema de archivos.
Uso práctico: Ubicarse en la ruta donde se encuentra información relevante.

# scp user@host:/ruta /destino
Descripción: Copia segura de archivos desde un host remoto hacia el local.
Explicación: Basado en SSH, cifra el contenido durante la transferencia.
Uso práctico: Extraer archivos sospechosos del objetivo para análisis.

# file archivo
Descripción: Identifica el tipo de archivo.
Explicación: Analiza cabecera y contenido binario del archivo.
Uso práctico: Determinar si un archivo es una imagen, audio, texto, ejecutable, etc. Útil para saber si se puede usar esteganografía.

# steghide --extract -sf archivo
Descripción: Extrae contenido oculto en un archivo usando esteganografía.
Explicación: --extract: inicia la extracción.
             -sf archivo: especifica el archivo portador.
Uso práctico: Extraer contraseñas, banderas u otros datos escondidos en imágenes o audios.

# echo
Descripción: Imprime texto o variables en la terminal.
Explicación: Comando básico para mostrar resultados o pasar entradas a otros comandos.
Uso práctico: Ver contenido de variables, pruebas rápidas, o para redirigir texto.

# su usuario
Descripción: Permite cambiar de usuario en la terminal.
Explicación: Requiere contraseña del usuario destino.
Uso práctico: Escalar privilegios o moverse entre cuentas comprometidas.

# sudo -l
Descripción: Lista los comandos que el usuario puede ejecutar como superusuario sin contraseña.
Uso práctico: Detectar posibles vectores de escalada de privilegios, como si puede ejecutar ruby, python, find, etc., como root.

# sudo ruby -e 'exec "/bin/bash"'
Descripción: Ejecuta una shell interactiva como root usando Ruby.
Explicación: -e: ejecuta código Ruby inline.
             exec "/bin/bash": lanza bash reemplazando el proceso Ruby.
Uso práctico: Escalada de privilegios si ruby está permitido por sudo sin contraseña.

# whoami
Descripción: Muestra el usuario actual con el que se está ejecutando la terminal.
Uso práctico: Verificar si se ha escalado privilegios (por ejemplo, si ahora eres root).

3.	Realice un diagrama de flujo de todo el procedimiento realizado.

![Diagrama de flujo mejorado del Laboratorio _Reto Amor (DockerLabs)_](https://github.com/user-attachments/assets/c5d94833-f618-4871-99d6-461437bd7f06)




