# Hardware e IoT

La **seguridad de hardware e IoT** (Internet of Things) trabaja con lo que puedes tocar: routers,
cámaras, cerraduras, wearables, dispositivos industriales, placas y *firmware*. Es un área de nicho muy
divertida porque mezcla **electrónica, redes, análisis de firmware e ingeniería inversa**.

Muchos dispositivos IoT son pequeños ordenadores con Linux, firmware sin firmar y servicios expuestos: un
campo enorme de aprendizaje y una de las puertas más directas de entrada a la **seguridad industrial (ICS/OT)**.

!!! warning "Solo tu hardware o con autorización"
    Manipular, extraer firmware o atacar un dispositivo ajeno es intrusión. Practica **solo** con
    hardware **tuyo**, de laboratorio o en auditorías con autorización por escrito. Muchos dispositivos
    están en producción detrás de vidas humanas: nunca pruebes contra infraestructura crítica real.

## Cómo es el día a día

| Bloque | Qué haces |
| --- | --- |
| **Reconocimiento** | Localizas el dispositivo, sus puertos y servicios (Nmap, Shodan/Censys). |
| **Acceso físico** | Encuentras **UART/JTAG/SWD**, sueldas pines y consigues consola de depuración. |
| **Extracción de firmware** | Lo sacas por SPI flash, UART o del propio firmware de actualización. |
| **Análisis de firmware** | Desempaquetas con **binwalk**, buscas secretos, claves y binarios vulnerables. |
| **Emulación** | Ejecutas partes con **QEMU** o **Firmadyne** para probar sin el dispositivo. |
| **Radio / protocolos** | Analizas BLE, Zigbee, Wi-Fi y RF con SDR y herramientas específicas. |
| **Informe** | Documentas el impacto y las mitigaciones, a menudo contra normas del sector. |

Herramientas típicas: **bus-pirate**, **JTAGulator**, **Logic analyzer**, **binwalk**, **Ghidra**,
**Wireshark**, **Shodan** y, en la parte industrial, análisis de protocolos como **Modbus**.

## Habilidades clave

