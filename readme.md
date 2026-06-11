# Práctica Servidor Web - Semana 8

## 1. Título
**Contenerización de Aplicaciones Frontend en React con Nginx y Orquestación de Red Local mediante Docker Desktop**

---

## 2. Tiempo de duración
**120 minutos**

---

## 3. Fundamentos

La arquitectura moderna de desarrollo de software se basa en el desacoplamiento de servicios utilizando microservicios o arquitecturas distribuidas de Frontend y Backend. Para garantizar que las aplicaciones funcionen exactamente igual en cualquier computadora, evitando el clásico problema de "en mi máquina sí funciona", se emplea la tecnología de contenedorización mediante Docker.

### Docker y Contenedores
Docker es una plataforma que permite empaquetar aplicaciones junto con todas sus dependencias, configuraciones y librerías dentro de unidades llamadas contenedores. Estos contenedores pueden ejecutarse de manera aislada y portable en distintos sistemas operativos sin necesidad de modificar el código.

A diferencia de las máquinas virtuales, los contenedores no requieren un sistema operativo completo, ya que comparten el kernel del sistema anfitrión. Esto permite un menor consumo de memoria RAM, tiempos de inicio más rápidos y mejor rendimiento general. Los contenedores son ampliamente utilizados en entornos DevOps y de despliegue continuo debido a su facilidad de replicación y automatización.

### Servidor Web Nginx
Nginx es un servidor web de código abierto altamente optimizado para servir aplicaciones web y contenido estático. En aplicaciones desarrolladas con React y Vite, el código fuente debe compilarse antes de ser desplegado en producción. Después de este proceso de compilación, se generan archivos HTML, CSS y JavaScript listos para ser servidos por un servidor web.

Nginx destaca por su eficiencia, estabilidad y bajo consumo de recursos, permitiendo manejar múltiples conexiones simultáneas sin afectar significativamente el rendimiento del sistema.

### Redes en Docker y WSL 2
Por defecto, los contenedores Docker operan dentro de redes aisladas. Esto significa que un contenedor no puede acceder directamente a servicios ejecutándose en localhost del sistema anfitrión.

En sistemas Windows, Docker Desktop utiliza WSL 2 (Windows Subsystem for Linux) para ejecutar contenedores Linux de forma eficiente. Gracias a WSL 2 y a configuraciones de red o herramientas de orquestación como Docker Compose, es posible establecer comunicación transparente entre aplicaciones locales, bases de datos y servicios independientes divididos en capas de microservicios.

---

## 4. Conocimientos previos
Para realizar esta práctica el estudiante necesita tener claros los siguientes temas:
* Comandos básicos de terminal de Windows (PowerShell/CMD).
* Navegación entre directorios (`cd`, `dir`, `mkdir`).
* Arquitectura cliente-servidor y políticas de intercambio de recursos de origen cruzado (CORS).
* Consumo de APIs REST mediante protocolos HTTP.
* Conceptos básicos de redes, aislamiento y mapeo de puertos.
* Manejo de editores de código fuente (Visual Studio Code).
* Conceptos fundamentales de Docker: Imágenes, Contenedores, Dockerfile y Volúmenes/Redes.

---

## 5. Objetivos a alcanzar
* Implementar contenedores independientes utilizando entornos basados en Node.js.
* Manipular archivos Dockerfile aplicando técnicas de configuración por capas y aislamiento de contextos.
* Desplegar aplicaciones React de manera desacoplada dentro de contenedores Docker.
* Resolver problemas de comunicación interna entre contenedores y servicios de backend.
* Configurar e inicializar Docker Desktop y WSL 2 en entornos de desarrollo Windows.
* Publicar aplicaciones web integradas mediante mapeo dinámico de puertos y orquestación con Docker Compose.

---

## 6. Equipo necesario
* Computador con sistema operativo Windows 10/11 de 64 bits.
* Docker Desktop con soporte WSL 2 (Windows Subsystem for Linux).
* Node.js instalado localmente (Entorno de ejecución de scripts).
* Visual Studio Code como IDE principal de desarrollo.
* Navegador web moderno (Chrome, Edge, Firefox) con herramientas de desarrollo habilitadas.

---

## 7. Material de apoyo
* Documentación oficial de Docker y Docker Compose Guides.
* Guía de la asignatura práctica correspondiente a la Semana 8.
* Cheat Sheet de comandos avanzados para Docker CLI y PowerShell.
* Documentación oficial de conectividad de redes en WSL 2.

---

## 8. Procedimiento Realizado

### Paso 1: Preparación del espacio de trabajo y reestructuración
Se abrió el entorno de desarrollo en Visual Studio Code dentro del directorio raíz `proyecto-contenedor`. Con el fin de evitar redundancias en el contexto de transferencia hacia el daemon de Docker, se estructuraron las subcarpetas del Frontend y Backend en niveles independientes y limpios.

Se crearon archivos `.dockerignore` tanto en el directorio de la API como en el del cliente web para evitar la inyección masiva de carpetas locales como `node_modules`.

```text
PROYECTO-CONTENEDOR/
├── backend/
│   ├── .dockerignore
│   ├── Dockerfile
│   ├── index.js
│   └── package.json
├── frontend/
│   ├── .dockerignore
│   ├── Dockerfile
│   ├── package.json
│   └── src/
│       ├── App.jsx
│       └── main.jsx
└── docker-compose.yml
c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 221752.png
### Paso 2: Instalación de dependencias y ejecución del Backend
Se ingresó al directorio `backend` mediante la terminal integrada de Visual Studio Code para inicializar el proyecto, instalar los módulos críticos de Node.js (`express` y `cors`), y estructurar los endpoints de la API.

```powershell
cd C:\Users\usuario\Desktop\proyecto-contenedor\backend

npm init -y
npm install express cors
npm start
c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 221836.png

c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 221913.png

## Paso 3: Instalación de Docker Desktop

Se descargó el instalador oficial de Docker Desktop para Windows y se ejecutó con permisos de administrador para evitar conflictos con las directivas de seguridad del sistema operativo. 

Durante el asistente de configuración, se marcó de forma obligatoria la opción de activar el motor de virtualización basado en **WSL 2 (Windows Subsystem for Linux)**, garantizando un entorno nativo de alto rendimiento para ejecutar los contenedores de Linux.

c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 222020.png

---


# 9. Resultados esperados

Al finalizar la práctica, la aplicación frontend debe ejecutarse correctamente dentro del contenedor Docker utilizando Nginx como servidor web.

Al acceder desde el navegador a:

```text
http://localhost:3000

c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 205704.png
c:\Users\usuario\Pictures\Screenshots\Captura de pantalla 2026-06-10 205834.png

# 10. Bibliografía

Docker, Inc. (2026). *Docker Desktop user guide and multi-stage builds documentation*. Recuperado de [https://docs.docker.com/build/building/multi-stage/](https://docs.docker.com/build/building/multi-stage/)

Nginx Software. (2025). *Nginx HTTP server deployment guidelines for production architectures*. Recuperado de [https://nginx.org](https://nginx.org)

Microsoft Corporation. (2026). *Windows Subsystem for Linux (WSL) documentation*. Recuperado de [https://learn.microsoft.com/windows/wsl/](https://learn.microsoft.com/windows/wsl/)
