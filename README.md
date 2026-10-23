# Automatización de Servidores Ubuntu con Docker y Ansible

Proyecto de aprovisionamiento de infraestructura como código (IaC) donde se orquestan 5 servidores Ubuntu mediante Docker Compose y se automatiza su configuración completa utilizando Ansible desde WSL.

---

## Tecnologías utilizadas

* **Docker & Docker Compose**: Despliegue de 5 nodos Ubuntu 22.04 con servidor OpenSSH y privilegios sudo sin contraseña.
* **Ansible**: Orquestación y configuración remota sin agentes vía SSH.
* **WSL (Ubuntu)**: Nodo de control para la ejecución de módulos y playbooks de Ansible.

---

## Tareas automatizadas en cada servidor

1. Actualización completa de índices y paquetes del sistema vía APT.
2. Creación del usuario de sistema `itla`.
3. Creación del directorio `/app` con propietario y permisos restringidos.
4. Creación del archivo `/app/hola.txt` con contenido predeterminado.
5. Instalación de las herramientas de diagnóstico y utilidad `cowsay` y `htop`.

---

## Estructura del repositorio

* `Dockerfile`: Imagen base de Ubuntu 22.04 con OpenSSH, Python 3 y usuario `ansible`.
* `docker-compose.yml`: Definición de los 5 servicios (`server1` a `server5`) y mapeo de puertos SSH (`2201-2205`).
* `ansible.cfg`: Configuración global que anula advertencias y desactiva la comprobación estricta de hosts SSH.
* `inventario.ini`: Definición de los nodos administrados, puertos loopback y credenciales de acceso.
* `playbook.yml`: Playbook con la secuencia de tareas declarativas.
* `README.md`: Documentación del proyecto.

---

## Pasos de ejecución

1. **Construir y levantar la infraestructura contenerizada:**
   ```bash
   docker compose up --build -d