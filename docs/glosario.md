# Glosario de ciberseguridad (A–Z)

**Resumen.** Los términos que más te vas a encontrar en el [Nivel 1 · Principiante](nivel-1-principiante/index.md)
y algunos del [Nivel 2 · Medio](nivel-2-medio/index.md), explicados en español y sin rodeos. El término
técnico se deja en inglés cuando es lo habitual (switch, firewall, payload…), pero la explicación siempre
va en castellano.

## Cómo usar este glosario

- No lo leas de corrido: **consúltalo** cuando te topes con una palabra rara.
- Los términos marcados **(Nivel 2)** los verás más adelante; aquí tienes la idea general para no perderte.
- Si una definición te sabe a poco, salta a la página del tema (normalmente está en el
  [Nivel 1](nivel-1-principiante/index.md)) y amplía.
- Este glosario es un apoyo de la [Ruta perfecta](ruta-perfecta.md): úsalo mientras estudias, no en lugar
  de estudiar.

## A

- **ACK (acknowledgement)**: mensaje de confirmación que una máquina envía para indicar que ha recibido
  datos correctamente. En TCP forma parte del *three-way handshake*.
- **Active Directory (AD)**: servicio de directorio de Microsoft que centraliza usuarios, equipos y
  permisos de una red Windows. Muy habitual como objetivo en pentesting. **(Nivel 2)**
- **Algoritmo**: conjunto ordenado y finito de pasos para resolver un problema. En criptografía define cómo
  se cifra o descifra.
- **APIPA (Automatic Private IP Addressing)**: mecanismo por el que un equipo **sin** servidor DHCP se
  asigna solo una dirección del rango `169.254.0.0/16`. Si ves una IP así, normalmente significa que no
  hay conexión con el DHCP.
- **ARP (Address Resolution Protocol)**: protocolo que traduce una dirección **IP** a la dirección **MAC**
  correspondiente dentro de una red local.
- **ASCII**: codificación que asigna un número a cada carácter latino básico (por ejemplo, la letra `A` es
  el 65).
- **Autenticación**: proceso de verificar que eres quien dices ser (usuario y contraseña, certificado,
  biometría…).
- **Autorización**: decidir qué puede hacer un usuario **ya** autenticado: qué ficheros lee, qué comandos
  ejecuta, a qué servicios accede.

## B

- **Backup (copia de seguridad)**: copia de los datos para poder recuperarlos si algo falla o es atacado.
- **Binario**: sistema de numeración en base 2, con solo los dígitos `0` y `1`. Es el lenguaje nativo de la
  electrónica digital.
- **BIOS (Basic Input/Output System)**: firmware clásico que inicializa el hardware y arranca el sistema
  operativo. En equipos modernos ha sido sustituido por UEFI.
- **Bit**: unidad mínima de información; vale `0` o `1`.
- **Boot (arranque)**: secuencia de inicio del ordenador, desde que se enciende hasta que carga el sistema
  operativo.
- **Broadcast (difusión)**: dirección o transmisión dirigida a **todos** los equipos de una red local. La
  dirección de broadcast de una red es la última del rango.
- **Bug bounty**: programa por el que una empresa paga a investigadores que reportan vulnerabilidades de
  forma responsable en lugar de explotarlas.
- **Byte**: grupo de **8 bits**. Es la unidad habitual para medir tamaño de datos.

## C

- **Cabecera (header)**: parte inicial de un paquete o mensaje que contiene metadatos (direcciones, puertos,
  *flags*…) y no los datos en sí.
- **Caché**: almacenamiento temporal y rápido de datos para acelerar accesos repetidos (por ejemplo, la
  caché DNS).
- **Checksum**: valor calculado sobre unos datos para detectar errores de transmisión o corrupción.
- **CIDR (Classless Inter-Domain Routing)**: notación que expresa una red con una IP y un prefijo de bits,
  como `192.168.1.0/24`.
- **Cifrado (criptografía)**: transformar la información para que solo quien tiene la clave pueda leerla.
- **Cifrado asimétrico**: usa un **par de claves**, una pública y otra privada (ejemplo: RSA).
- **Cifrado simétrico**: usa la **misma clave** para cifrar y descifrar; es más rápido (ejemplo: AES).
- **Cliente**: programa o máquina que solicita un servicio a un servidor.
- **Cookie**: pequeño dato que un servidor envía al navegador y este devuelve en cada petición; se usa para
  mantener sesiones y estado.
