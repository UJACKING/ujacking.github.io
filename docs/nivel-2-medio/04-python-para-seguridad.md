# Python para seguridad

Bash es perfecto para pegar comandos, pero cuando necesitas **lógica compleja**, manejar JSON, hablar
por red o procesar miles de respuestas, Python gana. Es el lenguaje franco de la ciberseguridad: lo usan
herramientas ofensivas, defensivas, parsers, scripts de explotación y frameworks enteros.

Esta página te enseña las bases que de verdad se usan: **sockets**, **`requests`**, resolución DNS,
banner grabbing y parseo de datos, con código real y correcto.

!!! danger "Uso ético y legal"
    El código de esta página se ejecuta **solo contra tu laboratorio** (localhost, tus VMs o plataformas
    autorizadas). Escanear o atacar sistemas de terceros es delito. Ver
    [Ética y legalidad](../nivel-1-principiante/00-etica-y-legalidad.md).

## Objetivos de aprendizaje

- Repasar las bases de Python útiles: ficheros, listas, diccionarios, funciones, excepciones.
- Entender un **socket** y crear conexiones TCP con la librería `socket`.
- Usar `requests` para consumir HTTP de forma segura.
- Resolver nombres DNS y hacer **banner grabbing** contra tu propio servicio.
- Parsear salidas con `json`, `re` y `csv`.
- Aplicar buenas prácticas: timeouts, manejo de errores, argumentos por línea de comandos.

**Tiempo estimado:** 120–180 min escribiendo código.

## Requisitos previos

- **[Scripts en Bash](../nivel-1-principiante/04-bash/04-scripts-bash.md)**: variables, bucles, argumentos.
- **[Capa de transporte](../nivel-1-principiante/02-redes/06-capa-de-transporte.md)**: TCP, UDP, puertos.
- **[Protocolos de aplicación](../nivel-1-principiante/02-redes/07-protocolos-de-aplicacion.md)**: HTTP.
- Un Python 3 reciente. Puedes usar un **entorno virtual** (`python3 -m venv .venv`).

## Explicación

### Por qué Python

| Ventaja | Detalle |
| --- | --- |
| Legible | Poca ceremonia; ideal para scripts de seguridad. |
| Baterías incluidas | `socket`, `json`, `re`, `hashlib`, `ssl`, `argparse`… |
| Ecosistema | `requests`, `scapy`, `impacket`, `paramiko`… |
| Multiplataforma | El mismo script corre en Linux, Windows y macOS. |

### Bases que vas a usar

```python
# Estructuras
puertos = [22, 80, 443]                 # lista
servicios = {"22": "ssh", "80": "http"}  # diccionario

# Bucle y condición
for p in puertos:
    if p in (80, 443):
        print(f"puerto web: {p}")

# Función con valor por defecto
def saludar(nombre: str = "mundo") -> str:
    return f"hola, {nombre}"

# Manejo de errores: nunca dejes caer el script por una excepción tonta
try:
    resultado = 10 / 0
except ZeroDivisionError as e:
    print(f"error controlado: {e}")
```

### Sockets: hablar por red a bajo nivel

Un **socket** es la puerta de entrada/salida de la red dentro de un programa. En Python, el módulo
`socket` te da acceso casi directo a TCP y UDP.

```python
import socket

def puerto_abierto(host: str, puerto: int, timeout: float = 1.0) -> bool:
    """Devuelve True si el puerto TCP acepta conexión."""
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)          # siempre timeout: nunca cuelgues el script
        try:
            return s.connect_ex((host, puerto)) == 0
        except socket.error:
            return False

if __name__ == "__main__":
    objetivo = "127.0.0.1"   # laboratorio propio
    for p in (22, 80, 443, 8080):
        estado = "abierto" if puerto_abierto(objetivo, p) else "cerrado/filtrado"
        print(f"{objetivo}:{p} -> {estado}")
```

Salida de ejemplo (salida de ejemplo):

```text
127.0.0.1:22 -> abierto
127.0.0.1:80 -> cerrado/filtrado
127.0.0.1:443 -> cerrado/filtrado
127.0.0.1:8080 -> cerrado/filtrado
```

Puntos clave: `connect_ex` no lanza excepción (devuelve un código de error), y `settimeout` evita
esperas infinitas.

