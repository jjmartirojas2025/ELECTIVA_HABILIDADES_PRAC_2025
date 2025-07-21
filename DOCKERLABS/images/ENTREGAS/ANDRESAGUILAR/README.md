# Hydra - Preguntas y Respuestas sobre su Uso en Seguridad Informática

## 1. ¿Qué es Hydra y para qué se utiliza principalmente en el ámbito de la seguridad informática?

Hydra es una herramienta de código abierto utilizada en pruebas de penetración para realizar ataques de **fuerza bruta** o **por diccionario** sobre servicios de autenticación. Su función principal es automatizar la verificación de múltiples combinaciones de usuario y contraseña para evaluar la seguridad de sistemas de acceso remoto o web.

---

## 2. Mencione al menos tres protocolos que soporta Hydra para realizar ataques de fuerza bruta.

Hydra soporta una gran variedad de protocolos. Entre ellos:

- `SSH` – Secure Shell
- `FTP` – File Transfer Protocol
- `HTTP/HTTPS` – Formularios web

También incluye: RDP, VNC, SMB, SMTP, TELNET, XMPP, etc.

---

## 3. ¿Cuál es la diferencia entre los parámetros `-l` y `-L` en Hydra?

- `-l`: Se usa para indicar **un único nombre de usuario**.
- `-L`: Se usa para proporcionar **un archivo con múltiples nombres de usuario**.

Esto permite realizar ataques contra un solo usuario (`-l`) o múltiples usuarios (`-L`).

---

## 4. Explica el propósito del parámetro `-P` y da un ejemplo de su uso en un comando.

El parámetro `-P` se utiliza para especificar un archivo que contiene una **lista de contraseñas** (diccionario) que serán probadas una por una.
