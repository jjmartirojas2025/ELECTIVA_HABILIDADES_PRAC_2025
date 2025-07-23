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

:eight_spoked_asterisk: **Resultado destacado:**

- Nmap scan report for 10.0.2.30
- Host is up (0.0020s latency).
- Not shown: 65533 closed ports

| Puerto  | Estado | Servicio | Versión                        |
|---------|--------|----------|--------------------------------|
| 22/tcp  | open   | ssh      | OpenSSH 8.9p1 Debian           |
| 80/tcp  | open   | http     | Apache httpd 2.4.54 ((Debian)) |

**Puerto 22/tcp:** Servicio SSH activo (OpenSSH 8.9p1)

**Puerto 80/tcp:** Servidor HTTP Apache activo. Se observará más a fondo en la siguiente fase.

Este escaneo inicial permite enfocar el análisis en el servicio web, donde se encuentra una posible vía de explotación


## :three: Análisis del Servicio Web (WordPress)

- Al acceder desde un navegador a http://10.0.2.30, el servidor redirige a un nombre de dominio interno: http://cachopo.local. Para resolver esta dirección correctamente, fue necesario editar el archivo /etc/hosts en la máquina atacante:

- echo "10.0.2.30 cachopo.local" >> /etc/hosts

Una vez hecho esto, se accede al sitio web, el cual está construido sobre WordPress. Para analizar su configuración y detectar vulnerabilidades, se utiliza la herramienta wpscan.

| Comando ejecutado:                       | `wpscan --url http://cachopo.local --enumerate u,vp,vt`     |
|------------------------------------------|--------------------------------------------------------------|
| Resultados destacados:                   | Usuario identificado: admin                                  |
|                                          | Plugin vulnerable detectado: simple-events                   |
|                                          | Tipo de vulnerabilidad: **Inyección SQL (SQLi)**             |

El plugin simple-events presenta una vulnerabilidad que permite manipular las consultas SQL a través de parámetros GET sin la debida sanitización, lo cual representa una grave brecha de seguridad. Esto indica una vía clara de explotación para acceder a información sensible de la base de datos, como usuarios y contraseñas, lo cual será abordado en la siguiente fase.

<h1 align="center"><img width="881" height="228" alt="image" src="https://github.com/user-attachments/assets/bdda20ed-314e-4cc6-a5d6-4a5ce403bf98" /></h1> 

