# Criptografía aplicada

La criptografía está detrás de cada conexión HTTPS, cada contraseña guardada, cada firma de software y
cada certificado. No necesitas ser matemático, pero **sí** entender qué garantiza cada herramienta y,
sobre todo, **cómo se usa mal**. La mayoría de los fallos criptográficos reales no rompen el algoritmo:
rompen su uso.

## Objetivos de aprendizaje

- Diferenciar criptografía **simétrica** y **asimétrica** y saber cuándo usar cada una.
- Entender **hashes** y por qué el **salt** es imprescindible con contraseñas.
- Conocer **PKI**, certificados y la cadena de confianza.
- Explicar cómo funciona **TLS** y qué protege (y qué no).
- Aplicar conceptos a casos reales: firmas, certificados, almacenamiento de contraseñas.
- Identificar los **errores típicos** y sus consecuencias.

**Tiempo estimado:** 90–120 min.

## Requisitos previos

- **[Seguridad en tránsito](../nivel-1-principiante/02-redes/08-seguridad-en-transito.md)**: TLS a vista
  de pájaro.
- **[Protocolos de aplicación](../nivel-1-principiante/02-redes/07-protocolos-de-aplicacion.md)**: HTTP.
- **[Bash](../nivel-1-principiante/04-bash/02-comandos-esenciales.md)**: para practicar con `openssl`.

## Explicación

### Simétrica vs asimétrica

**Criptografía simétrica**: **una sola clave** cifra y descifra. Rápida, ideal para grandes volúmenes.

- Algoritmos: AES (el estándar), ChaCha20.
- Problema: ¿cómo compartes la clave con quien no la tiene, sin que nadie la intercepte?

**Criptografía asimétrica** (de clave pública): **dos claves** relacionadas matemáticamente.

- **Clave pública**: se reparte libremente. Sirve para cifrar o para verificar firmas.
- **Clave privada**: secreta. Sirve para descifrar o para firmar.
- Algoritmos: RSA, ECC (curvas elípticas). Más lentos que los simétricos.

| | Simétrica | Asimétrica |
| --- | --- | --- |
| Claves | 1 compartida | Par público/privado |
| Velocidad | Muy alta | Baja |
| Uso típico | Cifrar datos, TLS sesión | Intercambio de claves, firmas |
| Reparto de claves | Problema | Resuelto por diseño |

La magia real es **combinarlas**: la asimétrica sirve para acordar/intercambiar una clave simétrica, y
con esa clave simétrica se cifra el grueso de la comunicación. Eso es, en esencia, lo que hace TLS.

```mermaid
flowchart LR
    A["Clave pública de B"] -->|cifra| M["Mensaje cifrado"]
    M -->|descifra con| B["Clave privada de B"]
    B2["Clave privada de A"] -->|firma| F["Firma"]
    F -->|verifica con| A2["Clave pública de A"]
```

### Hashes

Una **función de hash** toma una entrada de cualquier tamaño y produce una **huella** de tamaño fijo.
Propiedades que se exigen a un hash criptográfico:

- **Determinista**: misma entrada → mismo hash.
- **Unidireccional**: del hash no se vuelve a la entrada.
- **Resistente a colisiones**: difícil encontrar dos entradas con el mismo hash.
- **Efecto avalancha**: cambiar un bit cambia el hash por completo.

| Hash | Estado |
| --- | --- |
| MD5 | **Roto** para seguridad. Solo para integridad "no adversaria". |
| SHA-1 | Roto (colisiones demostradas). No usar. |
| SHA-256 / SHA-3 | Actuales y seguros para integridad. |
| bcrypt / scrypt / Argon2 | Diseñados **para contraseñas** (lentos y con coste configurable). |

**¿Por qué el salt?** Un **salt** es un valor aleatorio único que se añade a cada contraseña antes de
hashearla. Sin salt:

- Dos usuarios con la misma contraseña tienen el **mismo hash** → se ven a simple vista.
- Los **rainbow tables** (diccionarios de hashes precalculados) permiten revertir el hash al instante.

Con salt, cada hash es distinto y las tablas precalculadas dejan de servir. Además, para contraseñas se
usan funciones **lentas y con coste ajustable** (bcrypt/Argon2), de modo que probar millones de
combinaciones sea caro.

