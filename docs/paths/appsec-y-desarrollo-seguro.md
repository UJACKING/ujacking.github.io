# AppSec y desarrollo seguro

**AppSec** (Application Security) es la disciplina que protege el **software durante todo su ciclo de
vida**: desde que se diseña hasta que se despliega y se mantiene. No se trata solo de buscar bugs al
final, sino de que el equipo escriba código más seguro desde el principio y de automatizar controles en
la integración continua (CI/CD).

Es un área que combina **programación, seguridad y trabajo con equipos de desarrollo**, y hoy es una de
las más demandadas porque casi todo el negocio vive en aplicaciones web, APIs y microservicios.

## Cómo es el día a día

| Bloque | Qué haces |
| --- | --- |
| **Revisiones de código** | Lees *pull requests* buscando fallos de seguridad y propones cambios concretos. |
| **Threat modeling** | Con el equipo, dibujas cómo ataca un sistema y qué controles poner antes de escribirlo. |
| **SAST / DAST / SCA** | Analizas código, aplicaciones en marcha y dependencias con herramientas automáticas y descartas falsos positivos. |
| **Pentest ligero** | Pruebas manualmente flujos de autenticación, control de acceso y lógica de negocio. |
| **Integración en CI/CD** | Metes *security gates* en el pipeline para que un fallo crítico no llegue a producción. |
| **Formación** | Enseñas al equipo a no repetir el mismo error (inyección, XSS, secretos en el repo). |

Herramientas típicas: **Burp Suite**, **OWASP ZAP**, **Semgrep**, **Snyk/Dependabot**, **SonarQube**,
gestores de secretos y linters. Nunca inventes cobertura: la meta es *reducir riesgo*, no *cero hallazgos*.

!!! tip "AppSec no es 'el que dice no'"
    Un buen perfil de AppSec propone soluciones y las integra en el flujo del desarrollador. Si solo
    bloqueas, el equipo te acabará rodeando.

## Habilidades clave

