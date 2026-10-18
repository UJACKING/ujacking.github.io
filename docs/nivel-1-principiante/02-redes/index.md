# 02 · Redes

**Todo en ciberseguridad pasa por una red.** Si no entiendes cómo viajan los datos, no puedes
entender cómo se interceptan, cómo se filtran ni por qué un firewall bloquea lo que bloquea. Este
módulo te da esa base, desde cero y sin dar nada por supuesto.

Empezamos por los modelos OSI y TCP/IP, seguimos con direcciones y **subnetting** (el tema estrella
del módulo), bajamos por las capas de enlace, red y transporte, subimos a los protocolos de
aplicación, y terminamos capturando tráfico real con Wireshark. Al acabar sabrás leer una captura,
calcular una subred a mano y explicar qué ocurre entre que pulsas Enter y ves una web.

## ¿Qué vas a aprender aquí?

| # | Página | De qué va |
| --- | --- | --- |
| 0 | **[Portada del módulo](index.md)** | Esta página: orden de estudio y consejos. |
| 1 | **[Modelos OSI y TCP/IP](01-modelos-osi-y-tcp-ip.md)** | Las 7 capas, las 4 capas y cómo se encapsula un paquete. |
| 2 | **[Direccionamiento IP y MAC](02-direccionamiento-ip-y-mac.md)** | IPv4, IPv6, MAC y por qué hay una dirección lógica y otra física. |
| 3 | **[Subnetting](03-subnetting.md)** | Máscaras, CIDR, VLSM y 15+ ejercicios resueltos. **La página clave.** |
| 4 | **[Capa de enlace](04-capa-de-enlace.md)** | Ethernet, tramas, switches, ARP y ARP spoofing. |
| 5 | **[Capa de red](05-capa-de-red.md)** | Routers, tablas de rutas, NAT/PAT, ICMP y TTL. |
| 6 | **[Capa de transporte](06-capa-de-transporte.md)** | TCP, UDP, handshake, puertos y estados de conexión. |
| 7 | **[Protocolos de aplicación](07-protocolos-de-aplicacion.md)** | DNS, HTTP, DHCP, SSH, SMB y compañía: puerto, función y seguridad. |
| 8 | **[Seguridad en tránsito](08-seguridad-en-transito.md)** | TLS, certificados, cifrado simétrico/asimétrico, hashing y VPN. |
| 9 | **[Dispositivos, topologías y WiFi](09-dispositivos-topologias-y-wifi.md)** | Firewall, proxy, IDS/IPS, DMZ, topologías y seguridad WiFi. |
| 10 | **[Herramientas de diagnóstico](10-herramientas-de-diagnostico.md)** | `ip`, `ping`, `traceroute`, `dig`, `ss`, `curl`, `nc`, `whois`. |
| 11 | **[Wireshark](11-wireshark.md)** | Captura y análisis real de TCP, DNS y HTTP. |

## Orden recomendado

1. **Modelos OSI/TCP-IP.** Te da el mapa mental de todo el módulo.
2. **Direccionamiento.** Sin entender una IP y una MAC, el subnetting no tiene sentido.
3. **Subnetting.** Dedícale el tiempo que haga falta. Es la base de redes y de pentesting.
4. **Capas de enlace, red y transporte.** Cómo funciona cada salto del paquete.
5. **Protocolos de aplicación.** A qué puerto y de qué forma hablan los servicios reales.
6. **Seguridad en tránsito.** Cómo se protege la información mientras viaja.
7. **Dispositivos, topologías y WiFi.** Cómo se organiza y se defiende una red.
8. **Diagnóstico y Wireshark.** Pon a prueba y ve todo lo anterior con tus propios ojos.

## Cómo estudiar este módulo

- **Dibuja.** Una subred mal calculada suele venir de no haber dibujado los bloques. Coge papel.
- **Haz los ejercicios antes de mirar la solución.** El subnetting solo se aprende calculando.
- **Toca la terminal.** Los comandos de la página de diagnóstico se ejecutan, no se leen.
- **Captura tu propio tráfico.** Con Wireshark entenderás el handshake TCP mejor que con cualquier texto.

!!! tip "Consejo de laboratorio"
    Para el subnetting y el diagnóstico no necesitas nada especial. Para Wireshark, practica en tu
    propia red o, mejor, en una máquina virtual de laboratorio. Más adelante montarás el entorno
    completo en el módulo de Sistemas operativos.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Revisar el índice de este módulo cuando se publiquen las páginas de otros niveles, para añadir
    enlaces cruzados a Nivel 2 · Redes avanzadas y firewalls.

## Requisitos previos

- Saber usar un navegador y moverte por ficheros y carpetas. Poco más.
- Idealmente haber leído **[01 · Arquitectura de ordenadores](../01-arquitectura-de-ordenadores/index.md)**,
  que explica conceptos como bit, byte y binario que aquí se usan a diario.
- Leer antes **[00 · Ética y legalidad](../00-etica-y-legalidad.md)**: la parte ofensiva de este módulo
  (ARP spoofing) es solo teórica y requiere autorización.

## Siguiente paso

Empieza por **[01 · Modelos OSI y TCP/IP](01-modelos-osi-y-tcp-ip.md)**. Es el mapa del módulo: ténlo
a mano mientras estudias el resto.
