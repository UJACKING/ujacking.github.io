# Subnetting

**Resumen.** El subnetting es dividir una red en trozos más pequeños (subredes) para organizar
direcciones y aislar tráfico. Para hacerlo hay que saber calcular, a mano y sin calculadora, la
**dirección de red**, la de **broadcast**, el **rango de hosts** y el **número de hosts**. Esta página
es la más importante del módulo: lee, calcula y repite hasta que salga solo.

!!! tip "El tema que no puedes saltarte"
    El subnetting aparece en casi todas las certificaciones de redes y de seguridad, y lo usarás al
    interpretar escaneos con Nmap. Si hoy no te sale, no pasa nada: haz los ejercicios varias veces
    hasta mecanizarlo. Es cuestión de práctica, no de talento.

## Objetivos de aprendizaje

- Explicar qué es una **máscara de subred** y cómo separa red y host.
- Usar la **notación CIDR** (`/24`, `/26`…) y convertir máscara ↔ prefijo.
- Calcular **dirección de red**, **broadcast**, **rango de hosts** y **número de hosts**.
- Hacer **subnetting por prefijo** y **VLSM** (subredes de distinto tamaño).
- Resolver ejercicios variados con soltura y sin calculadora.

**Tiempo estimado: 120–180 min** (sí, es largo; merece la pena)

## Requisitos previos

- **[02 · Direccionamiento IP y MAC](02-direccionamiento-ip-y-mac.md)**: hay que entender qué es una
  dirección IPv4 y sus 4 octetos.
- Manejo básico de **potencias de 2**: 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024.
- **Recomendado:** saber convertir números pequeños a binario. Todo se entiende mejor viendo los bits.

## Explicación

### Qué es una máscara de subred

Una dirección IPv4 tiene parte de **red** y parte de **host**. La **máscara de subred** marca dónde
está la frontera:

- Bits en **1** → parte de **red**.
- Bits en **0** → parte de **host**.

Ejemplo con `192.168.1.50` y máscara `255.255.255.0`:

```text
IP:     192.168.1.50    →  11000000.10101000.00000001.00110010
Máscara:255.255.255.0   →  11111111.11111111.11111111.00000000
                           |--------- red ---------| |-- host --|
```

Los **24 primeros bits** son de red y los **8 últimos** de host. Por eso esa red es
`192.168.1.0` y admite hasta 254 equipos (`192.168.1.1`–`192.168.1.254`).

### Notación CIDR

En lugar de escribir la máscara se escribe una barra y el número de bits a 1 (los de red). Eso es
**CIDR** (Classless Inter-Domain Routing):

`255.255.255.0` = 24 bits a 1 = **/24**

La tabla siguiente es tu mejor amiga. Mézclala bien:

| CIDR | Máscara | Wildcard (inversa) | Nº direcciones | Hosts útiles | Salto (bloque) |
| --- | --- | --- | --- | --- | --- |
| /8 | 255.0.0.0 | 0.255.255.255 | 16.777.216 | 16.777.214 | en 2.º octeto: 256 |
| /12 | 255.240.0.0 | 0.15.255.255 | 1.048.576 | 1.048.574 | en 2.º octeto: 16 |
| /16 | 255.255.0.0 | 0.0.255.255 | 65.536 | 65.534 | en 3.er octeto: 256 |
| /20 | 255.255.240.0 | 0.0.15.255 | 4.096 | 4.094 | en 3.er octeto: 16 |
| /22 | 255.255.252.0 | 0.0.3.255 | 1.024 | 1.022 | en 3.er octeto: 4 |
| /23 | 255.255.254.0 | 0.0.1.255 | 512 | 510 | en 3.er octeto: 2 |
| /24 | 255.255.255.0 | 0.0.0.255 | 256 | 254 | en 4.º octeto: 256 |
| /25 | 255.255.255.128 | 0.0.0.127 | 128 | 126 | en 4.º octeto: 128 |
| /26 | 255.255.255.192 | 0.0.0.63 | 64 | 62 | en 4.º octeto: 64 |
| /27 | 255.255.255.224 | 0.0.0.31 | 32 | 30 | en 4.º octeto: 32 |
| /28 | 255.255.255.240 | 0.0.0.15 | 16 | 14 | en 4.º octeto: 16 |
| /29 | 255.255.255.248 | 0.0.0.7 | 8 | 6 | en 4.º octeto: 8 |
| /30 | 255.255.255.252 | 0.0.0.3 | 4 | 2 | en 4.º octeto: 4 |
| /31 | 255.255.255.254 | 0.0.0.1 | 2 | 0\* | en 4.º octeto: 2 |
| /32 | 255.255.255.255 | 0.0.0.0 | 1 | 1 | — |

