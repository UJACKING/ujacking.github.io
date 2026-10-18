# Criptografía

La **criptografía** es la ciencia de proteger información: que un mensaje solo lo lea quien debe
(confidencialidad), que no se pueda alterar sin que se note (integridad) y que podamos demostrar quién
lo envió (autenticidad). Es una disciplina **transversal**: la usas en TLS, en contraseñas, en VPN, en
firmas digitales, en blockchain y en cualquier login.

Cuidado con el mito: aplicar criptografía **mal** es peor que no aplicarla, porque da falsa sensación de
seguridad. Aquí importa el rigor matemático y las buenas prácticas más que la prisa.

## Cómo es el día a día

La criptografía no suele ser un puesto aislado en una empresa normal; normalmente es **una parte** de
otros roles (AppSec, cloud, identidad, I+D). Quien trabaja en ella hace cosas como:

| Bloque | Qué haces |
| --- | --- |
| **Diseño de protocolos** | Decidir qué primitivas usar (AES-GCM, ChaCha20-Poly1305, Ed25519, RSA-OAEP) y cómo combinarlas. |
| **Implementación segura** | Usar librerías de confianza (OpenSSL, libsodium, BoringSSL) en lugar de reinventar. |
| **Gestión de claves** | Rotación, HSM/KMS, custodia, revocación. Es donde más fallos reales ocurren. |
| **Auditoría** | Revisar usos de cripto en código: modos de cifrado, generación de aleatoriedad, padding. |
| **Formación y estándares** | Mantener el inventario criptográfico y prepararse para la migración a criptografía post-cuántica. |
| **CTF / investigación** | Romper esquemas mal implementados (nonce reuse, oráculos de padding, RNG débil). |

!!! warning "El fallo casi nunca es el algoritmo"
    AES o RSA no suelen romperse: se rompe *cómo* los usas. Reutilizar un nonce, usar ECB, un RNG
    predecible o comparar con `==` en vez de en tiempo constante son los errores clásicos.

## Habilidades clave