- **Programación real** en al menos un lenguaje de backend (Python, Java, Node.js, Go, PHP) y lectura de frontend.
- **Modelado de amenazas** (STRIDE, threat modeling ligero).
- **OWASP Top 10** y catálogo de patrones de fallo: [owasp.org](https://owasp.org) **(EN, Gratis)**.
- **APIs y autenticación**: OAuth2, JWT, control de acceso roto (IDOR/BOLA), CORS.
- **Herramientas de seguridad**: Burp Suite, ZAP, SAST/DAST/SCA.
- **CI/CD**: Git, pipelines, "shift-left", *security as code*.
- **Criptografía aplicada**: hashing de contraseñas, TLS, gestión de claves.
- **Comunicación**: escribir hallazgos accionables y priorizados.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Aprende a **programar de verdad** (una web con login, base de datos y sesiones). Git ayuda: [git-scm.com](https://git-scm.com).
2. Domina el **OWASP Top 10** con la teoría de [owasp.org](https://owasp.org) **(EN, Gratis)**.
3. Haz los laboratorios de **PortSwigger Web Security Academy**: [portswigger.net/web-security](https://portswigger.net/web-security) **(EN, Gratis)**. Son la mejor práctica guiada que existe.
4. Usa **OWASP Juice Shop** (proyecto de [owasp.org](https://owasp.org)) para practicar desde cero.
5. Repasa [Seguridad web y OWASP Top 10](../nivel-2-medio/07-seguridad-web-y-owasp-top-10.md) y
   [Burp Suite](../nivel-2-medio/08-burp-suite.md) del Nivel 2.

### Fase 2 · Medio (3–12 meses)

1. Aprende **revisión de código seguro** y **threat modeling** con las guías de OWASP.
2. Integra herramientas en un pipeline: **SAST** (Semgrep), **SCA** (Dependabot/Snyk), **DAST** (ZAP).
3. Estudia el **OWASP ASVS** (estándar de verificación) y las **Cheat Sheets** de OWASP **(EN, Gratis)**.
4. Practica con APIs: control de acceso a nivel de objeto (BOLA/IDOR), rate limiting, validación de input.
5. Aprende **gestión de secretos** y buenas prácticas de contenedores.

### Fase 3 · Avanzado (12 meses+)

1. Diseña el **programa AppSec** de una organización: políticas, formación, métricas, *gate* en CI/CD.
2. Adopta el **OWASP SAMM** para medir y mejorar la madurez del desarrollo seguro **(EN, Gratis)**.
3. Integra **NIST SSDF** (Secure Software Development Framework) en [nist.gov](https://www.nist.gov) **(EN, Gratis)**.
4. Especialízate en explotación avanzada de apps (deserialización, SSRF, plantillas) vía [portswigger.net/web-security](https://portswigger.net/web-security) y [hackthebox.com](https://www.hackthebox.com).
5. Participa en respuesta a incidentes de aplicaciones y *bug bounty* corporativo.

## Recursos gratuitos

### Guías y estándares

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| OWASP Top 10 | Guía | EN | Gratis | [owasp.org](https://owasp.org) |
| OWASP ASVS (verificación) | Estándar | EN | Gratis | [owasp.org](https://owasp.org) |
| OWASP SAMM (madurez) | Marco | EN | Gratis | [owasp.org](https://owasp.org) |
| OWASP Cheat Sheets | Guía | EN | Gratis | [owasp.org](https://owasp.org) |
| NIST SSDF | Marco | EN | Gratis | [nist.gov](https://www.nist.gov) |
| CWE (catálogo de debilidades) | Catálogo | EN | Gratis | [cwe.mitre.org](https://cwe.mitre.org) |

### Cursos y laboratorios

- **PortSwigger Web Security Academy**: [portswigger.net/web-security](https://portswigger.net/web-security) **(EN, Gratis)**.
- **OWASP Juice Shop** (proyecto de [owasp.org](https://owasp.org)) y **OWASP ZAP**: [zaproxy.org](https://www.zaproxy.org) **(EN, Gratis)**.
- **Hack The Box** y **TryHackMe**: [hackthebox.com](https://www.hackthebox.com) · [tryhackme.com](https://tryhackme.com) **(EN, Freemium)**.
- **SANS** *Top 25* y *reading room* de código seguro: [sans.org](https://www.sans.org) **(EN, Freemium)**.

### Vídeos

- **John Hammond** — retos web, análisis y AppSec aplicada: [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
- **LiveOverflow** — entender *por qué* funciona un fallo web y de bajo nivel: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.
- DevSecOps y código seguro: busca en [youtube.com](https://www.youtube.com) — TODO-UJACKING: fijar canales concretos verificados.

## Certificaciones habituales

Consulta cada web oficial: no fijamos precios ni formato de examen.

- **CSSLP** (Secure Software Lifecycle Professional) — ISC2 · [isc2.org](https://www.isc2.org)
- **OSWE** (Offensive Security Web Expert) — OffSec · [offsec.com](https://www.offsec.com)
- **GWEB** (GIAC Web Application Defender) — SANS/GIAC · [giac.org](https://www.giac.org)
- **Burp Suite Certified Practitioner** — PortSwigger · [portswigger.net](https://portswigger.net)
- **CompTIA Security+** — base técnica general: [comptia.org](https://www.comptia.org)

## Salidas laborales

- **AppSec Engineer / Analista de seguridad de aplicaciones**.
- **Consultor/a de desarrollo seguro**.
- **DevSecOps Engineer** (seguridad dentro del pipeline).
- **Product Security Engineer** (seguridad de producto en tecnológicas).
- **Penetration tester web** con foco en aplicaciones: ver [Pentesting web](pentesting-web.md).
- **Security Architect / Champion** dentro de un equipo de desarrollo.

Relacionado: [Criptografía](criptografia.md), [Cloud security](cloud-security.md), [GRC](grc.md) y el
portal de [Empleabilidad](../empleabilidad/index.md).

## Recordatorio ético

Probar aplicaciones **solo** con autorización por escrito o en laboratorios que lo permiten (PortSwigger,
Juice Shop, HTB, THM). Escanear o atacar una web de terceros sin permiso es un delito aunque "solo mires".
Si encuentras un fallo en un sistema ajeno, sigue un proceso de **divulgación responsable**.

## Siguiente paso

- Practica desde ya: [Nivel 2 · Medio](../nivel-2-medio/index.md).
- Si te llama el lado de encontrar bugs por recompensa: [Bug bounty](bug-bounty.md).