```bash
# Ejemplo de hashing con openssl (integridad, no contraseñas)
echo -n "hola" | openssl dgst -sha256
```

Salida de ejemplo (salida de ejemplo):

```text
(stdin)= b221d9dbb083a7f33428d7c2a3c3198ae925614d70210e28716ccaa7cd4ddb79
```

!!! warning "Un hash no es un cifrado"
    Un hash **no se descifra**. Los "descifradores de MD5" que hay por internet no descifran: **prueban**
    candidatos y comparan. Por eso una contraseña común en MD5 sin salt está perdida.

### PKI y certificados

La **PKI** (Public Key Infrastructure) es el sistema que da **confianza** en las claves públicas. ¿Cómo
sabes que la clave pública de `tu-banco.com` es de verdad del banco y no de un atacante?

- Una **Autoridad de Certificación (CA)** firma un **certificado** que une una clave pública con una
  identidad (dominio, organización).
- Tu sistema confía en un conjunto de **CAs raíz** preinstaladas.
- Cuando visitas un sitio, su certificado llega junto con la **cadena** hasta una CA raíz de confianza.

```mermaid
flowchart TD
    R["CA raíz (en tu sistema)"] --> I["CA intermedia"]
    I --> L["Certificado del sitio (tu-banco.com)"]
    L --> V{"¿Firmado por una CA de confianza y válido?"}
    V -->|Sí| OK["Conexión confiable"]
    V -->|No| KO["Aviso del navegador"]
```

Un certificado contiene: titular, clave pública, emisor, **fechas de validez**, número de serie y las
**extensiones** (para qué sirve, para qué dominios). Los certificados **caducan**: si la fecha no cubre
"ahora", el navegador protesta.

### TLS

**TLS** (Transport Layer Security) es el protocolo que da a HTTPS sus tres propiedades:

| Propiedad | Qué significa |
| --- | --- |
| **Confidencialidad** | Nadie en medio lee el contenido. |
| **Integridad** | Nadie lo modifica sin que se note. |
| **Autenticación** | El servidor demuestra su identidad con un certificado. |

El **handshake** (simplificado): el cliente y el servidor negocian versión y algoritmos, el cliente
verifica el certificado, ambos **acuerdan una clave de sesión** (intercambio de claves) y a partir de ahí
todo va cifrado con criptografía **simétrica**.

!!! info "TLS no lo protege todo"
    TLS protege el **transporte**, no el contenido final. No impide XSS, inyección SQL ni un servidor mal
    programado. Cifrar una web vulnerable la deja igual de vulnerable, solo que el tráfico no se lee en
    la red.

### Aplicaciones prácticas

| Caso | Qué se usa |
| --- | --- |
| Guardar contraseñas | Hash lento con salt (bcrypt/Argon2). Nunca reversible. |
| Firmar software | Firma con clave privada; los usuarios verifican con la pública. |
| HTTPS | Certificado + TLS. |
| Tokens/cookies | Firmados (HMAC) o cifrados; **no** "Base64 y ya". |
| VPN | Intercambio de claves + cifrado simétrico. |
| SSH | Par de claves; la privada nunca sale de tu equipo. |

### Errores típicos

| Error | Consecuencia |
| --- | --- |
| Usar MD5/SHA-1 para contraseñas | Se revierten con diccionarios. |
| Hash **sin salt** | Rainbow tables y colisiones entre usuarios. |
| Cifrado simétrico con clave *hardcodeada* en el código | Quien lee el código, descifra todo. |
| Cifrar pero no **autenticar** (sin MAC/integridad) | Manipulación de datos indetectable. |
| Aceptar certificados inválidos "para que funcione" | Hombre-en-el-medio indefenso. |
| Reutilizar el mismo IV/nonce | Rompe esquemas de cifrado. |
| Generar claves con `random` en vez de un CSPRNG | Claves predecibles. |
| Base64 como si fuera cifrado | No aporta ninguna seguridad. |

## Práctica guiada

### Ejercicio 1 — Genera claves

Crea un par de claves RSA y una ECC, e inspecciona sus cabeceras.

