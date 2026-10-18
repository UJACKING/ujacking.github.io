# Wireshark

**Resumen.** Wireshark es el analizador de tráfico de red de referencia: captura paquetes y te deja
inspeccionarlos capa por capa. Aquí verás cómo instalarlo, cómo es su interfaz, la diferencia entre
**filtros de captura** y de **visualización**, y un análisis guiado de tres casos reales: un
*three-way handshake* TCP, una consulta DNS y una petición HTTP.

## Objetivos de aprendizaje

- Instalar Wireshark y capturar en la interfaz correcta.
- Diferenciar **filtros de captura** (capture filters) y de **visualización** (display filters).
- Escribir filtros útiles con su sintaxis real.
- Analizar un **three-way handshake** de TCP.
- Analizar una **consulta DNS** y una **petición HTTP**.

**Tiempo estimado: 90–120 min**

## Requisitos previos

- **[06 · Capa de transporte](06-capa-de-transporte.md)**: necesitas el handshake TCP y los flags.
- **[07 · Protocolos de aplicación](07-protocolos-de-aplicacion.md)**: DNS y HTTP son los casos que
  analizaremos.
- **[04 · Capa de enlace](04-capa-de-enlace.md)** y **[05 · Capa de red](05-capa-de-red.md)**: las capas
  que aparecen en el panel de detalle.

!!! danger "Recordatorio ético y legal"
    Captura **solo tu propio tráfico** o el de una red para la que tengas **autorización explícita**.
    Interceptar comunicaciones ajenas es ilegal. Para practicar, usa tu red doméstica, tu máquina
    virtual aislada o un fichero `.pcap` de práctica.

## Explicación

### Qué es Wireshark

Wireshark es un **analizador de protocolos**: pone la tarjeta de red en *modo promiscuo* (recibe todo
el tráfico que llega a esa interfaz, no solo el tuyo) y muestra cada paquete desglosado por capas,
igual que el modelo OSI/TCP-IP. Lo usan administradores para diagnosticar y profesionales de seguridad
para investigar.

### Instalación

=== "Debian / Ubuntu"
    ```bash
    sudo apt update
    sudo apt install wireshark
    ```
    Durante la instalación te preguntará si quieres permitir la captura a usuarios **no root**.
    Responde **Sí** si quieres capturar sin `sudo` (se añade tu usuario al grupo `wireshark`).

=== "Fedora / RHEL"
    ```bash
    sudo dnf install wireshark
    ```

=== "Windows / macOS"
    Descarga el instalador desde la **web oficial**: <https://www.wireshark.org>. Para capturar en
    Windows necesitas además **Npcap** (el instalador te lo ofrece).

!!! note "Versiones"
    No te decimos "la última versión es X". Consulta la versión vigente y las notas de instalación en
    <https://www.wireshark.org>.

### La interfaz

Wireshark tiene tres zonas principales, más una barra de filtros:

1. **Lista de paquetes** (arriba): una fila por paquete, con número, hora, origen, destino, protocolo
   e info.
2. **Detalle del paquete** (centro): el árbol de capas — `Frame`, `Ethernet II`, `IP`, `TCP`, etc.
3. **Bytes** (abajo): el contenido en hexadecimal y ASCII.
4. **Barra de filtros**: arriba, donde escribes los **display filters**.
5. **Barra de estado**: abajo, resumen de lo capturado.

Para empezar: selecciona una **interfaz** en la pantalla inicial (el botón de la aleta azul) y la
captura arranca. El botón rojo la detiene.

### Filtros de captura vs filtros de visualización

Es el concepto que más confunde al principio:

| | Filtro de **captura** | Filtro de **visualización** |
| --- | --- | --- |
| Cuándo actúa | **Antes** de capturar (decide qué se guarda) | **Después** (decide qué se muestra) |
| Dónde se escribe | En la pantalla de captura, caja "Capture filter" | En la barra de filtros de arriba |
| Sintaxis | Estilo **BPF** (libpcap): `tcp port 80` | Estilo **Wireshark**: `tcp.port == 80` |
| Efecto | Lo no capturado **se pierde** | Se puede quitar y volver a ver todo |
| Cuándo usarlo | Cuando el tráfico es enorme y quieres reducir | Casi siempre, para analizar |

!!! tip "Regla práctica"
    Captura **ampliamente** (o sin filtro) y filtra **después** con display filters. Solo usa filtros
    de captura si el volumen es enorme, porque lo que descartes ya no lo recuperas.

**Ejemplos de filtros de captura** (sintaxis BPF, en la caja de captura):

```text
host 192.168.1.50
tcp port 443
udp port 53
not arp
```

**Ejemplos de filtros de visualización** (sintaxis Wireshark, en la barra de arriba):

```text
tcp
tcp.port == 80
ip.addr == 192.168.1.50
dns
http.request.method == "GET"
icmp
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

Comparación directa de la misma idea en las dos sintaxis:

| Quiero... | Filtro de captura | Filtro de visualización |
| --- | --- | --- |
| Solo HTTP | `tcp port 80` | `http` o `tcp.port == 80` |
| Solo DNS | `udp port 53` | `dns` |
| Tráfico de una IP | `host 10.0.0.5` | `ip.addr == 10.0.0.5` |
| Paquetes SYN | (difícil en captura) | `tcp.flags.syn == 1` |
| No ARP | `not arp` | `!arp` |

### Cómo se ve un paquete por capas

Al seleccionar un paquete HTTP verás el árbol:

```text
Frame 12: 500 bytes captured
Ethernet II, Src: 00:1a:2b:3c:4d:5e, Dst: ...
Internet Protocol Version 4, Src: 192.168.1.50, Dst: 93.184.216.34
Transmission Control Protocol, Src Port: 49214, Dst Port: 80, Seq: 1, Ack: 1
Hypertext Transfer Protocol
    GET / HTTP/1.1\r\n