\* El `/31` se usa en enlaces punto a punto (RFC 3021): sus 2 direcciones se usan para los dos
extremos, sin red ni broadcast. Para el examen, si no se menciona, cuenta 0 hosts útiles.

### Las tres direcciones que siempre calculas

En cada subred hay direcciones que **no se asignan** a equipos:

1. **Dirección de red:** la primera de la subred (todos los bits de host a **0**).
2. **Dirección de broadcast:** la última de la subred (todos los bits de host a **1**).
3. **Rango de hosts útiles:** desde la de red +1 hasta la de broadcast −1.

Fórmula de hosts útiles:

\[
\text{Hosts útiles} = 2^{(32 - \text{prefijo})} - 2
\]

Ejemplo para /26: \(2^{6} - 2 = 64 - 2 = 62\).

### Método del "salto" (o número mágico)

Es la forma más rápida de calcular a mano. Pasos:

1. Mira en qué **octeto** cae la máscara "interesante" (el que no es 255 ni 0).
2. Calcula el **salto**: `256 − (valor de ese octeto en la máscara)`.
3. Escribe los múltiplos del salto en ese octeto: 0, salto, 2·salto, 3·salto…
4. La **dirección de red** es el múltiplo igual o inmediatamente menor que el octeto de tu IP.
5. La **dirección de broadcast** es el múltiplo siguiente **menos 1**.

Ejemplo: IP `192.168.1.130`, máscara `255.255.255.128` (/25).

- Octeto interesante: el 4.º, máscara `128`.
- Salto: `256 − 128 = 128`.
- Múltiplos: `0, 128, 256`.
- `130` está entre `128` y `256` → red = `192.168.1.128`.
- Broadcast = siguiente múltiplo menos 1 = `192.168.1.127 + 128` → `192.168.1.255`.
- Hosts: `192.168.1.129`–`192.168.1.254` (126 en total).

### Subnetting por prefijo

"Subnetear por prefijo" es partir una red en subredes **todas del mismo tamaño**, alargando la
máscara.

Ejemplo: dividir `192.168.10.0/24` en subredes **/26**.

- Cada /26 tiene 64 direcciones; en el 4.º octeto saltamos de 64 en 64:
  `0, 64, 128, 192`.
- Número de subredes: \(2^{(26-24)} = 2^{2} = 4\).

| Subred | Red | Rango de hosts | Broadcast |
| --- | --- | --- | --- |
| 1 | 192.168.10.0/26 | .1 – .62 | .63 |
| 2 | 192.168.10.64/26 | .65 – .126 | .127 |
| 3 | 192.168.10.128/26 | .129 – .190 | .191 |
| 4 | 192.168.10.192/26 | .193 – .254 | .255 |

Fórmulas útiles:

- **Nº de subredes** al pasar de prefijo \(p_1\) a \(p_2\):
  \(2^{(p_2 - p_1)}\).
- **Nº de subredes por el salto:** por ejemplo, un /24 (bloque 256) partido en /27 (bloque 32) da
  \(256 / 32 = 8\) subredes.

### VLSM: subredes de distinto tamaño

**VLSM** (Variable Length Subnet Mask) es usar **máscaras distintas** en la misma red para no
desperdiciar direcciones. Se asignan **de mayor a menor** necesidad.

Ejemplo: repartir `192.168.1.0/24` entre:

- Departamento A: **100 hosts**
- Departamento B: **50 hosts**
- Departamento C: **20 hosts**
- Dos enlaces punto a punto: **2 hosts** cada uno

Paso a paso (siempre de mayor a menor):

1. **100 hosts** → necesito \(2^n - 2 \ge 100\) → \(n=7\) (128) → **/25**.
   `192.168.1.0/25` (rango `.1`–`.126`, broadcast `.127`).
2. **50 hosts** → \(n=6\) (64) → **/26**.
   `192.168.1.128/26` (rango `.129`–`.190`, broadcast `.191`).
3. **20 hosts** → \(n=5\) (32) → **/27**.
   `192.168.1.192/27` (rango `.193`–`.222`, broadcast `.223`).
4. **Enlace 1 (2 hosts)** → **/30**: `192.168.1.224/30` (hosts `.225`–`.226`).
5. **Enlace 2 (2 hosts)** → **/30**: `192.168.1.228/30` (hosts `.229`–`.230`).

Resto libre: `192.168.1.232` – `192.168.1.255`.

!!! note "Regla de oro del VLSM"
    **Primero las subredes grandes, después las pequeñas.** Si empiezas por las pequeñas, no podrás
    encajar las grandes sin solapamientos.

## Ejemplos prácticos

### Calcular la subred con Python (para comprobar tu resultado a mano)

```bash
python3 -c "import ipaddress; r=ipaddress.ip_network('192.168.1.130/25', strict=False); print('Red:', r.network_address); print('Broadcast:', r.broadcast_address); print('Hosts:', r.num_addresses-2); print('Primer host:', r.network_address+1); print('Último host:', r.broadcast_address-1)"
```

Salida de ejemplo:

```text
Red: 192.168.1.128
Broadcast: 192.168.1.255
Hosts: 126
Primer host: 192.168.1.129
Último host: 192.168.1.254
```

Usa esto solo para **comprobar** tus cálculos. En un examen o en una entrevista lo harás a mano.

### Comprobar subredes con `ipcalc` (si lo tienes instalado)

```bash
ipcalc 192.168.1.130/25
```

Salida de ejemplo:

```text
Address:   192.168.1.130        11000000.10101000.00000001.1 0000010
Netmask:   255.255.255.128 = 25 11111111.11111111.11111111.1 0000000
Network:   192.168.1.128/25
HostMin:   192.168.1.129
HostMax:   192.168.1.254
Broadcast: 192.168.1.255
Hosts/Net: 126
```

`ipcalc` no viene instalado en todas las distribuciones. Si no lo tienes, usa la línea de Python de
arriba. Puedes consultar su disponibilidad y detalles en <https://man7.org>.

## Errores comunes

- **Confundir dirección de red con primer host.** La red (`192.168.1.0`) no se asigna; el primer host
  es `192.168.1.1`.
- **Olvidar restar 2 al contar hosts.** 256 direcciones en un /24 son **254 hosts útiles**.
- **Usar el salto del octeto equivocado.** Con `/25` el salto es 128, no 256.
- **En VLSM, empezar por las subredes pequeñas.** Hay que ir de mayor a menor.
- **Creer que dos IPs parecidas están en la misma subred.** Hay que comparar con la máscara, no a
  ojo. (`192.168.1.50/26` y `192.168.1.80/26` **no** están en la misma subred.)
- **Escribir mal la máscara.** `/26` es `255.255.255.192`, no `.224` (eso es `/27`).

## Ejercicios

### Ejercicio 1

Para `192.168.1.130/25`, indica dirección de red, broadcast, rango de hosts útiles y número de hosts.

??? success "Solución"
    - Máscara `/25` → `255.255.255.128`. Salto = `256 − 128 = 128` → múltiplos `0, 128, 256`.
    - `130` cae entre `128` y `256` → **red = `192.168.1.128`**.
    - **Broadcast = `192.168.1.255`**.
    - **Hosts útiles = `192.168.1.129` – `192.168.1.254`**.
    - Nº de hosts: \(2^{7} - 2 = 126\).
    - (Comprobación rápida: `192.168.1.130` está en la 2.ª subred /25 del bloque `192.168.1.0/24`.)

