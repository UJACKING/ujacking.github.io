# Nmap en profundidad

Nmap (*Network Mapper*) es **la** herramienta de descubrimiento de red y auditoría de puertos. En
Nivel 1 lo usaste por encima; aquí vas a entender **qué hace cada escaneo por debajo**, cómo elegir el
ritmo, cómo usar los scripts **NSE** y cómo generar salidas que se puedan procesar.

!!! danger "Uso ético y legal"
    Escanear puertos de un sistema **sin autorización** es intrusión y está penado. Practica **solo**
    contra `localhost`, tus VMs de laboratorio o plataformas que lo permiten explícitamente
    (TryHackMe, Hack The Box). Lee [Ética y legalidad](../nivel-1-principiante/00-etica-y-legalidad.md).

## Objetivos de aprendizaje

- Entender la diferencia entre escaneo de **descubrimiento** (`-sn`) y de **puertos**.
- Dominar los tipos de escaneo `-sS`, `-sT`, `-sU` y cuándo usar cada uno.
- Elegir **timing** (`-T0`–`-T5`) y controlar el rendimiento.
- Usar el motor de scripts **NSE** (`-sC`, `--script`) con criterio.
- Detectar el **sistema operativo** y las versiones de servicio.
- Aplicar técnicas de **sigilo** y entender sus límites.
- Guardar resultados en todos los formatos (`-oN`, `-oX`, `-oG`, `-oA`).

**Tiempo estimado:** 120 min.

## Requisitos previos

- **[Herramientas de diagnóstico](../nivel-1-principiante/02-redes/10-herramientas-de-diagnostico.md)**:
  `ping`, `traceroute`, `nc`.
- **[Capa de transporte](../nivel-1-principiante/02-redes/06-capa-de-transporte.md)**: handshake TCP,
  puertos UDP, flags SYN/ACK/RST.
- Tener un objetivo de laboratorio en marcha (una VM vulnerable).

## Explicación

### Qué hace Nmap y qué NO hace

Nmap envía paquetes y **interpreta las respuestas** para deducir qué servicios escuchan. No "entra" en
las máquinas: observa cómo reaccionan. Es rápido, scriptable y muy preciso… si se interpreta bien.

### Descubrimiento de hosts con `-sn`

Antes de escanear puertos, a veces solo quieres saber **qué máquinas están vivas**:

```bash
nmap -sn 192.168.1.0/24
```

- `-sn` = *no port scan*: solo ping/ARP, sin escanear puertos.
- En la red local usa **ARP** (más fiable); en redes remotas, ICMP y paquetes a puertos típicos.
- Sustituye al antiguo `-sP`.

### Tipos de escaneo

| Flag | Nombre | Cómo funciona | Requiere root |
| --- | --- | --- | --- |
| `-sS` | TCP SYN (medio abierto) | Envía SYN; si recibe SYN/ACK no completa el handshake (envía RST). Rápido y discreto. | Sí |
| `-sT` | TCP connect | Completa el handshake con `connect()`. Más visible (queda en logs de la app). | No |
| `-sU` | UDP | Envía datagramas UDP; interpreta ICMP *port unreachable*. Lento. | Normalmente sí |
| `-sn` | Ping scan | Descubrimiento, sin puertos. | No |

```bash
# Escaneo SYN de los 1000 puertos más comunes
sudo nmap -sS 192.168.1.10

# TCP connect (sin privilegios)
nmap -sT 192.168.1.10

# UDP de los puertos más probables
sudo nmap -sU --top-ports 50 192.168.1.10
```

**Estados de puerto** que imprime Nmap:

| Estado | Significado |
| --- | --- |
| `open` | Hay un servicio escuchando y acepta conexiones. |
| `closed` | El puerto responde (RST) pero no hay servicio. |
| `filtered` | Un firewall descarta los paquetes: no hay respuesta. |
| `unfiltered` | Responde, pero Nmap no sabe si está abierto o cerrado (habitual en `-sA`). |
| `open|filtered` | No hay respuesta: puede ser abierto o filtrado (típico en UDP). |

