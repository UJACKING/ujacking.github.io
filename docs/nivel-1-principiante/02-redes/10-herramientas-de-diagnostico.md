# Herramientas de diagnóstico

**Resumen.** Saber diagnosticar es lo que separa a quien "sabe teoría" de quien resuelve problemas.
Esta página reúne las herramientas de línea de comandos que usarás a diario en redes y en seguridad:
`ip`, `ping`, `traceroute`, `nslookup`/`dig`, `ss`, `curl`, `nc`, `arp` y `whois`, con ejemplos de
comando y su salida explicada línea a línea.

## Objetivos de aprendizaje

- Diagnosticar la configuración de red con `ip`.
- Comprobar conectividad y ruta con `ping` y `traceroute`.
- Resolver y consultar DNS con `nslookup` y `dig`.
- Ver puertos y conexiones con `ss`.
- Interactuar con servicios con `curl` y `nc`.
- Consultar la caché ARP y datos de dominios con `arp` y `whois`.

**Tiempo estimado: 60–90 min**

## Requisitos previos

- **[05 · Capa de red](05-capa-de-red.md)** y **[06 · Capa de transporte](06-capa-de-transporte.md)**:
  entenderás mejor qué hacen `ping`, `traceroute` y `ss`.
- **[07 · Protocolos de aplicación](07-protocolos-de-aplicacion.md)**: `dig`, `curl` y `whois` tocan DNS
  y HTTP.

!!! danger "Recordatorio ético"
    Estas herramientas son **legítimas y cotidianas** para diagnosticar tus propios sistemas. Usarlas
    contra equipos o redes **ajenas** (escaneos, `nc`, `whois` masivo…) sin autorización puede ser
    ilegal. Limítate a tu equipo, tu red de laboratorio y plataformas que lo permiten. Ver
    **[00 · Ética y legalidad](../00-etica-y-legalidad.md)**.

## Explicación

### Familias de herramientas

| Herramienta | Para qué sirve |
| --- | --- |
| **`ip`** | Ver y configurar interfaces, direcciones y rutas. |
| **`ping`** | Comprobar si un host responde y medir latencia. |
| **`traceroute`** | Ver por qué routers pasa el tráfico hasta el destino. |
| **`nslookup` / `dig`** | Consultar DNS. |
| **`ss`** | Ver sockets, puertos a la escucha y conexiones. |
| **`curl`** | Hacer peticiones HTTP/FTP y ver respuestas. |
| **`nc`** (netcat) | Leer/escribir en conexiones TCP/UDP; probar puertos. |
| **`arp`** | Ver la tabla ARP (la caché IP↔MAC). |
| **`whois`** | Consultar el registro de un dominio o una IP. |

!!! tip "Comprobaciones en orden"
    Ante "no tengo red", sigue este orden: 1) `ip a` (¿tengo IP?), 2) `ping` a la puerta de enlace
    (¿llego al router?), 3) `ping` a una IP externa como `1.1.1.1` (¿hay salida?), 4) `dig` (¿resuelve
    nombres?). Así aíslas el problema por capas.

### Detalle: `ping` y `traceroute` con IPv4/IPv6

- `ping` usa ICMP. Si no hay respuesta, puede ser firewall, no necesariamente un host caído.
- En Linux, `ping` **no para solo**: usa `-c N` para enviar N paquetes.
- `traceroute` incrementa el TTL para descubrir hops; los `*` indican routers que no responden.

### Detalle: `nc` (netcat)

`nc` es la "navaja suiza" de TCP/UDP. Sirve para:

- Probar si un puerto está abierto (`nc -vz host puerto`).
- Conectar a un servicio y hablar con él a mano.
- Transferir datos entre equipos (con autorización).

Su potencia es también su peligro: por eso solo se usa en laboratorio propio.

## Ejemplos prácticos

A partir de aquí, todas las salidas van etiquetadas como **"(salida de ejemplo)"** cuando pueden variar
según tu red, tu versión o el host consultado.

### `ip` — configuración de red

```bash
ip -brief address
```

Salida de ejemplo:

```text
lo               UNKNOWN        127.0.0.1/8 ::1/128
enp3s0           UP             192.168.1.50/24 fe80::1a2b:3c4d:5e6f:7a8b/64
```

- `lo`: loopback. `enp3s0`: tu interfaz principal.
- `192.168.1.50/24`: tu IPv4 y prefijo. `fe80::.../64`: tu IPv6 link-local. **(salida de ejemplo)**

Tabla de rutas:

```bash
ip route
```

Salida de ejemplo:

```text
default via 192.168.1.1 dev enp3s0
192.168.1.0/24 dev enp3s0 proto kernel scope link src 192.168.1.50
```

- La **ruta por defecto** (`default via`) apunta a tu puerta de enlace. **(salida de ejemplo)**

### `ping` — conectividad y latencia

