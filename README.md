# Práctica 8: Automatización de Servidores Ubuntu con Docker y Ansible

Proyecto de automatización de infraestructura como código (IaC) donde se despliegan y orquestan 5 servidores Ubuntu mediante Docker Compose y se aprovisionan de forma concurrente utilizando Ansible desde WSL.

---

## 🚀 Tecnologías utilizadas

* **Docker & Docker Compose**: Despliegue de 5 nodos Ubuntu 22.04 configurados con servidor OpenSSH y privilegios sudo sin contraseña.
* **Ansible**: Orquestación y aprovisionamiento declarativo sin agentes vía SSH.
* **WSL (Ubuntu)**: Nodo de control para la ejecución de módulos y playbooks de Ansible.

---

## 📁 Estructura del repositorio

* `Dockerfile`: Imagen base de Ubuntu 22.04 con OpenSSH Server, Python 3 y el usuario `ansible`.
* `docker-compose.yml`: Definición de los 5 servicios (`server1` a `server5`) y mapeo de puertos SSH (`2201-2205`).
* `ansible.cfg`: Configuración global que anula advertencias y desactiva la comprobación estricta de hosts SSH.
* `inventario.ini`: Definición de los nodos administrados, puertos loopback y credenciales de acceso.
* `playbook.yml`: Playbook con la secuencia de tareas declarativas.
* `README.md`: Documentación del proyecto.

---

## 📋 Tareas automatizadas

1. **Actualización del sistema**: Actualización de repositorios y paquetes vía APT.
2. **Creación de usuario**: Creación del usuario de sistema `itla` con directorio `/home/itla` y shell bash.
3. **Gestión de directorios**: Creación del directorio `/app` con permisos restrictivos asignados al usuario y grupo `itla`.
4. **Despliegue de archivos**: Creación del archivo `/app/hola.txt` dentro de la carpeta `/app`.
5. **Instalación de paquetes**: Instalación de las herramientas de diagnóstico y utilidad `cowsay` y `htop`.

---

## ⚙️ Pasos de ejecución

1. **Construir y levantar la infraestructura contenerizada:**
   ```bash
   docker compose up --build -d

2.	Cargar la configuración de Ansible en WSL:
    Bash
    export ANSIBLE_CONFIG=./ansible.cfg

3.	Validar la conectividad SSH hacia los 5 servidores:
    Bash
    ansible servidores -m ping

4.	Ejecutar el playbook de aprovisionamiento:
    Bash
    ansible-playbook playbook.yml

5.	Comprobar la configuración en un contenedor:
    Bash
    docker exec -it server1 /usr/games/cowsay "Automatizacion exitosa"

    docker exec -it server1 cat /app/hola.txt

    docker exec -it server1 id itla

👤 Autor
•	Franciel Antonio Beltré Rodríguez