- **CPU (Central Processing Unit)**: unidad central de proceso; el «cerebro» que ejecuta las instrucciones.
- **CSRF (Cross-Site Request Forgery)**: ataque que obliga al navegador de una víctima autenticada a enviar
  una petición no deseada. **(Nivel 2)**
- **CVE (Common Vulnerabilities and Exposures)**: identificador público y único de una vulnerabilidad
  conocida, con el formato `CVE-AAAA-NNNN`.

## D

- **Dato**: información sin procesar; en seguridad, algo que puede tener valor y debe protegerse.
- **DDoS (Distributed Denial of Service)**: ataque de denegación de servicio lanzado desde **muchos**
  equipos a la vez para saturar un servicio.
- **DHCP (Dynamic Host Configuration Protocol)**: protocolo que asigna automáticamente direcciones IP y
  otros parámetros de red a los equipos.
- **DMZ (zona desmilitarizada)**: subred aislada donde se colocan los servicios expuestos a Internet para
  proteger la red interna.
- **DNS (Domain Name System)**: sistema que traduce nombres de dominio (`ejemplo.com`) a direcciones IP.

## E

- **Endianness**: orden en que se almacenan los bytes de un número en memoria: *big-endian* (primero el
  byte más significativo) o *little-endian* (primero el menos significativo).
- **Escalada de privilegios (privilege escalation)**: conseguir más permisos de los que se tenían,
  típicamente pasar de usuario normal a `root`/administrador. **(Nivel 2)**
- **Ethernet**: tecnología estándar de red de área local **cableada**.
- **Exploit**: código o técnica que aprovecha una vulnerabilidad para provocar un efecto no previsto por el
  diseño del sistema. **(Nivel 2)**

## F

- **Firewall (cortafuegos)**: dispositivo o software que filtra el tráfico según reglas, permitiendo o
  bloqueando conexiones.
- **Firmware**: software grabado en un componente de hardware (por ejemplo, el de la placa base).
- **Flag**: cadena secreta que confirma que has resuelto un reto en un CTF.
- **Forense digital**: disciplina de investigar y analizar evidencias digitales tras un incidente.
- **FTP (File Transfer Protocol)**: protocolo clásico para transferir ficheros. Envía las credenciales sin
  cifrar; hoy se prefieren SFTP o FTPS.
- **Fuerza bruta (brute force)**: probar sistemáticamente muchas combinaciones de contraseñas o claves hasta
  acertar.
- **Fuzzing**: enviar datos aleatorios o malformados a un programa para encontrar fallos. **(Nivel 2)**

## G

- **Gateway (puerta de enlace)**: dispositivo (normalmente el router) por el que sale el tráfico hacia otras
  redes.
- **Git**: sistema de control de versiones que registra el historial de cambios de un proyecto.
- **GPO (Group Policy Object)**: objeto de directiva de grupo en Windows que aplica configuraciones a
  usuarios y equipos de un dominio. **(Nivel 2)**

## H

- **Hacker**: persona con gran conocimiento técnico. El *hacker ético* (sombrero blanco) usa ese
  conocimiento con autorización; el de *sombrero negro* lo usa para delinquir.
- **Hash (función resumen)**: función que convierte datos de cualquier tamaño en una huella de tamaño fijo
  e irreversible (ejemplo: SHA-256).
- **Heap (montón)**: zona de memoria dinámica que un programa reserva y libera en tiempo de ejecución.
- **Honeypot**: sistema trampa diseñado para atraer y estudiar a los atacantes.
- **Host**: cualquier dispositivo conectado a una red (ordenador, servidor, móvil, impresora…).
- **HTTP (HyperText Transfer Protocol)**: protocolo de la web para pedir y recibir recursos; viaja **sin**
  cifrar.
- **HTTPS**: HTTP sobre TLS, lo que cifra y protege la integridad de la comunicación con la web.

## I

- **ICMP (Internet Control Message Protocol)**: protocolo de mensajes de control y error de red; es el que
  usan `ping` y `traceroute`.
- **IDS (Intrusion Detection System)**: sistema que **detecta** actividad sospechosa y avisa, pero no la
  bloquea.
- **IMAP (Internet Message Access Protocol)**: protocolo para consultar el correo dejándolo en el servidor y
  sincronizar las carpetas.
- **Interfaz de red**: conexión lógica o física por la que un equipo envía y recibe tráfico (por ejemplo,
  `eth0` o `wlan0`).