- **Electrónica básica**: voltaje, tierra, multímetro, soldadura, lectura de datasheets.
- **Linux embebido**: U-Boot, busybox, sistemas de ficheros, *overlay*.
- **Redes y radio**: TCP/IP, HTTP, MQTT, BLE, Zigbee.
- **Análisis de firmware**: `binwalk`, `firmware-mod-kit`, extracción de imágenes.
- **Ingeniería inversa** con **Ghidra**: [ghidra-sre.org](https://ghidra-sre.org).
- **Emulación** con QEMU: [qemu.org](https://www.qemu.org).
- **Estándares OWASP IoT** y **OWASP FSTM** (metodología de pruebas de firmware) en [owasp.org](https://owasp.org).
- **Pensamiento de sistema completo**: dispositivo + app + nube + radio.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Aprende **electrónica básica** y Linux embebido: refuerza [Nivel 1 · Principiante](../nivel-1-principiante/index.md).
2. Consigue un dispositivo de laboratorio barato (router viejo, placa de desarrollo como **Raspberry Pi** o **Arduino**): [raspberrypi.com](https://www.raspberrypi.com) · [arduino.cc](https://www.arduino.cc) **(EN, Freemium)**.
3. Escanea tu propio dispositivo y entiende sus puertos y servicios (Nmap, Wireshark).
4. Lee el **OWASP IoT Top 10** en [owasp.org](https://owasp.org) **(EN, Gratis)**.
5. Haz tu primer *teardown* y busca pines de depuración (UART).

### Fase 2 · Medio (3–12 meses)

1. Aprende a usar **UART/JTAG/SWD** con un adaptador USB-serie y una **bus pirate** o **JTAGulator**.
2. Extrae y **desempaqueta firmware** con **binwalk** (escríbelo tú: instálalo desde [github.com](https://github.com) y practica con tus imágenes).
3. Analiza binarios en **Ghidra** y busca secretos, claves y servicios.
4. **Emula** con QEMU y prueba vulnerabilidades sin riesgo en el dispositivo real.
5. Sube a **Shodan/Censys** para ver cuánta exposición hay "ahí fuera": [shodan.io](https://www.shodan.io) · [censys.com](https://censys.com) **(EN, Freemium)**.

### Fase 3 · Avanzado (12 meses+)

1. Domina **radio**: BLE, Zigbee y RF con SDR (RTL-SDR, HackRF).
2. Entra en **ICS/OT**: protocolos industriales (Modbus, PROFINET), normas y *purdue model*.
3. Analiza *secure boot*, cifrado de firmware, *fuses* y contramedidas de ataque físico.
4. Automatiza fuzzing de firmware y protocolos en un pipeline.
5. Investiga y publica (con divulgación responsable), o compite en retos de hardware en CTF.

## Recursos gratuitos

### Estándares y documentación

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| OWASP IoT Top 10 | Guía | EN | Gratis | [owasp.org](https://owasp.org) |
| OWASP FSTM (pruebas de firmware) | Metodología | EN | Gratis | [owasp.org](https://owasp.org) |
| Ghidra | Herramienta | EN | Gratis | [ghidra-sre.org](https://ghidra-sre.org) |
| Wireshark | Herramienta | EN | Gratis | [wireshark.org](https://www.wireshark.org) |
| QEMU (emulación) | Herramienta | EN | Gratis | [qemu.org](https://www.qemu.org) |
| Shodan / Censys | Búsqueda de dispositivos | EN | Freemium | [shodan.io](https://www.shodan.io) · [censys.com](https://www.censys.com) |
| FCC ID (datasheets y fotos internas) | Base de datos | EN | Gratis | [fcc.gov](https://www.fcc.gov) |
| Hackaday (proyectos y teardowns) | Blog/Comunidad | EN | Gratis | [hackaday.com](https://hackaday.com) |

### Cursos y laboratorios

- **TryHackMe** y **Hack The Box** tienen salas de introducción a IoT y *hardware hacking*: [tryhackme.com](https://tryhackme.com) · [hackthebox.com](https://www.hackthebox.com) **(EN, Freemium)**.
- **Hackaday** y comunidades maker para aprender electrónica e ingeniería práctica **(EN, Gratis)**.
- **OWASP** guías y proyectos IoT/FSTM: [owasp.org](https://owasp.org) **(EN, Gratis)**.
- **SANS** *ICS* y recursos de seguridad industrial (parte gratuita): [sans.org](https://www.sans.org) **(EN, Freemium)**.
- TODO-UJACKING: verificar y enlazar cursos/laboratorios de hardware hacking en español vigentes.

### Vídeos

- **LiveOverflow** — análisis de bajo nivel y firmware: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.
- **John Hammond** — retos de hardware e IoT: [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
- **Hackaday** publica charlas y *supercon* en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlaces verificados.

## Certificaciones habituales

No hay una certificación única y universal de "IoT"; según el sector (industrial, redes, ofensiva):

- **GICSP** (Global Industrial Cyber Security Professional) — SANS/GIAC · [giac.org](https://www.giac.org).
- **GRID** (GIAC Response and Industrial Defense) — SANS/GIAC · [giac.org](https://www.giac.org).
- **OSCP** para la base ofensiva general: [offsec.com](https://www.offsec.com).
- **CompTIA Security+** como entrada: [comptia.org](https://www.comptia.org).
- TODO-UJACKING: identificar certificaciones específicas de IoT/hardware reconocidas por el mercado y enlazar su web oficial.

## Salidas laborales

- **IoT Security Analyst / Engineer**.
- **Embedded Security Engineer** (firmware seguro en fabricantes).
- **ICS/OT Security Engineer** (seguridad industrial, sector crítico).
- **Hardware Penetration Tester** (auditorías de dispositivos).
- **Investigador/a en laboratorios de seguridad de hardware**.
- Puente a **análisis de malware y engineering inversa**: [Análisis de malware e ingeniería inversa](analisis-de-malware-e-ingenieria-inversa.md).

Es un área muy técnica y de nicho, con menos posiciones pero menos competencia. Combina bien con
[Seguridad móvil](seguridad-movil.md) y con [Cloud security](cloud-security.md). Ver
[Empleabilidad](../empleabilidad/index.md).

## Siguiente paso

- Refuerza los fundamentos: [Nivel 1 · Principiante](../nivel-1-principiante/index.md).
- Áreas cercanas: [Seguridad móvil](seguridad-movil.md) · [Análisis de malware e ingeniería inversa](analisis-de-malware-e-ingenieria-inversa.md).
- Índice de áreas: [Paths](index.md).
