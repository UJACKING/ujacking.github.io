# Direccionamiento IP y MAC

**Resumen.** Cada equipo necesita una dirección para que los datos sepan a dónde ir. Hay dos tipos:
la **lógica** (IP), que permite cruzar entre redes, y la **física** (MAC), que identifica la tarjeta de
red en el tramo local. Aquí aprenderás cómo son, qué rangos están reservados y en qué se diferencian.

## Objetivos de aprendizaje

- Entender la estructura de una dirección **IPv4** (32 bits, 4 octetos) y su notación decimal.
- Conocer las **clases históricas** y por qué hoy casi no se usan.
- Identificar los **rangos privados (RFC 1918)**, el **loopback** y las **APIPA/link-local**.
- Tener una idea básica de **IPv6** (128 bits, hexadecimal, compresión `::`).
- Entender la **dirección MAC**, el **OUI** y la diferencia entre dirección lógica y física.

**Tiempo estimado: 60–90 min**

## Requisitos previos

- **[01 · Modelos OSI y TCP/IP](01-modelos-osi-y-tcp-ip.md)**: conviene saber qué es la capa de red
  (IP) y la de enlace (MAC) antes de seguir.
- Nociones de **binario**; el módulo de arquitectura lo explica. Aquí verás los cálculos explicados.

## Explicación

### Dirección IPv4: qué es

Una dirección **IPv4** es un número de **32 bits** que se escribe como **cuatro números separados por
puntos**, cada uno de 0 a 255 (un byte = 8 bits, llamado *octeto*):

```text
192   .   168   .    1    .    50
8 bits  8 bits   8 bits   8 bits   = 32 bits
```

- El rango posible de cada octeto es 0–255 (256 valores, porque \(2^8 = 256\)).
- Total de direcciones IPv4: \(2^{32} \approx 4.290\) millones. Parecen muchas, pero se agotaron.

Cada dirección IPv4 tiene **dos partes**:

- **Parte de red:** identifica a qué red pertenece. Todos los equipos de la misma red comparten esta
  parte.
- **Parte de host:** identifica al equipo dentro de esa red.

La frontera entre ambas la marca la **máscara de subred**, que estudiarás en profundidad en la
página de **[Subnetting](03-subnetting.md)**. Por ahora quédate con la idea.

### Clases históricas (A, B, C, D, E)

Antes se asignaban direcciones por **clases**, mirando el primer octeto. Hoy el reparto es por CIDR
(lo verás en subnetting), pero las clases aparecen tanto en el temario como en exámenes, así que hay
que conocerlas:

| Clase | Primer octeto | Máscara por defecto | Uso pensado | Ejemplo |
| --- | --- | --- | --- | --- |
| A | 1 – 126 | 255.0.0.0 (/8) | Redes enormes | 10.0.0.1 |
| B | 128 – 191 | 255.255.0.0 (/16) | Redes medianas | 172.16.5.1 |
| C | 192 – 223 | 255.255.255.0 (/24) | Redes pequeñas | 192.168.1.1 |
| D | 224 – 239 | — | **Multicast** | 224.0.0.1 |
| E | 240 – 255 | — | **Experimental** (reservado) | 240.0.0.1 |

!!! note "El 127 no es clase A normal"
    El primer octeto **127** está reservado para **loopback**, no se asigna como red de clase A.

### Rangos privados (RFC 1918)

Estas direcciones **no son enrutables en Internet**: se usan dentro de redes privadas (casa, empresa,
laboratorio) y salen a Internet mediante NAT. Son las que verás el 99 % del tiempo:

| Rango privado | CIDR | Nº de direcciones |
| --- | --- | --- |
| 10.0.0.0 – 10.255.255.255 | 10.0.0.0/8 | ~16,7 millones |
| 172.16.0.0 – 172.31.255.255 | 172.16.0.0/12 | ~1 millón |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 | 65.536 |

Si ves `192.168.x.x` o `10.x.x.x`, estás casi seguro en una red privada.

### Otras direcciones especiales

| Dirección / rango | CIDR | Para qué sirve |
| --- | --- | --- |
| 127.0.0.0 – 127.255.255.255 | 127.0.0.0/8 | **Loopback**: el equipo hablándose a sí mismo (`127.0.0.1`). |
| 169.254.0.0 – 169.254.255.255 | 169.254.0.0/16 | **APIPA / link-local**: autoconfigurada si no hay DHCP. |
| 0.0.0.0 | /32 | "Cualquier interfaz" o "sin dirección asignada". |
| 255.255.255.255 | /32 | **Broadcast limitado**: a todos los equipos de la red local. |

!!! warning "Truco de diagnóstico: APIPA"
    Si un equipo Windows muestra una dirección `169.254.x.x`, es señal de que **no consiguió IP por
    DHCP**. Casi siempre significa problema de conexión o de servidor DHCP.

### IPv6, muy básico

IPv6 nació para resolver el agotamiento de IPv4. Características principales:

- **128 bits** de longitud (frente a 32).
- Se escribe en **hexadecimal**, en **8 grupos de 16 bits** separados por `:`.