- **IOC (Indicator of Compromise)**: pista observable de una intrusión (un hash de malware, una IP, un
  dominio…). **(Nivel 2)**
- **IP (Internet Protocol)**: protocolo de capa de red que direcciona y enruta paquetes entre redes.
- **IPS (Intrusion Prevention System)**: como un IDS, pero además puede **bloquear** la actividad detectada.
- **IPv4**: versión de IP de 32 bits (por ejemplo, `192.168.1.10`).
- **IPv6**: versión de IP de 128 bits, con un espacio de direcciones muchísimo mayor.

## J

- **Jitter**: variación del retardo entre paquetes; afecta sobre todo a voz y vídeo en tiempo real.
- **JSON (JavaScript Object Notation)**: formato de texto ligero para intercambiar datos, muy usado en APIs
  web.

## K

- **Kali Linux**: distribución Linux orientada a pruebas de seguridad y pentesting.
- **Kerberos**: protocolo de autenticación basado en *tickets*, usado por Active Directory. **(Nivel 2)**
- **Kernel (núcleo)**: parte central del sistema operativo; gestiona memoria, procesos, ficheros y hardware.
- **Kill chain (cadena de ataque)**: modelo que describe las fases de un ataque (reconocimiento, armado,
  entrega, explotación, instalación, mando y control, acciones sobre el objetivo).

## L

- **LAN (Local Area Network)**: red de área local; normalmente una casa, una oficina o tu laboratorio.
- **Latencia**: tiempo que tarda un paquete en ir y volver; se mide en milisegundos.
- **LDAP (Lightweight Directory Access Protocol)**: protocolo para consultar y modificar servicios de
  directorio, como Active Directory.
- **LFI (Local File Inclusion)**: vulnerabilidad web que permite leer ficheros del servidor a través de la
  aplicación. **(Nivel 2)**
- **Linux**: familia de sistemas operativos de código abierto basados en el kernel Linux.
- **Log (registro)**: fichero donde el sistema o una aplicación anotan eventos; clave para investigar
  incidentes.
- **Loopback**: interfaz especial que apunta al propio equipo (`127.0.0.1` en IPv4).

## M

- **MAC (Media Access Control)**: dirección física de 48 bits de una interfaz de red, expresada en
  hexadecimal (por ejemplo, `00:1a:2b:3c:4d:5e`).
- **Malware**: software malicioso (virus, gusanos, troyanos, ransomware…).
- **Máscara de subred**: número que indica qué bits de una dirección IP identifican la **red** y cuáles el
  **host** (por ejemplo, `255.255.255.0`).
- **Metasploit**: framework muy usado para desarrollar y ejecutar exploits en laboratorio. **(Nivel 2)**
- **MFA (autenticación multifactor)**: combinar dos o más factores distintos (algo que sabes, tienes o eres)
  para iniciar sesión.
- **MITM (Man-in-the-Middle)**: ataque en el que el atacante se coloca en medio de dos partes y puede leer o
  modificar su tráfico.

## N

- **NAT (Network Address Translation)**: traducción de direcciones privadas a una pública (y viceversa) para
  salir a Internet.
- **Netcat (nc)**: utilidad de red para leer y escribir datos por TCP/UDP; sirve para depurar y crear
  conexiones simples.
