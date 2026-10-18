# Bug bounty

El **bug bounty** (o *crowdsourced security*) es un modelo en el que empresas y organizaciones **invitan a
terceros a buscar vulnerabilidades en sus sistemas** a cambio de una recompensa, un reconocimiento o
ambos. Tú pruebas *solo* lo que el programa autoriza, dentro del **alcance (scope)** definido, y reportas
los fallos con calidad.

Es una forma fantástica de aprender sobre sistemas reales y de monetizar habilidades ofensivas, pero
también es **competitiva** y exige método: no es "hackear lo que me dé la gana".

!!! danger "Aviso ético y legal — léelo antes de nada"
    Un *bug bounty* **no** es permiso para atacar cualquier cosa. Solo puedes probar:

    - Sistemas incluidos **explícitamente** en el **alcance (in-scope)** de un programa **publicado** en una
      plataforma legítima.
    - Respetando **todas** las reglas del programa (fuera de alcance, límites de prueba, datos de usuarios, etc.).

    Probar un sistema **sin autorización** es un **delito** en España (acceso ilícito a sistemas, daños,
    descubrimiento de secretos) y en la mayoría de países, aunque "solo sea mirar" o "sea para ayudar".
    No hay excusa. Si dudas si algo entra en alcance: **no lo pruebes** y pregunta al programa.
    Nunca accedas a datos reales de usuarios, nunca provoques daños y nunca extorsiones. Reporta de forma
    privada y sigue un proceso de **divulgación responsable**.

## Cómo es el día a día

| Bloque | Qué haces |
| --- | --- |
| **Elegir objetivo** | Filtras programas por alcance, tecnología, competencia y reputación. |
| **Reconocimiento** | Enumeras subdominios, tecnologías, endpoints y APIs **dentro** de alcance. |
| **Pruebas manuales** | Buscas control de acceso, lógica de negocio, XSS, SSRF, IDOR, etc. |
| **Validación** | Confirmas el impacto real y descartas falsos positivos. |
| **Escritura del reporte** | Explicas pasos claros, impacto, PoC minimalista y solución propuesta. |
| **Seguimiento** | Respondes preguntas del triaje y esperas *bounty* o cierre. |

El trabajo real es **80 % reconocimiento y criterio, 20 % "click"**. Aprender a escribir bien un informe
distingue a quien cobra de quien no.

## Habilidades clave

