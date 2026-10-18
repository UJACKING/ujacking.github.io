# Máquinas objetivo

Un laboratorio sin objetivos es media práctica. En esta página tienes las **máquinas vulnerable** que
usarás a lo largo de todo el curso: aplicaciones web deliberadamente inseguras y sistemas completos con
fallos a propósito. Su función es ser tu **blanco de práctica legal**: sistemas que **existen para ser
atacados** y que puedes romper tantas veces como quieras.

!!! danger "Recordatorio ético"
    Estas máquinas son vulnerables **a propósito** y por eso están pensadas para correr **aisladas** en tu
    laboratorio. **Jamás** las conectes a Internet ni a tu red real. Todo lo que hagas aquí es en tu
    laboratorio o en plataformas autorizadas:
    **[00 · Ética y legalidad](../00-etica-y-legalidad.md)** y
    **[07 · Laboratorio de red virtual](07-laboratorio-red-virtual.md)**.

## Objetivos de aprendizaje

- Elegir la máquina objetivo adecuada para cada tipo de práctica.
- Desplegar cada una: con **VirtualBox/VMware** o con **Docker** según corresponda.
- Saber **para qué sirve** cada máquina y qué técnicas se practican en ella.
- Entender las precauciones especiales de las **VMs de Windows de evaluación**.

**Tiempo estimado:** 60–90 min (más descargas).

## Requisitos previos

- **[07 · Laboratorio de red virtual](07-laboratorio-red-virtual.md)**: red aislada montada.
- **[06 · Montar Kali y Parrot](06-montar-kali-y-parrot.md)**: tu máquina atacante lista.
- Nociones básicas de **HTTP y web** (útiles, no obligatorias): módulo de
  **[Redes · protocolos de aplicación](../02-redes/07-protocolos-de-aplicacion.md)**.

## Explicación

### Un objetivo para cada cosa

Hay dos grandes familias de objetivos, y conviene usar la adecuada según lo que quieras practicar:

- **Sistemas completos vulnerables:** una máquina entera con muchos servicios y fallos. Sirven para
  practicar **pentesting de infraestructura** (reconocimiento, explotación de servicios, escalada).
- **Aplicaciones web vulnerables:** una app que corre sobre un servidor. Sirven para practicar
  **seguridad web** (inyecciones, XSS, control de acceso…).

| Objetivo | Familia | Practicas sobre todo | Despliegue |
| --- | --- | --- | --- |
| **Metasploitable 2** | Sistema completo | Escaneo, explotación de servicios, shells | VirtualBox/VMware |
| **DVWA** | Web | Inyección SQL, XSS, CSRF, subida de ficheros | Docker o servidor web |
| **OWASP Juice Shop** | Web (moderna) | Top 10 de OWASP, bypass de autenticación, XSS | Docker o Node.js |
| **WebGoat** | Web (aprendizaje) | Lecciones guiadas de seguridad web | Docker o Java |
| **VulnHub (varias)** | Sistema completo | Máquinas completas con flag, tipo CTF | VirtualBox |
| **VMs de evaluación de Windows** | Sistema completo | Enumeración y ataque a Windows | Hipervisor |

!!! tip "Empieza por las web con Docker"
    Levantar DVWA, Juice Shop o WebGoat con Docker es cuestión de minutos y **no consume los recursos de
    una VM completa**. Son perfectas para tus primeras semanas: aprendes sin pelearte con la instalación.

### Docker en 30 segundos

**Docker** empaqueta una aplicación y sus dependencias en un **contenedor**: un proceso aislado que corre
compartiendo el kernel del sistema. No es una máquina virtual completa (pesa y arranca muchísimo menos),
pero **para el laboratorio** cumple de sobra cuando el objetivo es una aplicación web.