### Timing y rendimiento

`-T` ajusta la agresividad:

| Parámetro | Nombre | Cuándo usarlo |
| --- | --- | --- |
| `-T0` | *Paranoid* | Evasión extrema; lentísimo. |
| `-T1` | *Sneaky* | Evasión; muy lento. |
| `-T2` | *Polite* | Reducir carga en la red. |
| `-T3` | *Normal* | Por defecto. |
| `-T4` | *Aggressive* | Redes rápidas y fiables (lo habitual en laboratorio). |
| `-T5` | *Insane* | Puede perder resultados por ir demasiado rápido. |

Además puedes afinar con `--min-rate`, `--max-rate`, `--min-parallelism` o `--host-timeout`. Un uso
típico en redes locales rápidas:

```bash
sudo nmap -sS -T4 --min-rate 1000 -p- 192.168.1.10
```

`-p-` escanea **los 65 535 puertos TCP** (los 1000 por defecto se quedan cortos en una auditoría seria).

### Detección de versión, sistema operativo y scripts

```bash
# Versiones de servicio
sudo nmap -sV 192.168.1.10

# Detección de SO (necesita root, mejor con puertos abiertos y cerrados)
sudo nmap -O 192.168.1.10

# Scripts por defecto y versión
sudo nmap -sC -sV 192.168.1.10

# Todo junto
sudo nmap -A 192.168.1.10
```

`-A` es un atajo de `-sV -O -sC --traceroute` (más agresivo y ruidoso).

**NSE (Nmap Scripting Engine)** permite ejecutar scripts en Lua para tareas concretas:

```bash
# Categorías de scripts por defecto
nmap -sC 192.168.1.10

# Un script concreto
nmap --script http-headers -p 80 192.168.1.10

# Varios scripts
nmap --script "smb-os-discovery,smb-enum-shares" -p 445 192.168.1.10

# Por categoría
nmap --script "vuln" -p 80 192.168.1.10
```

Categorías NSE habituales:

| Categoría | Qué hace |
| --- | --- |
| `default` | Los que corre `-sC`: información útil y segura. |
| `discovery` | Más enumeración. |
| `safe` | No intrusivos. |
| `intrusive` | Pueden alterar el servicio o dejar rastro. |
| `vuln` | Comprueban vulnerabilidades conocidas. |
| `broadcast` | Descubrimiento en la red local. |
| `auth` | Pruebas de credenciales. |
| `brute` | Fuerza bruta (¡cuidado con bloqueos!). |

!!! warning "`vuln` y `brute` en laboratorio"
    Los scripts `vuln` y `brute` pueden tumbar servicios, llenar logs o bloquear cuentas. Úsalos **solo**
    en tu laboratorio y **nunca** de forma masiva contra producción. Un falso positivo de `vuln` no es
    una vulnerabilidad confirmada: hay que verificarlo a mano.

### Sigilo: qué se puede y qué no

El escaneo deja rastro. Técnicas de evasión (siempre en laboratorio, jamás contra redes ajenas):

| Técnica | Flag | Comentario |
| --- | --- | --- |
| Fragmentar paquetes | `-f` | Cada vez menos eficaz con firewalls modernos. |
| Señuelos (*decoys*) | `-D RND:10` | Mezcla tu IP con señuelos aleatorios. |
| Escaneo lento | `-T1`/`-T2` | Difícil de distinguir del ruido normal. |
| Puerto origen | `--source-port 53` | Ignorado por la mayoría de IDS. |
| Aleatorizar hosts | `--randomize-hosts` | Orden impredecible. |
| Codificar tiempos | `--data-length` | Rellena paquetes. |

Ninguna técnica te hace **invisible**: un IDS/IPS moderno o un EDR detecta el patrón. El "sigilo" es una
cuestión de grado, no de binario. La verdadera defensa es segmentar, filtrar y monitorizar.

### Formatos de salida