```

Ese orden es la **encapsulación** que estudiaste: Ethernet → IP → TCP → HTTP.

## Ejemplos prácticos

### Análisis 1: el three-way handshake de TCP

1. Abre Wireshark y empieza a capturar en tu interfaz.
2. En una terminal, abre una conexión nueva, por ejemplo:

    ```bash
    curl -s -o /dev/null http://example.com
    ```

3. Detén la captura y aplica este **display filter**:

    ```text
    tcp.port == 80 && tcp.flags.syn == 1
    ```

Verás una secuencia como esta **(salida de ejemplo)**:

```text
No.  Source        Destination   Protocol  Info
10   192.168.1.50  93.184.216.34 TCP       49214 → 80 [SYN] Seq=0 Win=64240 ...
11   93.184.216.34 192.168.1.50  TCP       80 → 49214 [SYN, ACK] Seq=0 Ack=1 Win=65535 ...
12   192.168.1.50  93.184.216.34 TCP       49214 → 80 [ACK] Seq=1 Ack=1 Win=64240 ...
```

Lectura línea a línea:

- **Paquete 10 [SYN]:** el cliente pide abrir conexión desde el puerto efímero `49214` al puerto `80`.
  `Seq=0` es el número de secuencia inicial relativo (Wireshark muestra valores relativos por
  defecto).
- **Paquete 11 [SYN, ACK]:** el servidor acepta. `Ack=1` confirma el SYN del cliente (`Seq=0` + 1).
- **Paquete 12 [ACK]:** el cliente confirma. **Conexión establecida** (`ESTABLISHED`).

A partir de aquí verías el `[PSH, ACK]` con la petición HTTP y los segmentos de respuesta.

!!! tip "Sigue la conversación"
    Clic derecho en un paquete → **Follow → TCP Stream** (o HTTP Stream) para ver todo el diálogo
    reconstruido. Es la forma más rápida de entender una conexión.

### Análisis 2: una consulta DNS

Sin cerrar la captura, ejecuta:

```bash
dig example.com +short
```

Filtra por DNS:

```text
dns
```

Verás algo así **(salida de ejemplo)**:

```text
No.  Source        Destination   Protocol  Info
1    192.168.1.50  192.168.1.1   DNS       Standard query 0x1a2b A example.com
2    192.168.1.1   192.168.1.50  DNS       Standard query response 0x1a2b A example.com A 93.184.216.34
```

- **Paquete 1:** el cliente pregunta al resolutor (`192.168.1.1`) por el registro **A** de
  `example.com`. Fíjate en el **Transaction ID** (`0x1a2b`).
- **Paquete 2:** la **respuesta**, con el mismo ID, y la **IP** en la sección de respuestas
  (`A 93.184.216.34`).

Observa que el **DNS clásico va en claro**: si miras el detalle del paquete, se lee el nombre
consultado sin problema. Eso es exactamente el problema de privacidad que resuelven **DoT/DoH**.

### Análisis 3: una petición HTTP

Filtra por HTTP:

```text
http
```

Selecciona la petición y mira el detalle **(salida de ejemplo)**:

```text
GET / HTTP/1.1\r\n
Host: example.com\r\n
User-Agent: curl/8.x\r\n
Accept: */*\r\n
\r\n
```

Y la respuesta:

```text
HTTP/1.1 200 OK\r\n
Content-Type: text/html; charset=UTF-8\r\n
Content-Length: 1256\r\n
```

Puntos a destacar:

- El **método** (`GET`), la **ruta** (`/`) y la **versión** (`HTTP/1.1`) están en claro.
- La cabecera **Host** indica el dominio. Sin HTTPS, todas las cabeceras y el cuerpo son legibles.
- Compara con una petición **HTTPS** (puerto 443): con el filtro `tls` solo verías el handshake TLS y
  datos cifrados, **no** el HTTP por dentro. Esa es la ventaja de HTTPS.

!!! warning "TODO-UJACKING: falta un `.pcap` de práctica"
    Añadir un fichero de captura de ejemplo (por ejemplo `assets/pcap/practica-redes.pcap`) con un
    handshake TCP, una consulta DNS y una petición HTTP, y enlazarlo aquí para que el alumno pueda
    seguir el análisis sin depender de su propia red. Pendiente de crear el recurso y verificar la
    ruta de descarga.

## Errores comunes

- **Filtrar mal por confundir sintaxis.** `tcp port 80` (captura) ≠ `tcp.port == 80` (visualización).
  Si tu filtro de visualización usa la sintaxis de captura, la barra se pone **roja**.
- **No ver tráfico porque la interfaz es la equivocada.** Si estás en WiFi, captura `wlan0`, no
  `enp3s0`.
- **Capturar sin permisos.** Con `sudo` funciona; sin él, tu usuario debe estar en el grupo
  `wireshark`.
- **Esperar ver datos de HTTPS.** Está cifrado: solo verás el handshake TLS.
- **Aplicar filtros de captura demasiado pronto.** Si descartas algo, ya no lo recuperas: captura amplio
  y filtra después.
- **Asumir que Wireshark "ve Internet".** Solo ve el tráfico que pasa por **tu** interfaz (o la red
  local en modo promiscuo con switches, muy limitado). No es magia.

## Ejercicios

### Ejercicio 1

¿Qué diferencia hay entre un filtro de captura y uno de visualización?

??? success "Solución"
    El de **captura** decide **antes** qué se guarda (lo descartado se pierde) y usa sintaxis **BPF**
    (`tcp port 80`). El de **visualización** decide **después** qué se muestra, es reversible y usa la
    sintaxis de Wireshark (`tcp.port == 80`).

### Ejercicio 2

Escribe un filtro de visualización para ver solo tráfico del puerto 443.

??? success "Solución"
    `tcp.port == 443`. (Si quisieras capturarlo: filtro de captura `tcp port 443`.)

### Ejercicio 3

Quieres ver solo los paquetes **SYN** sin ACK (inicios de conexión). ¿Qué filtro usas?

??? success "Solución"
    `tcp.flags.syn == 1 && tcp.flags.ack == 0`.

### Ejercicio 4

Describe los tres paquetes del three-way handshake tal como los etiqueta Wireshark.

??? success "Solución"
    1. `[SYN]` del cliente (`Seq=...`).
    2. `[SYN, ACK]` del servidor (`Ack=` confirma el SYN del cliente).
    3. `[ACK]` del cliente. Conexión **ESTABLISHED**.

### Ejercicio 5

En una consulta DNS capturada, ¿qué campo relaciona la pregunta con su respuesta?

??? success "Solución"
    El **Transaction ID** (por ejemplo `0x1a2b`). La respuesta lleva el mismo ID que la pregunta.

### Ejercicio 6

¿Por qué en una captura de HTTPS no ves la petición `GET` en claro?

??? success "Solución"
    Porque HTTPS cifra el contenido con **TLS**. Wireshark ve la cabecera TCP y el handshake TLS, pero
    el HTTP va dentro del canal cifrado y no es legible.

### Ejercicio 7

Estás en WiFi y no capturas nada. ¿Qué revisas primero?

??? success "Solución"
    Que estás capturando en la **interfaz correcta** (`wlan0` para WiFi, no la Ethernet), que la
    captura está **iniciada** y que tienes **permisos** (usuario en el grupo `wireshark` o ejecutar con
    `sudo`).

## Resumen

- Wireshark captura y muestra el tráfico **por capas**: Ethernet → IP → TCP/UDP → aplicación.
- Los **filtros de captura** (BPF, antes) reducen lo que se guarda; los de **visualización** (sintaxis
  Wireshark, después) deciden lo que se ve.
- El **three-way handshake** (SYN, SYN-ACK, ACK) se ve claramente con `tcp.flags.syn == 1`.
- El **DNS** clásico va en claro; DoT/DoH lo cifran.
- **HTTP** en claro se lee entero; **HTTPS** no (solo el handshake TLS).
- **Follow TCP/HTTP Stream** reconstruye el diálogo completo.

## Checklist

- [ ] He instalado Wireshark y capturado en la interfaz correcta.
- [ ] Distingo filtro de captura y de visualización.
- [ ] Escribo filtros como `tcp.port == 80`, `dns`, `http.request.method == "GET"`.
- [ ] Identifico el handshake TCP en una captura.
- [ ] Analizo una consulta DNS y localizo la IP de respuesta.
- [ ] Veo una petición HTTP y comparo con una HTTPS cifrada.
- [ ] Sé usar "Follow TCP/HTTP Stream".

## Para ir más allá

- **Wireshark (web oficial)** — descargas, documentación y la wiki. Tipo: herramienta ·
  Inglés (EN) · **Gratis**. <https://www.wireshark.org>
- **`tshark`** — la versión de línea de comandos de Wireshark, útil para automatizar. Tipo:
  herramienta · Inglés (EN) · **Gratis**. Incluido con Wireshark; consúltalo en
  <https://www.wireshark.org>.
- **RFC 9110 (HTTP Semantics)** — para entender las cabeceras que veas en las capturas. Tipo:
  documentación oficial · Inglés (EN) · **Gratis**. <https://www.rfc-editor.org>
- **TryHackMe** y **Hack The Box** — salas/máquinas donde practicar análisis de tráfico.
  Tipo: plataforma · Inglés (EN) · **Freemium**. <https://tryhackme.com> ·
  <https://www.hackthebox.com>

## Siguiente paso

¡Has terminado el módulo de Redes! El siguiente paso es conocer los sistemas con los que trabajarás
cada día: sigue con **[03 · Sistemas operativos](../03-sistemas-operativos/index.md)**.