??? success "Solución"
    ```bash
    openssl genrsa -out rsa.key 2048
    openssl ecparam -name prime256v1 -genkey -noout -out ec.key
    head -n1 rsa.key
    head -n1 ec.key
    ```
    Verás `-----BEGIN PRIVATE KEY-----` o similar. **Nunca compartas** la clave privada.

### Ejercicio 2 — Cifra con clave pública

Cifra un mensaje corto con una clave pública y descífralo con la privada.

??? success "Solución"
    ```bash
    openssl rsa -in rsa.key -pubout -out rsa.pub
    echo "mensaje secreto" > msg.txt
    openssl pkeyutl -encrypt -pubin -inkey rsa.pub -in msg.txt -out msg.enc
    openssl pkeyutl -decrypt -inkey rsa.key -in msg.enc
    ```
    RSA **solo** cifra mensajes pequeños. Para datos grandes se combina con cifrado simétrico.

### Ejercicio 3 — Firma y verificación

Firma un fichero con tu clave privada y verifica la firma con la pública.

??? success "Solución"
    ```bash
    openssl dgst -sha256 -sign rsa.key -out firma.bin msg.txt
    openssl dgst -sha256 -verify rsa.pub -signature firma.bin msg.txt
    ```
    Si el fichero cambia un solo byte, la verificación **falla**. Esa es la magia de la integridad.

### Ejercicio 4 — Hash vs hash+salt

Hashea la misma contraseña dos veces sin salt y con salt, y compara.

??? success "Solución"
    ```bash
    echo -n "password123" | openssl dgst -sha256
    echo -n "password123" | openssl dgst -sha256
    # mismo hash ambas veces -> sin salt
    # Con salt (prefijamos un valor aleatorio distinto cada vez):
    echo -n "s4lt1:password123" | openssl dgst -sha256
    echo -n "s4lt2:password123" | openssl dgst -sha256
    # hashes distintos aunque la contraseña sea la misma
    ```
    Conclusión: sin salt, el atacante ve contraseñas repetidas y puede usar tablas precalculadas.

### Ejercicio 5 — Inspecciona un certificado TLS

Obtén el certificado de un sitio y lee emisor y fechas.

??? success "Solución"
    ```bash
    openssl s_client -connect example.com:443 -servername example.com </dev/null 2>/dev/null \
      | openssl x509 -noout -subject -issuer -dates
    ```
    Fíjate en `issuer` (quién lo firmó) y en las fechas `notBefore`/`notAfter`. Un certificado caducado
    rompe la confianza aunque el sitio funcione.

### Ejercicio 6 — Clasifica errores

Para cada caso, di el error: (a) contraseñas con MD5, (b) `AES` sin verificar integridad, (c) clave
AES en el repositorio, (d) `base64(user)` como "token seguro".

??? success "Solución"
    - (a) Hash **roto** y **sin salt**: reversible por diccionario.
    - (b) Falta **autenticación** (MAC/AEAD): manipulación indetectable.
    - (c) Clave **hardcodeada**: comprometida por fuga del código.
    - (d) Base64 **no es cifrado**: cualquiera lo decodifica.

## Para ir más allá

- **OpenSSL** — documentación. EN, **Gratis**. <https://www.openssl.org>
- **RFC 8446 (TLS 1.3)** — el estándar. EN, **Gratis**. <https://www.rfc-editor.org>
- **NIST — criptografía** — guías. EN, **Gratis**. <https://csrc.nist.gov>
- **OWASP — Cryptographic Storage Cheat Sheet** — EN, **Gratis**. <https://cheatsheetseries.owasp.org>
- **Crypto 101** — libro libre introductorio. EN, **Gratis**. <https://www.crypto101.io>
- **Cryptohack** — retos prácticos de criptografía. EN, **Gratis**. <https://cryptohack.org>
- **Ruta de Criptografía de la web** — [paths/criptografia.md](../paths/criptografia.md).

## Siguiente paso

Con la criptografía clara, toca analizar el pasado y la información abierta: **forense digital y OSINT**.
Sigue con **[11 · Forense y OSINT](11-forense-y-osint.md)**.