```bash
# Normal, XML, greppable y "todos" a la vez (recomendado)
sudo nmap -sS -sV -oA escaneo-web 192.168.1.10
```

| Flag | Formato | Uso |
| --- | --- | --- |
| `-oN` | Normal | Leer a ojo. |
| `-oX` | XML | Alimentar otras herramientas (por ejemplo, `xsltproc`). |
| `-oG` | Greppable | `grep` y scripts. |
| `-oA` | Todos | Genera `.nmap`, `.xml` y `.gnmap`. |

`-oA escaneo-web` produce `escaneo-web.nmap`, `escaneo-web.xml` y `escaneo-web.gnmap`.

## Práctica guiada

Usa tu laboratorio. Un objetivo de práctica y tu máquina atacante.

### Ejercicio 1 — Descubre la red

Localiza las máquinas vivas de tu subred de laboratorio.

??? success "Solución"
    ```bash
    ip a                       # localiza tu subred (p. ej. 192.168.56.0/24)
    nmap -sn 192.168.56.0/24
    ```
    Anota cada IP y su MAC. En redes locales Nmap usa ARP, así que es muy fiable.

### Ejercicio 2 — Escaneo completo con versión

Escanea **todos** los puertos TCP de tu objetivo y detecta versiones.

??? success "Solución"
    ```bash
    sudo nmap -p- -sV -T4 --min-rate 1000 -oA full-tcp 192.168.56.10
    ```
    `-p-` cubre los 65 535 puertos. `-sV` identifica versión. `-oA full-tcp` guarda los tres formatos.

### Ejercicio 3 — UDP

Escanea los puertos UDP más comunes.

??? success "Solución"
    ```bash
    sudo nmap -sU --top-ports 50 -T4 192.168.56.10
    ```
    Los puertos `open|filtered` son normales en UDP: si no hay respuesta, Nmap no puede decidir.

### Ejercicio 4 — Scripts NSE

Sobre un servidor web de tu laboratorio, obtén cabeceras y métodos permitidos.

??? success "Solución"
    ```bash
    nmap --script http-headers,http-methods -p 80 192.168.56.10
    ```
    Si el puerto 80 no está abierto, no verás resultados relevantes: primero confirma que hay un servicio.

### Ejercicio 5 — Detecta el SO

Intenta identificar el sistema operativo del objetivo.

??? success "Solución"
    ```bash
    sudo nmap -O 192.168.56.10
    ```
    La detección de SO mejora cuantas más huellas (**un** puerto abierto y **uno** cerrado) reciba Nmap.
    Si tienes SSH y algún puerto cerrado, el resultado es más fiable.

### Ejercicio 6 — De greppable a tablita

Del fichero `.gnmap`, extrae las líneas con puertos abiertos.

??? success "Solución"
    ```bash
    grep "Ports:" full-tcp.gnmap
    ```
    El formato greppable está pensado justo para esto: cada host en una línea con todos sus puertos,
    ideal para `cut`, `awk` o un script de Python.

## Para ir más allá

- **Nmap — documentación oficial** — referencia completa de opciones y NSE. EN, **Gratis**.
  <https://nmap.org> y <https://nmap.org/book>
- **NSE scripts** — catálogo. EN, **Gratis**. <https://nmap.org/nsedoc>
- **Zenmap** — GUI oficial de Nmap. EN, **Gratis**. <https://nmap.org/zenmap>
- **Hack The Box / TryHackMe** — máquinas para practicar enumeración. EN, **Freemium**.
  <https://www.hackthebox.com> · <https://tryhackme.com>
- **Masscan** — escaneo masivo de puertos (más rápido, más ruidoso). EN, **Gratis**.
  <https://github.com/robertdavidgraham/masscan>
- **`man nmap`** — local. EN, **Gratis**. <https://man7.org>

## Siguiente paso

Dominas el escaneo. Ahora, para no ir "a lo loco", necesitas método. Sigue con
**[06 · Metodología de pentesting](06-metodologia-de-pentesting.md)**.