```bash
ping -c 3 1.1.1.1
```

Salida de ejemplo:

```text
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=57 time=12.4 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=57 time=12.1 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=57 time=12.6 ms
--- 1.1.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
```

- `-c 3`: solo 3 paquetes.
- `ttl=57`: saltos restantes de la respuesta.
- `time=12.4 ms`: RTT. `0% packet loss`: ninguno se perdió. **(salida de ejemplo)**

### `traceroute` — la ruta hasta el destino

```bash
traceroute example.com
```

Salida de ejemplo:

```text
traceroute to example.com (93.184.216.34), 30 hops max, 60 byte packets
 1  _gateway (192.168.1.1)  0.42 ms  0.40 ms  0.51 ms
 2  10.0.0.1 (10.0.0.1)  6.21 ms  6.10 ms  6.30 ms
 3  93.184.216.34 (93.184.216.34)  12.55 ms  12.10 ms  12.88 ms
```

Cada número es un **hop** (router). `* * *` sería un router que no responde a ICMP.
**(salida de ejemplo)**. En Windows el comando es `tracert`.

### `nslookup` y `dig` — DNS

```bash
nslookup example.com
```

Salida de ejemplo:

```text
Server:		192.168.1.1
Address:	192.168.1.1#53

Non-authoritative answer:
Name:	example.com
Address: 93.184.216.34
```

- `Server`: el resolutor consultado. `Non-authoritative answer`: viene de caché. **(salida de ejemplo)**

```bash
dig example.com A +short
```

Salida de ejemplo:

```text
93.184.216.34
```

`dig` es más detallado por defecto y más cómodo para scripting. Prueba también
`dig MX ejemplo.com` (correo) o `dig AAAA ejemplo.com` (IPv6). **(salida de ejemplo)**

### `ss` — puertos y conexiones

```bash
ss -tuln
```

Salida de ejemplo:

```text
Netid State  Local Address:Port   Peer Address:Port
udp   UNCONN 0.0.0.0:68            0.0.0.0:*
tcp   LISTEN 0.0.0.0:22            0.0.0.0:*
tcp   LISTEN 127.0.0.1:631         0.0.0.0:*
```

- `-t` TCP, `-u` UDP, `-l` escuchas, `-n` números.
- `0.0.0.0:22` escucha en todas las interfaces; `127.0.0.1:631` solo en local. **(salida de ejemplo)**

### `curl` — peticiones HTTP

```bash
curl -I https://example.com
```

Salida de ejemplo:

```text
HTTP/1.1 200 OK
Content-Type: text/html; charset=UTF-8
Content-Length: 1256
```

`-I` pide solo cabeceras (HEAD). Para ver el cuerpo, quita `-I`. Para seguir redirecciones, añade `-L`.
**(salida de ejemplo)**

### `nc` (netcat) — hablar con un servicio

```bash
nc -vz example.com 443
```

Salida de ejemplo:

```text
Connection to example.com 443 port [tcp/https] succeeded!
```

- `-z`: modo "escaneo" (no envía datos), `-v`: verboso.
- Sirve para comprobar si un **puerto** acepta conexiones. **(salida de ejemplo)**

!!! warning "Sobre `nc` y el escaneo"
    `nc -vz` contra máquinas **ajenas** es escaneo de puertos y requiere autorización. Úsalo solo en tu
    laboratorio o contra hosts que te pertenezcan.

### `arp` — tabla ARP

```bash
arp -n
```

Salida de ejemplo:

```text
Address                  HWtype  HWaddress           Flags Mask   Iface
192.168.1.1              ether   aa:bb:cc:dd:ee:01   C            enp3s0
192.168.1.20             ether   aa:bb:cc:dd:ee:02   C            enp3s0
```

Muestra la caché **IP ↔ MAC**. `arp` está en desuso en Linux a favor de `ip neigh`, que da lo mismo con
otro formato. **(salida de ejemplo)**

### `whois` — datos de un dominio o IP

```bash
whois example.com
```

Salida de ejemplo (recortada):

```text
Domain Name: EXAMPLE.COM
Registrar: ...
Creation Date: ...
Name Server: A.IANA-SERVERS.NET
```

Muestra el **registro** del dominio: registrador, fechas y servidores de nombres. La salida varía según
el registro de cada TLD. **(salida de ejemplo)**

## Errores comunes

- **Usar el `ping` de Windows y esperar a que pare.** `ping` en Windows hace 4 por defecto; en Linux
  no para sin `-c`.
- **Concluir que un host está caído por no responder a ping.** Puede filtrar ICMP.
- **Confundir `ss` con `netstat`.** `ss` es el sucesor moderno y más rápido.
- **Olvidar `-L` en `curl`.** Sin ella, no sigues redirecciones (verás el 301/302).
- **Creer que `whois` es una "base de datos de propietarios".** Según el TLD y las leyes de privacidad,
  muchos datos están ocultos; sirve para el registro técnico, no para identificar personas.