- **NIC (Network Interface Card)**: tarjeta o adaptador de red que conecta el equipo a la red.
- **Nmap**: herramienta libre de escaneo de redes y puertos, muy usada en pentesting
  ([nmap.org](https://nmap.org)).
- **NSE (Nmap Scripting Engine)**: sistema de scripts de Nmap para tareas avanzadas de descubrimiento y
  detección.
- **NTP (Network Time Protocol)**: protocolo para sincronizar el reloj de los equipos; una hora correcta es
  clave para los logs y la criptografía.

## O

- **OSI (Open Systems Interconnection)**: modelo de referencia de **7 capas** que describe cómo se comunican
  los sistemas en red.
- **OSINT (Open Source Intelligence)**: inteligencia obtenida de fuentes públicas y abiertas (webs, redes
  sociales, registros públicos…).
- **OWASP (Open Worldwide Application Security Project)**: comunidad que publica recursos de seguridad web,
  como el OWASP Top 10. **(Nivel 2)**

## P

- **Paquete**: unidad de datos que viaja por la red; lleva cabeceras (direcciones, puertos…) y la carga útil.
- **PAT (Port Address Translation)**: variante de NAT que distingue las conexiones por **puerto**, lo que
  permite que muchos equipos compartan una sola IP pública.
- **Payload (carga útil)**: parte del paquete o del exploit que lleva los datos o el código que se ejecuta.
  **(Nivel 2)**
- **Pentesting (prueba de penetración)**: evaluación **autorizada** de la seguridad de un sistema simulando
  un ataque real.
- **Permisos**: reglas que determinan quién puede leer, escribir o ejecutar cada recurso.
- **Phishing (suplantación)**: engaño para que la víctima entregue credenciales o ejecute algo malicioso.
- **Ping**: utilidad que envía paquetes ICMP para comprobar si un host responde.
- **POP3 (Post Office Protocol 3)**: protocolo para descargar el correo del servidor al cliente.
- **Protocolo**: conjunto de reglas que define cómo se comunican dos sistemas.
- **Proxy**: intermediario que recibe peticiones y las reenvía en nombre del cliente; se usa para interceptar
  tráfico (por ejemplo, Burp Suite).
- **Puerto**: número (0–65535) que identifica un servicio concreto dentro de una máquina; por ejemplo, `80`
  para HTTP y `443` para HTTPS.

## Q

- **QoS (Quality of Service)**: mecanismo para priorizar cierto tráfico (voz, vídeo) frente a otro.
- **Query (consulta)**: petición estructurada de información; típica en bases de datos y servicios de
  directorio.

## R

- **RAID**: combinación de varios discos que mejora el rendimiento y/o la tolerancia a fallos (por ejemplo,
  RAID 1 duplica los datos).
- **RAM (Random Access Memory)**: memoria de trabajo rápida y **volátil**; su contenido se pierde al apagar.
- **Ransomware**: malware que cifra los datos y exige un rescate a cambio de devolverlos.
- **Reconocimiento (recon)**: primera fase de un pentest: recopilar información sobre el objetivo.
- **Red (network)**: conjunto de dispositivos conectados que pueden intercambiar datos.
- **Red Team**: equipo ofensivo que simula ataques **autorizados** para probar las defensas de una
  organización.
- **Root**: cuenta de máximo privilegio en Linux/Unix. «Ser root» es tener control total.
- **Router (encaminador)**: dispositivo que conecta redes distintas y decide por dónde enviar cada paquete.
- **RSA**: uno de los algoritmos de cifrado asimétrico más usados (clave pública y clave privada).

## S

- **Salting (sal)**: añadir datos aleatorios a una contraseña antes de calcular su hash, para dificultar los
  ataques con tablas precalculadas.
- **Segmentación de red**: dividir una red en partes más pequeñas para limitar el alcance de un incidente.
- **Servidor**: equipo o programa que ofrece un servicio a los clientes (web, correo, ficheros…).
- **SHA (Secure Hash Algorithm)**: familia de funciones hash (SHA-256, SHA-3…).
- **SIEM**: sistema que centraliza y correlaciona logs para detectar incidentes. **(Nivel 2)**
- **SMTP (Simple Mail Transfer Protocol)**: protocolo para **enviar** correo electrónico.
- **SNMP (Simple Network Management Protocol)**: protocolo para monitorizar y gestionar dispositivos de red.
- **SOC (Security Operations Center)**: equipo y centro dedicado a vigilar y responder a incidentes de
  seguridad. **(Nivel 2)**
- **Socket**: combinación de dirección IP y puerto que identifica un extremo de una conexión; es la interfaz
  de programación de red que usan las aplicaciones.
- **SSH (Secure Shell)**: protocolo para conectarse y administrar una máquina de forma remota y cifrada.
- **SSL (Secure Sockets Layer)**: protocolo antiguo de cifrado de comunicaciones; su sucesor es TLS.
- **Stack (pila)**: estructura de datos «último en entrar, primero en salir»; en memoria, la zona donde un
  programa guarda variables y direcciones de retorno. El *stack overflow* (desbordamiento de pila) es una
  clase de vulnerabilidad.
- **Subnetting (subneteo)**: dividir una red en subredes más pequeñas ajustando la máscara.
- **Switch (conmutador)**: dispositivo de capa de enlace que conecta equipos de una misma red local y
  reenvía las tramas según la dirección MAC.

## T

- **TCP (Transmission Control Protocol)**: protocolo de transporte **orientado a conexión y fiable**;
  garantiza que los datos llegan ordenados y completos.
- **Three-way handshake**: establecimiento de una conexión TCP en tres pasos: `SYN`, `SYN-ACK`, `ACK`.
- **TLS (Transport Layer Security)**: protocolo que cifra y protege la integridad de las comunicaciones; es
  la «s» de HTTPS.
- **Topología**: forma en que están conectados los dispositivos de una red (estrella, bus, malla…).
- **Tráfico**: conjunto de paquetes que circulan por una red.
- **Troyano (Trojan)**: malware que se disfraza de programa legítimo para engañar al usuario.
- **TTL (Time To Live)**: campo que limita cuántos saltos puede dar un paquete antes de descartarse; cada
  router lo reduce en una unidad.

## U

- **UDP (User Datagram Protocol)**: protocolo de transporte **no orientado a conexión y sin garantías**;
  rápido, pero no confirma la entrega.
- **UEFI (Unified Extensible Firmware Interface)**: firmware moderno que sustituye a la BIOS e inicializa el
  equipo antes de cargar el sistema operativo.
- **Unicast**: comunicación dirigida a un **único** destinatario.
- **Uptime**: tiempo que un sistema lleva funcionando sin interrupciones.
- **URL (Uniform Resource Locator)**: dirección que identifica un recurso en la web.
- **USB**: interfaz estándar de conexión de periféricos; también una vía habitual de infección física.
- **Usuario**: identidad con la que se accede a un sistema, con sus propios permisos y su propio espacio.

## V

- **Virtualización**: ejecutar uno o varios sistemas operativos dentro de otro mediante una máquina virtual.
- **Virus**: malware que se copia a sí mismo dentro de otros ficheros y se propaga al ejecutarse.
- **VLAN (Virtual LAN)**: red lógica separada dentro de la misma infraestructura física.
- **VLSM (Variable Length Subnet Mask)**: usar máscaras de distinta longitud dentro de la misma red para no
  desperdiciar direcciones.
- **VM (máquina virtual)**: ordenador simulado por software que ejecuta un sistema operativo completo.
- **VPN (Virtual Private Network)**: túnel cifrado que conecta a un equipo o red remota como si estuviera en
  la red local.
- **Vulnerabilidad**: fallo o debilidad que un atacante puede aprovechar para comprometer un sistema.

## W

- **WAN (Wide Area Network)**: red de área amplia que conecta ubicaciones lejanas; Internet es la mayor WAN.
- **Web (aplicación web)**: software al que se accede por navegador mediante HTTP/HTTPS.
- **WiFi**: tecnología de red **inalámbrica** de área local.
- **Wireshark**: analizador de tráfico de red que permite capturar y examinar paquetes
  ([wireshark.org](https://www.wireshark.org)).
- **Worm (gusano)**: malware que se propaga solo por la red, sin necesidad de que el usuario haga nada.
- **WPA (Wi-Fi Protected Access)**: estándar de seguridad WiFi que sustituyó al obsoleto WEP; hoy se
  considera desfasado.
- **WPA2**: estándar WiFi muy extendido y, bien configurado, todavía válido; introdujo mejoras de cifrado
  sobre WPA.
- **WPA3**: el estándar WiFi más reciente, con protección reforzada frente a ataques de diccionario. Si tu
  equipo y tu router lo soportan, es la opción recomendada.
- **Writeup**: documento que explica paso a paso cómo se resolvió una máquina o un reto.

## X

- **X.509**: estándar que define el formato de los **certificados digitales** usados en TLS.
- **XML (eXtensible Markup Language)**: formato de texto para estructurar datos, común en servicios web.
- **XSS (Cross-Site Scripting)**: vulnerabilidad web que permite inyectar y ejecutar JavaScript en el
  navegador de otras personas. **(Nivel 2)**

## Y

- **YARA**: herramienta y lenguaje de reglas para identificar malware por patrones. **(Nivel 2)**
- **YubiKey**: ejemplo de llave de seguridad física (USB/NFC) usada como segundo factor de autenticación.

## Z

- **Zero Trust**: modelo de seguridad que **no confía en nada por defecto** y verifica cada acceso, esté
  dentro o fuera de la red.
- **Zero-day**: vulnerabilidad desconocida por el fabricante y **sin parche disponible** en el momento de
  su explotación.
- **Zombie (bot)**: equipo infectado y controlado remotamente que forma parte de una botnet.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Revisar y ampliar el glosario con los términos que vayan apareciendo en el Nivel 2 y en los Paths
    (por ejemplo, *pivoting*, *tunneling*, *buffer overflow*, *SQLi*, *SSRF*), y añadir enlaces internos a
    la página concreta de cada término cuando todas las páginas estén publicadas.