### Ejercicio 2

Para `10.0.0.200/26`, calcula red, broadcast y rango de hosts.

??? success "Solución"
    - `/26` → `255.255.255.192`. Salto = `256 − 192 = 64` → múltiplos `0, 64, 128, 192, 256`.
    - `200` cae entre `192` y `256` → **red = `10.0.0.192`**.
    - **Broadcast = `10.0.0.255`**.
    - **Hosts = `10.0.0.193` – `10.0.0.254`** (62 hosts).

### Ejercicio 3

Para `172.16.5.70/27`, calcula red, broadcast, rango de hosts y nº de hosts.

??? success "Solución"
    - `/27` → `255.255.255.224`. Salto = `256 − 224 = 32` → `0, 32, 64, 96, 128…`
    - `70` cae entre `64` y `96` → **red = `172.16.5.64`**.
    - **Broadcast = `172.16.5.95`**.
    - **Hosts = `172.16.5.65` – `172.16.5.94`**.
    - Nº de hosts: \(2^{5} - 2 = 30\).

### Ejercicio 4

Para `192.168.10.5/28`, calcula red, broadcast y rango de hosts.

??? success "Solución"
    - `/28` → `255.255.255.240`. Salto = `256 − 240 = 16` → `0, 16, 32, 48…`
    - `5` cae entre `0` y `16` → **red = `192.168.10.0`**.
    - **Broadcast = `192.168.10.15`**.
    - **Hosts = `192.168.10.1` – `192.168.10.14`** (14 hosts).

### Ejercicio 5

Para `203.0.113.66/27`, calcula red, broadcast y nº de hosts.

??? success "Solución"
    - `/27` → máscara `...224`, salto = 32 → `0, 32, 64, 96…`
    - `66` cae entre `64` y `96` → **red = `203.0.113.64`**.
    - **Broadcast = `203.0.113.95`**.
    - Nº de hosts: 30.

### Ejercicio 6

Para `10.10.10.10/30`, calcula red, broadcast y rango de hosts.

??? success "Solución"
    - `/30` → máscara `...252`, salto = `256 − 252 = 4` → `0, 4, 8, 12…`
    - `10` cae entre `8` y `12` → **red = `10.10.10.8`**.
    - **Broadcast = `10.10.10.11`**.
    - **Hosts = `10.10.10.9` – `10.10.10.10`** (2 hosts). Típico en enlaces punto a punto.

### Ejercicio 7

¿Cuántas subredes **/24** se pueden sacar de `172.16.0.0/16`? ¿Cuántos hosts tiene cada una?