```text
2001:0db8:0000:0000:0000:ff00:0042:8329
```

Reglas de escritura abreviada:

- Se pueden **quitar ceros a la izquierda** de cada grupo:
  `2001:db8:0:0:0:ff00:42:8329`
- Los **grupos de ceros consecutivos** se sustituyen una sola vez por `::`:
  `2001:db8::ff00:42:8329`

El prefijo habitual en redes domésticas es **/64** (la mitad de la dirección para red y la mitad para
el host). El equivalente a "IP privada" autoconfigurada es la **link-local `fe80::/10`**, que cada
interfaz genera sola.

!!! info "No te agobies con IPv6"
    En este nivel basta con reconocer el formato, la compresión `::` y que existe la link-local
    `fe80::`. El detalle se ve más adelante.

### Dirección MAC: la dirección "física"

La **MAC** (Media Access Control) es la dirección de la tarjeta de red. Es:

- De **48 bits**, escrita en **hexadecimal** como 6 pares separados por `:` o `-`:
  `00:1A:2B:3C:4D:5E`
- **Fija de fábrica** (aunque se puede cambiar por software: *MAC spoofing*).
- **Única a nivel mundial** en teoría.

Se divide en dos mitades:

| Parte | Bits | Qué identifica |
| --- | --- | --- |
| **OUI** (Organizationally Unique Identifier) | 24 primeros bits (3 primeros pares) | El **fabricante** de la tarjeta |
| Parte de la serie (NIC specific) | 24 bits siguientes | El **número concreto** de esa tarjeta |