- **Usar `nc` contra terceros.** Es escaneo; necesita autorización.

## Ejercicios

### Ejercicio 1

Quieres comprobar si tienes IP y cuál es tu puerta de enlace. ¿Qué dos comandos ejecutas?

??? success "Solución"
    `ip -brief address` (o `ip a`) para ver tu IP, y `ip route` para ver la **ruta por defecto**
    (`default via ...`), que es tu puerta de enlace.

### Ejercicio 2

Tu equipo navega, pero `ping 1.1.1.1` falla. ¿Qué conclusión sacas?

??? success "Solución"
    **Ninguna definitiva:** Wikipedia navega, así que hay conectividad; probablemente el ICMP esté
    **filtrado** o bloqueado en algún punto. La ausencia de respuesta a ping no implica falta de red.

### Ejercicio 3

¿Qué comando usarías para ver qué puertos TCP están a la escucha en tu equipo?

??? success "Solución"
    `ss -tln` (TCP, escuchas, números). Añade `-u` (`ss -tuln`) si quieres incluir UDP.

### Ejercicio 4

Quieres ver solo las cabeceras de la respuesta de `https://example.com`. Escribe el comando.

??? success "Solución"
    `curl -I https://example.com`. La opción `-I` hace una petición **HEAD**, que devuelve solo las
    cabeceras.

### Ejercicio 5

¿Qué devuelve `dig example.com A +short` y en qué se diferencia de `nslookup`?

??? success "Solución"
    Devuelve la **dirección IPv4** del dominio (el registro **A**), de forma resumida. `nslookup`
    muestra además el servidor consultado y si la respuesta es autoritativa o de caché; `dig` es más
    detallado por defecto y más cómodo de usar en scripts.

### Ejercicio 6

¿Para qué sirve `arp -n` y cuál es su equivalente moderno en Linux?

??? success "Solución"
    Para ver la **caché ARP**, es decir, las correspondencias **IP ↔ MAC** de tu red local. El
    equivalente moderno es `ip neigh`.

### Ejercicio 7

Un compañero dice: "he hecho `nc -vz` a un servidor de la empresa y he visto los puertos abiertos".
¿Qué problema ético hay?

??? success "Solución"
    Que `nc -vz` es un **escaneo de puertos**. Sin **autorización** explícita de la empresa, hacerlo
    contra su infraestructura puede incumplir sus normas y ser ilegal. En un trabajo real, estas pruebas
    se hacen solo con **contrato/permiso** y en plataformas o entornos autorizados.

## Resumen

- **`ip`**: interfaces, direcciones y rutas (`ip a`, `ip route`).
- **`ping`**: conectividad y latencia (usa `-c` en Linux).
- **`traceroute`**: ruta por hops (Windows: `tracert`).
- **`nslookup`/`dig`**: consultas DNS (`A`, `AAAA`, `MX`…).
- **`ss`**: puertos a la escucha y conexiones.
- **`curl`**: peticiones HTTP y sus cabeceras.
- **`nc`**: hablar con servicios y probar puertos (solo con autorización).
- **`arp`**: caché IP↔MAC (equivalente moderno: `ip neigh`).
- **`whois`**: registro de dominios/IP (datos limitados por privacidad).

## Checklist

- [ ] Veo mi IP y mi ruta por defecto con `ip`.
- [ ] Compruebo conectividad con `ping` e interpreto el TTL y el RTT.
- [ ] Trazo la ruta con `traceroute`.
- [ ] Resuelvo nombres con `nslookup` y `dig`.
- [ ] Listo puertos y conexiones con `ss`.
- [ ] Hago una petición y veo cabeceras con `curl`.
- [ ] Comprendo para qué sirve `nc` y sus límites éticos.
- [ ] Consulto `arp`/`ip neigh` y `whois`.

## Para ir más allá

- **`man7.org`** — páginas de manual de `ip`, `ss`, `ping`, `traceroute`, `dig`, `curl`, `nc`. Tipo:
  documentación · Inglés (EN) · **Gratis**. <https://man7.org>
- **DNS**: RFC 1035 — especificación del sistema de nombres. Tipo: documentación oficial ·
  Inglés (EN) · **Gratis**. <https://www.rfc-editor.org>
- **Wireshark** — complemento perfecto: ves lo que estos comandos hacen por dentro. Tipo: herramienta ·
  Inglés (EN) · **Gratis**. <https://www.wireshark.org>
- **TryHackMe** — salas de redes para practicar comandos guiados. Tipo: plataforma · Inglés (EN) ·
  **Freemium**. <https://tryhackme.com>

## Siguiente paso

Para terminar el módulo, sube el nivel de observación: aprende a **capturar y analizar** tráfico real
con **[11 · Wireshark](11-wireshark.md)**.