??? success "Solución"
    - \(2^{(24 - 16)} = 2^{8} = **256 subredes** /24.
    - Cada /24 tiene \(2^{8} − 2 = **254 hosts** útiles.

### Ejercicio 8 (VLSM)

Reparte `192.168.1.0/24` entre: 100 hosts, 50 hosts, 20 hosts y dos enlaces de 2 hosts. Indica cada
subred con su prefijo y rango.

??? success "Solución"
    De mayor a menor:
    1. **100 hosts** → /25 → `192.168.1.0/25` (hosts `.1`–`.126`, bcast `.127`).
    2. **50 hosts** → /26 → `192.168.1.128/26` (hosts `.129`–`.190`, bcast `.191`).
    3. **20 hosts** → /27 → `192.168.1.192/27` (hosts `.193`–`.222`, bcast `.223`).
    4. **Enlace 1** → /30 → `192.168.1.224/30` (hosts `.225`–`.226`).
    5. **Enlace 2** → /30 → `192.168.1.228/30` (hosts `.229`–`.230`).
    Libre: `192.168.1.232` – `192.168.1.255`.

### Ejercicio 9

¿Están `192.168.1.50/26` y `192.168.1.80/26` en la misma subred? ¿Y `192.168.1.10/29` y
`192.168.1.14/29`?

??? success "Solución"
    - `/26`: salto 64 → subredes `.0–.63`, `.64–.127`. `50` está en `.0/26`; `80` está en `.64/26`.
      **No** están en la misma subred.
    - `/29`: salto 8 → subredes `.0–.7`, `.8–.15`. `10` y `14` están ambas en `.8/29`.
      **Sí** están en la misma subred.

### Ejercicio 10

¿Qué máscara (decimal y CIDR) necesitas para una subred de **4096 direcciones**?

??? success "Solución"
    \(2^{n} = 4096 \Rightarrow n = 12\) bits de host → prefijo = \(32 − 12 = **/20**\).
    Máscara: `255.255.240.0`.

### Ejercicio 11

¿Cuántas subredes **/27** caben en una red `10.0.0.0/24`?

??? success "Solución"
    \(2^{(27 - 24)} = 2^{3} = **8 subredes** (o, con el salto: 256 / 32 = 8).

### Ejercicio 12

En `192.168.10.0/24`, ¿cuál es la **4.ª subred /26**? Indica red, rango y broadcast.

??? success "Solución"
    /26 = salto 64. Las subredes son: 1.ª `.0`, 2.ª `.64`, 3.ª `.128`, **4.ª `.192`**.
    - Red: **`192.168.10.192/26`**.
    - Hosts: `192.168.10.193` – `192.168.10.254`.
    - Broadcast: `192.168.10.255`.

### Ejercicio 13

¿Cuál es la **wildcard** (máscara inversa) de un `/26`? ¿Para qué se usa?

??? success "Solución"
    Wildcard = `255.255.255.255 − 255.255.255.192 = **0.0.0.63**`.
    Se usa en las listas de control de acceso (ACL) de Cisco y en Nmap, donde se expresa el "comodín"
    complementario a la máscara.

### Ejercicio 14

Para `172.16.4.0/22`, da red, broadcast, rango de hosts y nº de hosts.

??? success "Solución"
    - `/22` → `255.255.252.0`. Octeto interesante: el **3.º**, con valor 252 → salto = `256 − 252 = 4`.
    - El 3.er octeto de `4.0` es 4, que es múltiplo exacto de 4 → **red = `172.16.4.0`**.
    - La subred abarca los octetos 3.º y 4.º: del `4.0` al `7.255` → **broadcast = `172.16.7.255`**.
    - **Hosts = `172.16.4.1` – `172.16.7.254`**.
    - Nº de hosts: \(2^{10} − 2 = 1022\).

### Ejercicio 15

Elige el prefijo más ajustado para cada caso sin desperdiciar de más: (a) 2 hosts, (b) 6 hosts,
(c) 500 hosts.

??? success "Solución"
    - (a) 2 hosts → **/30** (\(2^2 − 2 = 2\)).
    - (b) 6 hosts → **/29** (\(2^3 − 2 = 6\)).
    - (c) 500 hosts → necesito \(2^n − 2 \ge 500\) → \(n = 9\) (510) → **/23**.

### Ejercicio 16

Divide `192.168.0.0/24` en subredes de **25 hosts** cada una. ¿Qué prefijo usas y cuántas salen?

??? success "Solución"
    - 25 hosts → \(2^n − 2 \ge 25\) → \(n = 5\) → **/27** (30 hosts útiles).
    - Nº de subredes: \(2^{(27 - 24)} = 2^{3} = **8 subredes**.
    - Son: `.0/27, .32/27, .64/27, .96/27, .128/27, .160/27, .192/27, .224/27`.

### Ejercicio 17 (sumarización)

Resume en una sola red estas cuatro: `192.168.0.0/24`, `192.168.1.0/24`, `192.168.2.0/24`,
`192.168.3.0/24`.

??? success "Solución"
    Las cuatro comparten los dos primeros octetos `192.168` y varían en el 3.º, de 0 a 3. Necesito
    cubrir 4 bloques (0, 1, 2, 3), que son \(2^2\) → resto 2 bits del 3.er octeto.
    - Prefijo = \(24 − 2 = **/22**\).
    - Red resumida: **`192.168.0.0/22`** (máscara `255.255.252.0`), que abarca
      `192.168.0.0` – `192.168.3.255`.

### Ejercicio 18

En `192.168.5.0/24`, ¿cuál es la **6.ª subred /28**? Da red, rango y broadcast.

??? success "Solución"
    /28 = salto 16 → subredes: 1.ª `.0`, 2.ª `.16`, 3.ª `.32`, 4.ª `.48`, 5.ª `.64`, **6.ª `.80`**.
    - Red: **`192.168.5.80/28`**.
    - Hosts: `192.168.5.81` – `192.168.5.94`.
    - Broadcast: `192.168.5.95`.

### Ejercicio 19

Convierte a CIDR: (a) `255.255.240.0`, (b) `255.255.255.248`, (c) `255.255.0.0`.

??? success "Solución"
    - (a) `255.255.240.0` → 8 + 8 + 4 = **/20**.
    - (b) `255.255.255.248` → 8 + 8 + 8 + 5 = **/29**.
    - (c) `255.255.0.0` → 8 + 8 = **/16**.

### Ejercicio 20

Una empresa tiene la red `10.20.0.0/16` y quiere subredes con **al menos 1000 hosts**. ¿Qué prefijo
usa y cuántas subredes obtiene?

??? success "Solución"
    - 1000 hosts → \(2^n − 2 \ge 1000\) → \(n = 10\) (1022) → prefijo = \(32 − 10 = **/22**\).
    - Nº de subredes: \(2^{(22 - 16)} = 2^{6} = **64 subredes** /22.

## Resumen

- La **máscara** separa la parte de red (bits a 1) de la de host (bits a 0).
- **CIDR** expresa la máscara con `/n` = número de bits de red.
- En cada subred hay **dirección de red**, **broadcast** y un **rango de hosts** (red+1 … broadcast−1).
- **Hosts útiles** = \(2^{(32 - \text{prefijo})} − 2\).
- El **método del salto**: salto = `256 − octeto de la máscara`; red = múltiplo menor o igual;
  broadcast = siguiente múltiplo − 1.
- **Subnetting por prefijo**: subredes iguales, \(2^{(p_2 - p_1)}\) subredes.
- **VLSM**: máscaras distintas; siempre **de mayor a menor**.

## Checklist

- [ ] Convierto máscaras entre formato decimal y CIDR de memoria.
- [ ] Calculo la dirección de red a mano con el método del salto.
- [ ] Calculo broadcast y rango de hosts sin calculadora.
- [ ] Sé el número de hosts de cualquier prefijo (/24 a /30).
- [ ] Divido una red en subredes iguales por prefijo.
- [ ] Reparto por VLSM de mayor a menor sin solapar.
- [ ] He resuelto los 20 ejercicios sin mirar las soluciones.

## Para ir más allá

- **RFC 1918** y **RFC 4632 (CIDR)** — fundamentos de direccionamiento privado y CIDR. Tipo:
  documentación oficial · Inglés (EN) · **Gratis**. <https://www.rfc-editor.org>
- **`ipcalc` y `sipcalc`** — utilidades de línea de comandos para comprobar redes. Tipo: herramienta ·
  Inglés (EN) · **Gratis**. <https://man7.org>
- **TryHackMe** — tiene salas de redes y de subnetting (algunas gratuitas). Tipo: plataforma de
  práctica · Inglés (EN) · **Freemium**. <https://tryhackme.com>
- **SubnettingPractice (busca "subnetting practice" en tu buscador)** — genera ejercicios aleatorios
  para practicar. Tipo: práctica · Inglés (EN) · **Gratis**. Si no encuentras una fuente fiable,
  practica con los ejercicios de esta página. TODO-UJACKING: añadir aquí un recurso concreto de
  práctica de subnetting verificado y estable.

## Siguiente paso

Con el direccionamiento dominado, toca bajar a la primera capa "de verdad": sigue con
**[04 · Capa de enlace](04-capa-de-enlace.md)**.