Ejemplo: en `00:1A:2B:3C:4D:5E`, el OUI es `00:1A:2B` (identifica al fabricante) y `3C:4D:5E` es el
número de esa unidad. Puedes consultar a qué fabricante pertenece un OUI en un buscador de OUI (por
ejemplo, el servicio público de <https://www.wireshark.org>).

Dos MAC especiales importantes:

- `FF:FF:FF:FF:FF:FF` → **broadcast**: lo reciben todas las tarjetas de la red local.
- El bit menos significativo del primer octeto distingue **unicast** (0) y **multicast** (1).

### Dirección lógica vs física

| | Dirección IP (lógica) | Dirección MAC (física) |
| --- | --- | --- |
| Capa | Red (capa 3) | Enlace (capa 2) |
| Formato | 32 bits (IPv4), decimal con puntos | 48 bits, hexadecimal con `:` |
| Alcance | Global, **cruza redes** | Local, **solo el tramo** |
| Cambia | Normalmente no durante el viaje | **Sí, en cada salto** |
| Se asigna | Manual o por DHCP | De fábrica (o por software) |
| Ejemplo | 192.168.1.50 | 00:1A:2B:3C:4D:5E |

!!! note "Cómo encajan las dos"
    Para **cruzar de red**, el paquete usa la IP de principio a fin. Pero para **entregar** ese paquete
    dentro de cada red local, se usa la MAC del siguiente equipo (el router). Esa traducción de IP a
    MAC es justo lo que hace **ARP**, que verás en la capa de enlace.

## Ejemplos prácticos

### Ver tus direcciones IP y MAC

```bash
ip address show
```

Salida de ejemplo (recortada):

```text
2: enp3s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ...
    link/ether 00:1a:2b:3c:4d:5e brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.50/24 brd 192.168.1.255 scope global enp3s0
    inet6 fe80::1a2b:3c4d:5e6f:7a8b/64 scope link
```

Línea a línea:

- `link/ether 00:1a:2b:3c:4d:5e` es la **MAC** de la interfaz (`brd` es su dirección de broadcast).
- `inet 192.168.1.50/24` es la **IPv4**; `/24` es el prefijo (máscara).
- `brd 192.168.1.255` es la **dirección de broadcast** de esa red.
- `inet6 fe80::.../64 scope link` es la **IPv6 link-local** autoconfigurada.

### Ver solo las MAC de tu red (tabla de vecinos)

```bash
ip neigh
```

Salida de ejemplo:

```text
192.168.1.1 dev enp3s0 lladdr aa:bb:cc:dd:ee:01 REACHABLE
192.168.1.20 dev enp3s0 lladdr aa:bb:cc:dd:ee:02 STALE
```

Cada línea asocia una IP con la MAC de un equipo de la misma red local. Esa tabla la rellena ARP.

## Errores comunes

- **Confundir "privada" con "oculta".** Una IP privada no es más segura por sí misma; solo significa
  que no se enruta en Internet.
- **Pensar que la MAC nunca cambia.** Cambia en cada salto entre routers, y además se puede falsificar
  por software.
- **Creer que `127.0.0.1` es "mi IP".** Es la del **loopback**: sirve para que el equipo hable consigo
  mismo, no para que le lleguen datos desde fuera.
- **Olvidar que el primer octeto de las clases no salta a 127.** El 127 está reservado para loopback.
- **Escribir una MAC con 5 o 7 pares.** Son siempre **6 pares** (48 bits).

## Ejercicios

### Ejercicio 1

Indica, para cada dirección, si es privada, loopback, APIPA/link-local o pública:
`10.5.5.5`, `192.168.0.10`, `127.0.0.1`, `169.254.10.20`, `8.8.8.8`.

??? success "Solución"
    - `10.5.5.5` → **privada** (rango 10.0.0.0/8).
    - `192.168.0.10` → **privada** (rango 192.168.0.0/16).
    - `127.0.0.1` → **loopback**.
    - `169.254.10.20` → **APIPA / link-local**.
    - `8.8.8.8` → **pública** (es un DNS público de Google, ese sí enrutable en Internet).

### Ejercicio 2

¿A qué clase histórica pertenece la dirección `172.20.10.5`? ¿Es privada?

??? success "Solución"
    El primer octeto es **172**, que está en el rango **128–191**: es **clase B**. Además, 172.20 cae
    dentro de `172.16.0.0/12`, así que también es **privada**.

### Ejercicio 3

Dada la MAC `AA:BB:CC:11:22:33`, ¿cuál es el OUI y qué identifica?

??? success "Solución"
    El **OUI** son los tres primeros pares: `AA:BB:CC`. Identifica al **fabricante** de la tarjeta. Los
    tres últimos (`11:22:33`) identifican esa unidad concreta.

### Ejercicio 4

¿Verdadero o falso? "La dirección IP de un paquete cambia en cada salto entre routers, igual que la
MAC." Justifica.

??? success "Solución"
    **Falso.** La **IP no cambia** en cada salto (salvo NAT, caso especial): identifica el destino
    final. Lo que cambia en cada salto es la **MAC**, porque la entrega dentro de cada red local se
    hace al siguiente equipo físico.

### Ejercicio 5

Escribe abreviadas estas direcciones IPv6 usando la regla de los ceros:
`2001:0db8:0000:0000:0000:0000:00a4:0001`

??? success "Solución"
    Quitando ceros a la izquierda y comprimiendo el bloque de ceros consecutivos con `::`:
    `2001:db8::a4:1`.

### Ejercicio 6

Un equipo muestra la IP `169.254.33.7`. ¿Qué está pasando y qué revisarías primero?

??? success "Solución"
    El equipo no obtuvo dirección por DHCP y se autoconfiguró una **APIPA** (`169.254.0.0/16`). Habría
    que revisar: que el cable o el WiFi estén conectados, que el **servidor DHCP** esté funcionando y
    accesible, y que no haya un problema de configuración de red.

### Ejercicio 7

¿Cuántas direcciones hay en total en IPv4 y cuántas en IPv6? Exprésalo con potencias.

??? success "Solución"
    - IPv4: 32 bits → \(2^{32} = 4.294.967.296\) direcciones.
    - IPv6: 128 bits → \(2^{128}\), un número astronómicamente mayor (del orden de
      \(3{,}4 \times 10^{38}\)).

## Resumen

- **IPv4**: 32 bits, 4 octetos (0–255), notación decimal con puntos; se divide en parte de red y
  parte de host.
- **Clases históricas**: A (1–126), B (128–191), C (192–223), D multicast (224–239), E experimental
  (240–255).
- **Privadas (RFC 1918)**: 10.0.0.0/8, 172.16.0.0/12 y 192.168.0.0/16.
- **Especiales**: loopback 127.0.0.0/8, APIPA 169.254.0.0/16.
- **IPv6**: 128 bits en hexadecimal, compresión `::`, link-local `fe80::/10`.
- **MAC**: 48 bits hexadecimales, OUI de fabricante + número de serie; solo vale en el tramo local.
- La **IP es lógica y global**; la **MAC es física y local**.

## Checklist

- [ ] Sé pasar una IPv4 de formato decimal a su significado (4 octetos, 32 bits).
- [ ] Reconozco a qué clase histórica pertenece una dirección.
- [ ] Distingo direcciones privadas, loopback y APIPA a simple vista.
- [ ] Sé leer y abreviar una dirección IPv6 básica.
- [ ] Puedo descomponer una MAC en OUI y número de serie.
- [ ] Explico la diferencia entre dirección lógica y física.

## Para ir más allá

- **RFC 1918 — Address Allocation for Private Internets** — define los rangos privados. Tipo:
  documentación oficial · Inglés (EN) · **Gratis**. <https://www.rfc-editor.org>
- **RFC 4291 — IPv6 Addressing Architecture** — formato y compresión de direcciones IPv6. Tipo:
  documentación oficial · Inglés (EN) · **Gratis**. <https://www.rfc-editor.org>
- **MDN Web Docs** — repaso general de conceptos web y de red. Tipo: referencia · Español/Inglés (EN) ·
  **Gratis**. <https://developer.mozilla.org>
- **Wireshark** — captura ARP y verás la correspondencia IP↔MAC en directo. Tipo: herramienta ·
  Inglés (EN) · **Gratis**. <https://www.wireshark.org>

## Siguiente paso

Ya sabes qué es una dirección y qué es una máscara de pasada. Toca el tema clave del módulo:
**[03 · Subnetting](03-subnetting.md)**. Tómatelo con calma, es el más importante.