### Resolución DNS

```python
import socket

def resolver(nombre: str) -> list[str]:
    """Devuelve la lista de IPs asociadas a un nombre."""
    try:
        _, _, ips = socket.gethostbyname_ex(nombre)
        return ips
    except socket.gaierror as e:
        print(f"no se pudo resolver {nombre}: {e}")
        return []

print(resolver("localhost"))
```

### Banner grabbing contra tu propio servicio

Muchos servicios envían un **banner** al conectarse (versión de SSH, HTTP, SMTP…). Se lee tras
establecer la conexión.

```python
import socket

def banner(host: str, puerto: int, timeout: float = 2.0) -> str:
    with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
        s.settimeout(timeout)
        try:
            s.connect((host, puerto))
            s.sendall(b"HEAD / HTTP/1.0\r\n\r\n")   # para servicios HTTP
            datos = s.recv(1024)
            return datos.decode(errors="replace").strip()
        except socket.error as e:
            return f"sin banner / error: {e}"

print(banner("127.0.0.1", 8000))
```

!!! warning "El banner puede mentir"
    Un administrador puede **falsear** el banner ("Server: nginx" cuando es Apache, o al revés). Un
    banner es un indicio, no una verdad. Cruza siempre con más señales.

### HTTP con `requests`

`requests` es la librería estándar de facto para HTTP (hay que instalarla: `pip install requests`).

```python
import requests

def cabeceras(url: str) -> dict:
    """Devuelve las cabeceras de respuesta HTTP, o {} si falla."""
    try:
        r = requests.get(url, timeout=5, allow_redirects=True)
        return dict(r.headers)
    except requests.RequestException as e:
        print(f"error de red: {e}")
        return {}

for clave, valor in cabeceras("http://127.0.0.1:8000").items():
    print(f"{clave}: {valor}")
```

Cabeceras de seguridad que conviene saber leer:

| Cabecera | Para qué sirve |
| --- | --- |
| `Strict-Transport-Security` | Fuerza HTTPS en el navegador (HSTS). |
| `Content-Security-Policy` | Limita de dónde puede cargar recursos la web. |
| `X-Content-Type-Options: nosniff` | Evita adivinar tipos MIME. |
| `X-Frame-Options` | Evita embeber la web en un iframe (clickjacking). |
| `Set-Cookie` | Ojo a las banderas `Secure` y `HttpOnly`. |

### Parseo: JSON, regex y CSV

```python
import json, re, csv, io

# JSON
datos = json.loads('{"ip": "192.168.1.10", "puertos": [22, 80]}')
print(datos["ip"], datos["puertos"])

# Regex: extraer versiones de un texto
texto = "Server: Apache/2.4.58 (Ubuntu)"
m = re.search(r"Apache/([\d.]+)", texto)
if m:
    print(f"versión detectada: {m.group(1)}")

# CSV desde texto
contenido = "ip,puerto\n192.168.1.10,22\n192.168.1.10,80\n"
for fila in csv.DictReader(io.StringIO(contenido)):
    print(f"{fila['ip']}:{fila['puerto']}")
```

### Automatización: un revisor de cabeceras

Junta todo en un script con argumentos de línea de comandos, timeouts y código de salida.