- **Fundamentos matemáticos**: aritmética modular, teoría de números, probabilidad, álgebra básica.
- **Cifrado simétrico y asimétrico**: AES, ChaCha20, RSA, curvas elípticas (ECC).
- **Hashing y MAC**: SHA-2/SHA-3, HMAC, derivación de claves (PBKDF2, scrypt, Argon2).
- **Protocolos**: TLS, SSH, Signal, firma digital, PKI y certificados X.509.
- **Programación** (Python ideal para prototipos) y uso de librerías criptográficas.
- **Aleatoriedad segura**: entender por qué `random` no sirve y hay que usar CSPRNG.
- **Análisis de implementaciones**: buscar patrones inseguros en código y configuraciones.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Repasa el módulo [Criptografía aplicada](../nivel-2-medio/10-criptografia-aplicada.md) del Nivel 2.
2. Entiende los tres pilares: **confidencialidad, integridad, autenticidad**, y cuándo usar cada primitiva.
3. Lee las **RFC** de los protocolos básicos en [rfc-editor.org](https://www.rfc-editor.org) **(EN, Gratis)**.
4. Sigue **Computerphile** para intuiciones claras: [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlace directo al canal.
5. Empieza **Cryptohack** para practicar retos de cripto desde cero: [cryptohack.org](https://cryptohack.org) **(EN, Gratis)**.

### Fase 2 · Medio (3–12 meses)

1. Curso universitario abierto de criptografía (el clásico de **Dan Boneh** en [coursera.org](https://www.coursera.org)) **(EN, Freemium)**.
2. Domina **AES** (modos y por qué GCM), **HMAC**, **derivación de claves** y **TLS**.
3. Practica con **PyCryptodome** y **OpenSSL**: [openssl.org](https://www.openssl.org) **(EN, Gratis)**.
4. Aprende a **leer y escribir RFC** y a entender qué garantiza (y qué no) cada esquema.
5. Juega con **CrypTool** para visualizar algoritmos: [cryptool.org](https://www.cryptool.org) **(EN, Gratis)**.

### Fase 3 · Avanzado (12 meses+)

1. Aprende **criptografía de curva elíptica**, **pareos** y **pruebas de conocimiento cero (ZKP)**.
2. Estudia **criptografía post-cuántica** con material de [nist.gov](https://www.nist.gov) **(EN, Gratis)**.
3. Analiza implementaciones reales: nonce reuse, oráculos de padding, RNG débil, *timing attacks*.
4. Contribuye a librerías o participa en retos avanzados de CTF de la categoría *crypto*: [ctftime.org](https://ctftime.org).
5. Interésate por **multiparty computation**, **homomorphic encryption** y **MPC wallets**.

## Recursos gratuitos

### Libros y guías

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| Crypto 101 (libro introductorio) | Libro | EN | Gratis | [crypto101.io](https://www.crypto101.io) |
| RFCs (protocolos) | Estándar | EN | Gratis | [rfc-editor.org](https://www.rfc-editor.org) |
| NIST CSRC (FIPS, SP 800) | Estándar | EN | Gratis | [csrc.nist.gov](https://csrc.nist.gov) |
| Documentación de OpenSSL | Documentación | EN | Gratis | [openssl.org](https://www.openssl.org) |
| Computerphile (vídeos) | Vídeo | EN | Gratis | [youtube.com](https://www.youtube.com) |

### Cursos y laboratorios

- **Cryptohack**: retos interactivos de criptografía, de básico a avanzado: [cryptohack.org](https://cryptohack.org) **(EN, Gratis)**.
- **Coursera** (criptografía de Dan Boneh, entre otros): [coursera.org](https://www.coursera.org) **(EN, Freemium)**.
- **Khan Academy** (bases matemáticas de criptografía): [khanacademy.org](https://www.khanacademy.org) **(EN, Gratis)**.
- **CrypTool** (software educativo): [cryptool.org](https://www.cryptool.org) **(EN, Gratis)**.
- **SageMath** (cálculo matemático para retos de cripto): [sagemath.org](https://www.sagemath.org) **(EN, Gratis)**.
- **CTFs**: retos de categoría *crypto* en [ctftime.org](https://ctftime.org) y laboratorios de [hackthebox.com](https://www.hackthebox.com) **(EN, Freemium)**.

### Vídeos

- **LiveOverflow** — cripto aplicada y errores de implementación: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.
- Todas las clases del curso de **Christof Paar** están publicadas; busca "Introduction to Cryptography" en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: verificar el enlace exacto de la lista de reproducción.
- TODO-UJACKING: recopilar vídeos de criptografía en español con enlaces verificados.

## Certificaciones habituales

No existe una certificación pura y universalmente reconocida de "criptografía". Este conocimiento suele
acreditarse **dentro** de otras certificaciones o mediante formación universitaria:

- **CISSP** y **CSSLP** incluyen dominio criptográfico — ISC2 · [isc2.org](https://www.isc2.org).
- **OSWE / OSEP** (explotación con cripto mal usada) — OffSec · [offsec.com](https://www.offsec.com).
- **GIAC** tiene certificaciones con fuerte componente criptográfico: [giac.org](https://www.giac.org).
- Formación reglada: **másteres y posgrados universitarios** en criptografía y seguridad (universidad de tu país).

Consulta siempre la web oficial: no fijamos precios ni temario de examen.

## Salidas laborales

- **Criptógrafo/a aplicado** (normalmente requiere base matemática fuerte o posgrado).
- **Security Engineer** con foco en identidad, TLS y gestión de claves.
- **Blockchain / Web3 Security Engineer**.
- **Cloud Security Engineer** (KMS, HSM, cifrado en reposo y en tránsito).
- **Investigador/a en criptografía** (academia, I+D, laboratorios).
- **Consultor/a de PKI y firma digital**.

Es una especialidad muy técnica: valórala si te gustan las matemáticas. Complementa bien con
[AppSec](appsec-y-desarrollo-seguro.md) y con [Blue Team y SOC](blue-team-soc.md).

## Siguiente paso

- Refuerza bases: [Nivel 2 · Medio](../nivel-2-medio/index.md).
- Si te atrae el software: [AppSec y desarrollo seguro](appsec-y-desarrollo-seguro.md).
- Índice de áreas: [Paths](index.md).