- **Método de reconocimiento** ordenado (subdominios, puertos, *fingerprinting*, JS, APIs).
- **OWASP Top 10 y lógica de negocio**: [owasp.org](https://owasp.org) **(EN, Gratis)**.
- **Control de acceso** (IDOR/BOLA), SSRF, deserialización, inyecciones.
- **Burp Suite** y **ZAP** a fondo, incluida programación de extensiones.
- **Buenas prácticas de reporte**: claro, reproducible, con impacto.
- **Lectura de reglas**: interpretar el alcance y el *safe harbor* del programa.
- **Persistencia y ética**: saber cuándo parar y cuándo no tocar.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Completa la base con [Nivel 1 · Principiante](../nivel-1-principiante/index.md) y el
   [Nivel 2 · Medio](../nivel-2-medio/index.md) (especialmente OWASP Top 10 y Burp Suite).
2. Haz **todos** los laboratorios de [PortSwigger Web Security Academy](https://portswigger.net/web-security) **(EN, Gratis)**.
3. Lee programas y reportes **públicos** para entender el formato: *Hacktivity* de [hackerone.com](https://www.hackerone.com) **(EN, Gratis)**.
4. Sigue a **IppSec** y **John Hammond** para ver método real: [@IppSec](https://www.youtube.com/@IppSec) · [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
5. **Aún no pruebes nada fuera de un programa**: practica en laboratorio.

### Fase 2 · Medio (3–12 meses)

1. Elige una plataforma y empieza por programas con **VDP** (sin pago, buena práctica): [hackerone.com](https://www.hackerone.com) · [bugcrowd.com](https://www.bugcrowd.com) · [intigriti.com](https://www.intigriti.com) · [yeswehack.com](https://www.yeswehack.com) **(EN, Gratis)**.
2. Domina tu **pipeline de reconocimiento** (subdominios con herramientas de código abierto).
3. Practica en apps reales y vulnerables como **OWASP Juice Shop** ([owasp.org](https://owasp.org)).
4. Escribe informes impecables y acepta el triaje como aprendizaje.
5. Especialízate en una clase de fallo (p. ej., control de acceso o lógica de negocio).

### Fase 3 · Avanzado (12 meses+)

1. Cadenas de vulnerabilidades y explotación avanzada (SSRF→metadata, deserialización, *prototype pollution*).
2. Automatización propia y *tooling* a medida.
3. *Bug bounty* en programas competitivos y privados (por reputación).
4. Reconoce el límite: derivar a **pentesting profesional** o a **AppSec**.
5. Publica *writeups* **solo** cuando el programa lo permita y ya esté remediado.

## Recursos gratuitos

### Plataformas y programas

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| HackerOne | Plataforma | EN | Gratis | [hackerone.com](https://www.hackerone.com) |
| Bugcrowd | Plataforma | EN | Gratis | [bugcrowd.com](https://www.bugcrowd.com) |
| Intigriti | Plataforma | EN | Gratis | [intigriti.com](https://www.intigriti.com) |
| YesWeHack | Plataforma | EN/FR | Gratis | [yeswehack.com](https://www.yeswehack.com) |
| disclose.io | Guía de divulgación | EN | Gratis | [disclose.io](https://disclose.io) |
| PortSwigger Web Security Academy | Formación | EN | Gratis | [portswigger.net/web-security](https://portswigger.net/web-security) |

### Cursos y laboratorios

- **PortSwigger Web Security Academy**: el mejor recurso gratuito de seguridad web **(EN, Gratis)**.
- **Owasp Juice Shop** y **OWASP ZAP**: [owasp.org](https://owasp.org) · [zaproxy.org](https://www.zaproxy.org) **(EN, Gratis)**.
- **Hack The Box** y **TryHackMe**: laboratorios guiados: [hackthebox.com](https://www.hackthebox.com) · [tryhackme.com](https://tryhackme.com) **(EN, Freemium)**.
- **VulnHub**: máquinas vulnerables para practicar: [vulnhub.com](https://www.vulnhub.com) **(EN, Gratis)**.
- TODO-UJACKING: verificar y enlazar guías de bug bounty en español (blogs/comunidades) antes de recomendarlas.

### Vídeos

- **IppSec** — metodología y máquinas resueltas paso a paso: [@IppSec](https://www.youtube.com/@IppSec) **(EN, Gratis)**.
- **John Hammond** — retos web y análisis de vulnerabilidades: [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
- **LiveOverflow** — entender el "por qué" de los fallos: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.

## Certificaciones habituales

Ninguna certificación es obligatoria para hacer *bug bounty*; pesan el **reputación y los writeups**. Las
más útiles para demostrar nivel (consulta siempre la web oficial, sin precios ni formato aquí):

- **Burp Suite Certified Practitioner** — PortSwigger · [portswigger.net](https://portswigger.net).
- **OSWE** (Offensive Security Web Expert) — OffSec · [offsec.com](https://www.offsec.com).
- **eWPTX** (Web Application Penetration Tester eXtreme) — INE Security · [ine.com](https://ine.com).
- **OSCP** — base ofensiva reconocida: [offsec.com](https://www.offsec.com).

## Salidas laborales

- **Bug bounty hunter** a tiempo completo o parcial (ingresos variables; no es un sueldo fijo).
- **Penetration tester web**: ver [Pentesting web](pentesting-web.md).
- **AppSec / Product Security Engineer**: ver [AppSec y desarrollo seguro](appsec-y-desarrollo-seguro.md).
- **Red Team** a partir de la experiencia ofensiva: [Active Directory y Red Team](active-directory-y-red-team.md).
- **Security Researcher** en vendors.

El *bug bounty* funciona muy bien como **segundo ingreso** mientras te formas; mucha gente lo usa como
gimnasio para acabar en pentesting profesional. Ver [Empleabilidad](../empleabilidad/index.md).

## Siguiente paso

- Practica sin riesgo: [Nivel 2 · Medio](../nivel-2-medio/index.md).
- Si quieres seguridad de aplicaciones por dentro: [AppSec y desarrollo seguro](appsec-y-desarrollo-seguro.md).
- Índice de áreas: [Paths](index.md).