```python
#!/usr/bin/env python3
"""Revisa cabeceras de seguridad de una URL. Uso: python revisa.py <url>"""
import argparse
import sys
import requests

SEGURIDAD = [
    "strict-transport-security",
    "content-security-policy",
    "x-content-type-options",
    "x-frame-options",
]

def main() -> int:
    parser = argparse.ArgumentParser(description="Comprueba cabeceras de seguridad HTTP.")
    parser.add_argument("url", help="URL a revisar (laboratorio propio)")
    args = parser.parse_args()

    try:
        r = requests.get(args.url, timeout=5)
    except requests.RequestException as e:
        print(f"[!] error: {e}", file=sys.stderr)
        return 1

    presentes = {k.lower() for k in r.headers}
    for cabecera in SEGURIDAD:
        marca = "OK " if cabecera in presentes else "FALTA"
        print(f"[{marca}] {cabecera}")
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

### Buenas prácticas

| Práctica | Por qué |
| --- | --- |
| **Timeout siempre** | Sin él, una conexión muerta cuelga el script. |
| **Manejar excepciones** | Un script de seguridad corre contra entornos hostiles. |
| **`argparse`** | Nada de rutas o IPs *hardcodeadas*. |
| **Logging** en vez de `print` en herramientas largas | Niveles y salida configurable. |
| **Entorno virtual** | Dependencias aisladas y reproducibles. |
| **No reinventar** | Antes de escribir, mira si `scapy`, `requests` o `impacket` ya lo hacen. |
| **Respetar límites** | Nada de lanzar 10.000 conexiones: saturas tu propia red. |
| **Código legible** | Docstrings, tipos, nombres claros. |

!!! tip "Del script al proyecto"
    Cuando tengas varios scripts, organízalos como **proyecto**: carpeta `src/`, `requirements.txt`,
    `README.md` y `argparse`. Te servirá de porfolio:
    [GitHub como portfolio](../empleabilidad/github-como-portfolio.md).

## Práctica guiada

Crea un fichero `lab.py` y ve añadiendo los ejercicios. Ejecuta con `python3 lab.py`.

### Ejercicio 1 — Escáner de puertos propio

Escribe un script que reciba una IP y una lista de puertos y diga cuáles están abiertos.

??? success "Solución"
    ```python
    import socket
    import sys

    def escanear(host, puertos, timeout=0.5):
        abiertos = []
        for p in puertos:
            with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
                s.settimeout(timeout)
                if s.connect_ex((host, p)) == 0:
                    abiertos.append(p)
        return abiertos

    if __name__ == "__main__":
        host = sys.argv[1] if len(sys.argv) > 1 else "127.0.0.1"
        print(escanear(host, [22, 80, 443, 3306, 8000, 8080]))
    ```

### Ejercicio 2 — Resolución inversa

Dada una IP, obtén su nombre (PTR).

??? success "Solución"
    ```python
    import socket

    def inversa(ip):
        try:
            nombre, _, _ = socket.gethostbyaddr(ip)
            return nombre
        except socket.herror:
            return "sin PTR"

    print(inversa("127.0.0.1"))
    ```

### Ejercicio 3 — Comprueba si una web usa HTTPS

Descarga una URL y comprueba si la petición terminó en `https`.

??? success "Solución"
    ```python
    import requests

    def usa_https(url):
        r = requests.get(url, timeout=5)
        return r.url.startswith("https://")

    print(usa_https("http://127.0.0.1:8000"))
    ```

### Ejercicio 4 — Parsea un JSON de resultados

Convierte una salida JSON con hosts y puertos en líneas legibles.

??? success "Solución"
    ```python
    import json

    datos = json.loads('[{"ip":"10.0.0.5","puertos":[80,443]},{"ip":"10.0.0.6","puertos":[22]}]')
    for host in datos:
        for p in host["puertos"]:
            print(f"{host['ip']}:{p}")
    ```

### Ejercicio 5 — HASHea ficheros

Calcula el SHA-256 de un fichero, leyéndolo por bloques.

??? success "Solución"
    ```python
    import hashlib

    def sha256(ruta, bloque=65536):
        h = hashlib.sha256()
        with open(ruta, "rb") as f:
            while trozo := f.read(bloque):
                h.update(trozo)
        return h.hexdigest()

    print(sha256("lab.py"))
    ```
    Leer por bloques evita cargar ficheros grandes enteros en memoria.

## Para ir más allá

- **Documentación oficial de Python** — EN, **Gratis**. <https://docs.python.org>
- **`requests`** — documentación. EN, **Gratis**. <https://requests.readthedocs.io>
- **PEP 8 (estilo)** — EN, **Gratis**. <https://peps.python.org>
- **Scapy** — manipulación de paquetes. EN, **Gratis**. <https://scapy.net>
- **Real Python** — tutoriales. EN, **Freemium**. <https://realpython.com>
- **Automatiza las cosas aburridas con Python** — libro clásico. EN, **Gratis** (edición online).
  <https://automatetheboringstuff.com>

## Siguiente paso

Con Python en el bolsillo, apliquemos automatización al escaneo de puertos de verdad. Sigue con
**[05 · Nmap en profundidad](05-nmap-en-profundidad.md)**.