Instalación: sigue la guía oficial en [https://docs.docker.com](https://docs.docker.com).

Comandos que usarás:

| Comando | Qué hace |
| --- | --- |
| `docker run -p 80:80 imagen` | Ejecuta la imagen, publicando su puerto 80 en tu 80. |
| `docker run -d -p 8080:8080 imagen` | Lo mismo, pero en **segundo plano** (detached). |
| `docker ps` | Contenedores **en ejecución**. |
| `docker ps -a` | Todos (incluidos los parados). |
| `docker stop ID` | Para un contenedor. |
| `docker rm ID` | Elimina un contenedor parado. |
| `docker images` | Imágenes descargadas. |
| `docker pull imagen` | Descarga una imagen. |

!!! warning "Aísla también los contenedores"
    Publicar un puerto con `-p` lo hace accesible desde la máquina **anfitriona** y, según tu red, desde
    más sitios. En un laboratorio doméstico estate atento a **no exponerlo al exterior** y, si puedes,
    liga el puerto solo a la interfaz del laboratorio.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Verificar y fijar los **nombres de imagen y etiquetas exactos** publicados oficialmente para DVWA,
    Juice Shop y WebGoat (en sus páginas de proyecto y en el registro oficial de imágenes), y ajustar los
    comandos de esta página a los vigentes.

### Metasploitable 2

**Qué es:** una máquina virtual basada en Ubuntu, creada por el equipo de **Metasploit** (Rapid7),
**deliberadamente** llena de servicios vulnerables. Es la máquina "clásica" para aprender pentesting de
infraestructura: tiene FTP, SSH, HTTP, Samba, base de datos, Tomcat y más, casi todo vulnerable.

**Para qué sirve:** practicar **reconocimiento y explotación de servicios** con Nmap, Metasploit y
herramientas de red. Es la compañera natural de las introducciones a Metasploit y a Nmap.

**Cómo desplegarla:**

1. Descarga el archivo oficial desde la web del proyecto (Rapid7/Metasploit). TODO-UJACKING: confirmar el
   enlace de descarga y la licencia vigentes.
2. Está distribuida como **disco virtual (VMDK)**; se importa en VirtualBox/VMware como disco existente.
3. Asígnale **solo** la red **host-only/interna** del laboratorio.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Confirmar el **enlace de descarga oficial** y la **licencia** de Metasploitable 2 desde la web del
    proyecto, y anotar aquí las **credenciales por defecto** publicadas (no darlas de memoria).

**Nota:** es una máquina **antigua** (servicios de hace muchos años). Sigue siendo fantástica para
aprender, pero no refleja un sistema actual. Cuando quieras algo más moderno, existen proyectos
sucesores (como Metasploitable 3) que se construyen con herramientas de automatización; comprueba su
estado y requisitos en la web oficial del proyecto.

### DVWA (Damn Vulnerable Web Application)

**Qué es:** una aplicación web **PHP + MySQL** creada para practicar vulnerabilidades web de forma guiada.
Tiene cada vulnerabilidad en un **nivel de dificultad** (Low / Medium / High) que puedes cambiar, y un
panel para configurar todo.

**Para qué sirve:** practicar las vulnerabilidades clásicas: **inyección SQL**, **XSS**, **CSRF**,
**ejecución de comandos**, **inclusión de ficheros**, **subida de ficheros**… Es una base excelente antes
de lanzarte a plataformas reales como PortSwigger.

**Cómo desplegarla (Docker, lo más rápido):**

```bash
docker run --rm -it -p 80:80 vulnerables/web-dvwa
```

```text
[*] Starting MySQL...
[*] Starting Apache...
```

*(salida de ejemplo; el nombre exacto de la imagen debe confirmarse)* Luego abre en tu navegador la IP de
la máquina de laboratorio en el puerto 80 y accede con las credenciales que indique el proyecto (por
defecto suele ser `admin` / `password`, pero **compruébalo en la web del proyecto**).

**Alternativa:** instalarla como aplicación web en un servidor propio (Apache + PHP + MySQL). El proyecto
es de **OWASP**: [https://owasp.org](https://owasp.org).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Verificar las **credenciales por defecto** y las **instrucciones de instalación vigentes** de DVWA en
    su repositorio/página oficial, y actualizar este apartado.

### OWASP Juice Shop

**Qué es:** una aplicación web **moderna** (JavaScript/Node.js) deliberadamente insegura, proyecto insignia
de OWASP. Simula una tienda online y esconde **decenas de retos**: cada uno está mapeado a una
vulnerabilidad real del **OWASP Top 10**. Lleva una puntuación y un "hacko-meter".

**Para qué sirve:** es de las mejores formas de aprender **seguridad web actual**: XSS, inyección,
control de acceso roto, fallos de autenticación, fugas de información… Y tiene una buena **guía de pistas**
integrada (que puedes usar solo cuando te atasques).

**Cómo desplegarla (Docker):**

```bash
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

```text
info: Server listening on port 3000
```

*(salida de ejemplo; el nombre exacto de la imagen debe confirmarse)* Abre `http://IP-del-laboratorio:3000`.

**Alternativa:** instalación con **Node.js** directamente desde el repositorio del proyecto.
Web oficial del proyecto (OWASP): [https://owasp.org](https://owasp.org).

### WebGoat

**Qué es:** otra aplicación **OWASP**, hecha como **curso guiado**: te presenta lecciones y ejercicios con
explicaciones, y tú vas resolviéndolos contra la propia aplicación. Es más "profesor" que "reto libre".

**Para qué sirve:** aprender **fundamentos de seguridad web** de forma estructurada, sobre todo si nunca
has tocado una vulnerabilidad. Hay también una versión pensada para organizar competiciones (WebWolf) que
puedes ver en el proyecto.

**Cómo desplegarla (Docker):**

```bash
docker run -d -p 8080:8080 webgoat/webgoat
```

```text
(arranca en segundo plano; comprueba con docker ps)
```

*(el nombre exacto de la imagen debe confirmarse)* Abre `http://IP-del-laboratorio:8080/WebGoat` y
**regístrate** para empezar las lecciones.

**Alternativa:** ejecutarlo con Java desde el repositorio. Proyecto OWASP: [https://owasp.org](https://owasp.org).

### Máquinas de VulnHub

**Qué es:** [VulnHub](https://www.vulnhub.com) es un catálogo de **máquinas virtuales completas** creadas
por la comunidad para practicar. Cada una suele tener un **objetivo** (conseguir `root`, encontrar una
flag) y un nivel de dificultad.

**Para qué sirve:** es el paso natural desde Metasploitable. Aquí ya no hay "todo vulnerable a lo loco":
hay máquinas más realistas, de distintos sistemas y dificultades, que te obligan a **enumerar**, pensar y
encadenar pasos.

**Cómo desplegarlas:**

1. Descarga el fichero de la máquina (habitualmente `.ova`, `.vmdk` o `.zip`) desde VulnHub.
2. Impórtalo en **VirtualBox** (`Archivo → Importar servicio virtualizado` para `.ova`).
3. Asígnala **solo** a la red **host-only/interna** del laboratorio.
4. Lee la descripción de la máquina: muchas indican el objetivo y a veces las credenciales iniciales.

!!! tip "Elige por dificultad y por objetivo"
    Empieza por máquinas etiquetadas como **fáciles** y de **una sola ruta**. Cuando encadenes 5 fáciles
    sin ayuda, sube de nivel. Cada máquina suele traer su discusión/otras soluciones: **inténtala antes**
    de mirar.

### VMs de evaluación de Windows

**Qué es:** Microsoft publica periódicamente **máquinas virtuales de evaluación** de Windows (entornos de
desarrollo y versiones de evaluación de Windows Server / Windows cliente, y algunas VMs con navegador para
probar compatibilidad). Sirven para que tú tengas un Windows **legal** con el que practicar en tu
laboratorio.

**Para qué sirve:** practicar **enumeración y ataque a Windows** con un sistema real: usuarios, servicios,
SMB, registro, etc. Es la base de lo que harás en Active Directory en Nivel 2.

**Cómo desplegarlas:**

1. Descarga la VM desde el sitio **oficial** de Microsoft (no desde terceros).
2. Impórtala en tu hipervisor.
3. Al ser de **evaluación**, suele tener **fecha de caducidad** y **condiciones de licencia**. Léelas.
4. Conéctala **solo** al laboratorio.

!!! warning "PENDIENTE (TODO-UJACKING)"
    **Verificar la disponibilidad y las licencias** de las VMs de evaluación de Windows (y de las VMs de
    navegador) en la web oficial de Microsoft: qué formatos se ofrecen hoy (VirtualBox/VMware/Hyper-V),
    durante cuánto tiempo son evaluables, si requieren activación y si su uso está permitido en tu país.
    Sustituir las descripciones genéricas de este apartado por los datos oficiales vigentes.

!!! danger "Estas VMs caducan"
    Una VM de evaluación **no** es una licencia permanente de Windows. Cuando caduca, deja de funcionar
    correctamente y **no** debes intentar extenderla ilegalmente. Para un laboratorio permanente,
    plantéate usar versiones de evaluación oficiales vigentes o entornos de nube autorizados.

## Ejemplos prácticos

### 1. Levantar Juice Shop con Docker

```bash
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

En tu **máquina atacante**, comprueba que responde:

```bash
curl -I http://10.10.10.30:3000
```

```text
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: text/html; charset=utf-8
```

*(salida de ejemplo)* `curl -I` pide solo las cabeceras. Ver un `200 OK` confirma que el objetivo web está
arriba en la red del laboratorio.

### 2. Descubrir los objetivos del laboratorio

```bash
sudo nmap -sn 10.10.10.0/24
sudo nmap -sV -p 22,80,3000,8080 10.10.10.0/24
```

```text
Nmap scan report for 10.10.10.30
PORT     STATE SERVICE VERSION
80/tcp   open  http    Apache httpd
3000/tcp open  http    Node.js (Express)
```

*(salida de ejemplo)* Primero descubres qué hosts están vivos; luego escaneas solo los puertos que te
interesan. Recuerda: **solo** contra `10.10.10.0/24`, tu red de laboratorio.

### 3. Consultar el estado de tus contenedores

```bash
docker ps
```

```text
CONTAINER ID   IMAGE                     PORTS                    NAMES
9f1c2d3e4a5b   bkimminich/juice-shop     0.0.0.0:3000->3000/tcp   happy_hopper
```

*(salida de ejemplo)* Te da el ID (para pararlo con `docker stop`), la imagen y el mapeo de puertos.

## Errores comunes

| Error | Por qué ocurre | Solución |
| --- | --- | --- |
| Objetivo con IP de mi red real | Está en bridged/NAT. | Cámbialo a host-only/interna y verifica el aislamiento. |
| `docker: command not found` | Docker no está instalado. | Instálalo siguiendo la guía oficial de Docker. |
| El puerto ya está ocupado | Otro servicio usa ese puerto. | Publica en otro puerto: `-p 8081:8080`. |
| No puedo entrar en DVWA/Juice Shop | Credenciales o URL incorrectas. | Consulta la web del proyecto; a veces hay que inicializar la app. |
| La máquina objetivo caduca | Es una VM de **evaluación**. | Asume la caducidad; no la extiendas de forma ilegal. |
| El objetivo es lentísimo | Es una VM completa y antigua. | Prefiere contenedores para web; sube recursos solo si hace falta. |
| Descargué una VM de un tercero | Prisa. | Descarga **solo** de la web oficial del proyecto. |

## Ejercicios

1. **Elige y justifica.** Para practicar inyección SQL, ¿qué objetivo usarías y por qué?
2. **Levanta DVWA.** Ponlo en marcha con Docker y accede desde tu atacante. Documenta puerto y URL.
3. **Cambia la dificultad.** En DVWA, sube la dificultad de un módulo de Low a Medium y explica qué
   cambió.
4. **Descubre la red.** Con `nmap -sn`, localiza todos los objetivos del laboratorio y anota sus IPs.
5. **Aísla y verifica.** Comprueba que tus objetivos **no** tienen salida a Internet y que tu atacante
   **sí** la tiene.
6. **Investiga VulnHub.** Elige una máquina fácil, lee su descripción y anota objetivo y dificultad.

??? success "Solución"
    1. **DVWA** (o **Juice Shop**), porque están hechas para exponer esa vulnerabilidad de forma guiada y
       con niveles de dificultad. Metasploitable también tiene web vulnerable, pero está orientada a
       infraestructura.
    2. `docker run --rm -it -p 80:80 vulnerables/web-dvwa`; accede a `http://IP-del-laboratorio/`. Anota
       puerto 80 y la IP del laboratorio.
    3. Al subir la dificultad, la aplicación añade **validaciones y filtros** (saneado de entradas,
       consultas parametrizadas, tokens anti-CSRF…). El reto deja de resolverse con el `payload` más
       simple y hay que entender el filtro para saltarlo.
    4. `sudo nmap -sn 10.10.10.0/24`; apunta gateway, atacante y cada objetivo encendido.
    5. Desde cada objetivo: `ping -c 3 8.8.8.8` no debe responder. Desde la atacante: `ping -c 3 8.8.8.8`
       debe responder (por el adaptador NAT).
    6. En [https://www.vulnhub.com](https://www.vulnhub.com), filtra por dificultad fácil, elige una y
       anota el objetivo indicado por su autor y las pistas/credenciales que publique.

## Resumen

- Los objetivos se dividen en **sistemas completos** (Metasploitable, VulnHub, Windows) y
  **aplicaciones web** (DVWA, Juice Shop, WebGoat).
- **Docker** es la vía rápida para los objetivos web; las VMs completas son para infraestructura.
- **Nunca** expongas un objetivo a Internet y **nunca** lo pongas en modo puente.
- Empieza por lo fácil y guiado (WebGoat, DVWA) y sube hacia retos libres (Juice Shop, VulnHub).
- Las **VMs de evaluación de Windows** tienen caducidad y licencia: léelas y **verifica** su disponibilidad
  en la web oficial.
- Documenta cada práctica: es tu porfolio y tu protección.

## Checklist

- [ ] Sé distinguir objetivos de **infraestructura** y de **web**.
- [ ] Tengo un objetivo web levantado con **Docker**.
- [ ] Sé dónde descargar **Metasploitable 2** y cómo importarlo.
- [ ] Conozco **DVWA**, **Juice Shop** y **WebGoat** y para qué sirve cada uno.
- [ ] Sé usar **VulnHub** para buscar máquinas por dificultad.
- [ ] Entiendo que las **VMs de Windows de evaluación** caducan y tienen licencia.
- [ ] Todos mis objetivos están **solo** en la red de laboratorio.
- [ ] He verificado el **aislamiento** de cada objetivo.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [VulnHub](https://www.vulnhub.com) | Catálogo de VMs vulnerables | EN | Gratis |
| [OWASP](https://owasp.org) | DVWA, Juice Shop, WebGoat y el Top 10 | EN | Gratis |
| [PortSwigger Web Security Academy](https://portswigger.net/web-security) | Laboratorios web guiados | EN | Gratis |
| [Documentación de Docker](https://docs.docker.com) | Contenedores | EN | Gratis |
| [TryHackMe](https://tryhackme.com) | Salas y máquinas guiadas | EN | Freemium |
| [Hack The Box](https://www.hackthebox.com) | Máquinas y laboratorios online | EN | Freemium |

## Siguiente paso

Con el laboratorio completo, ya puedes pasar a la consola de verdad: el módulo de **Bash**, empezando por
**[Terminal, shell y consola](../04-bash/01-terminal-shell-y-consola.md)**, y luego tu
**[primer laboratorio](../07-primer-laboratorio.md)** de extremo a extremo.
