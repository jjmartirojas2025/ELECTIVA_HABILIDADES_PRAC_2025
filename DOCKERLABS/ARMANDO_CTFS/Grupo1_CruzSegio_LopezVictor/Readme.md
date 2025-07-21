# Reto CTF: Ubuntu con SSH – Usuario `legion`

## 1. Descripción General

Este reto plantea un escenario CTF individual mediante una imagen Docker que ejecuta Ubuntu con el servicio SSH habilitado. Se incluye el usuario `legion`, cuya contraseña es el núcleo del desafío. Una vez descubierta, permite autenticarse vía SSH y obtener la bandera correspondiente.

El objetivo es:
- Resolver un acertijo que contiene pistas sobre la contraseña.
- Validar la contraseña mediante una conexión SSH.
- Aplicar herramientas de **Diccionario** como `crunch` e `hydra`.
- Documentar el proceso de acceso al contenedor Docker.

---

## 2. Resolución del Acertijo

### Acertijo:

> Cinco guardianes vigilantes,  
> cada uno con su inicial,  
> la primera se esconde en “estrella”,  
> la segunda en la “selva” tropical,  
> tercera y cuarta van seguidas,  
> ambas en “dedo” se dejan hallar,  
> la última es misteriosa,  
> y en “gato” suena al final.  
> Juntas caminan siempre en fila.

### Análisis:

| Posición | Clave                     | Letra identificada |
|----------|---------------------------|---------------------|
| 1        | Se esconde en "estrella"  | **E**               |
| 2        | En "selva" tropical       | **s**               |
| 3 y 4    | En “dedo”, seguidas       | **d**, **e**        |
| 5        | Suena al final de "gato"  | **g**               |

➡️ **Contraseña sugerida por el acertijo:** `Esdeg`

➡️ También se interpreta como palabra coherente: `Esdeg`

---

## 3. Uso de Crunch

**Crunch** es una herramienta para generar diccionarios personalizados. En caso de requerir fuerza bruta:

```bash
crunch 5 5 -t @@DEO -o dict2.txt
```

O para un diccionario basado en las letras del acertijo:

```bash
crunch 5 5 -o posibles.txt -f /usr/share/crunch/charset.lst alpha -t %%@@@
```

![Crunch](/Images/crunch_dic.png)

---

## 4. Uso de Hydra

Si se desea probar todas las contraseñas generadas:

```bash
hydra -l legion -P posibles.txt ssh://localhost -s 2222
```

- `-l legion`: usuario a atacar.
- `-P posibles.txt`: diccionario con contraseñas.
- `ssh://localhost`: protocolo y host.
- `-s 2222`: puerto SSH mapeado en el contenedor.

![Crunch](/Images/hydra_dic.png)

---

## 5. Resultado de la conexión SSH

Una vez descubierta la contraseña (`debería ser: DESEO`), se puede acceder al contenedor:

```bash
ssh legion@localhost -p 2222
```

### Resultado esperado:

📸 **[Aquí se insertará la imagen del acceso exitoso vía SSH con el usuario `legion`]**

![Resultado](/Images/ssh_conection.png)

---

> ⚠️ **Nota:** Este contenedor no tiene persistencia por defecto. Si se reinicia o elimina, se perderán los datos y configuraciones internas.

---
