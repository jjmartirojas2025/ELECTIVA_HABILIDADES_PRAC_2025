<img width="396" height="238" alt="image" src="https://github.com/user-attachments/assets/db04cf02-4560-4714-92d2-cc68c08b6d63" />
1.  Cuadro de Herramientas Empleadas
Herramienta	Definición	Funcionalidad	Casos de Uso
Hydra	Herramienta de fuerza bruta para descifrar credenciales de servicios en red.	Automatiza ataques de login contra múltiples protocolos (SSH, FTP, HTTP).	Pentesting de sistemas autenticados; evaluación de contraseñas débiles.
Nmap	Escáner de redes de código abierto.	Detecta hosts activos, puertos abiertos y servicios.	Reconocimiento de infraestructura antes del ataque.
Dirb	Fuerza bruta para descubrimiento de directorios web.	Escanea URLs usando diccionarios para identificar rutas ocultas.	Detección de paneles de login, API no documentadas o errores.
Nikto	Escáner de vulnerabilidades web.	Revisa configuraciones inseguras, versiones obsoletas, y archivos comunes.	Evaluación rápida de seguridad de un servidor web.
Gobuster	Herramienta en Go para descubrimiento de rutas.	Similar a Dirb, pero más rápida y con soporte DNS.	Descubrimiento de subdominios, directorios ocultos.

<img width="442" height="370" alt="image" src="https://github.com/user-attachments/assets/c7e369e8-7c1b-4acd-825f-cca16316c8ea" />
<img width="396" height="248" alt="image" src="https://github.com/user-attachments/assets/cfef4036-97d9-408c-b89f-7f1a3e2d4cc2" />
2.  Explicación Detallada de Comandos Utilizados en el CTF
 Ejemplo 1: Ataque con Hydra a servicio SSH
Comando:
hydra -l admin -P rockyou.txt -t 4 -f 10.10.10.2 ssh
Explicación de parámetros:
- -l admin: Usuario objetivo.
- -P rockyou.txt: Archivo de contraseñas.
- -t 4: Cuatro hilos concurrentes.
- -f: Finaliza al encontrar la primera credencial válida.
- 10.10.10.2: Dirección IP del servidor.
- ssh: Protocolo objetivo.
Variantes:
- -L users.txt
- -s 2222
- -V
🔹 Ejemplo 2: Escaneo con Nmap
Comando:
nmap -sS -sV -p- 10.10.10.2
Explicación de parámetros:
- -sS: Escaneo SYN.
- -sV: Detecta versiones.
- -p-: Todos los puertos.
Variantes:
- -A
- -Pn
- -T4
🔹 Ejemplo 3: Descubrimiento con Dirb
Comando:
dirb http://10.10.10.2/ /usr/share/wordlists/common.txt
Explicación de parámetros:
- URL objetivo.
- Diccionario común.
Variantes:
- -X .php
- -r
- -o resultado.txt
<img width="442" height="662" alt="image" src="https://github.com/user-attachments/assets/1ff602d8-6c5f-4e03-833d-f5c941f552cc" />
