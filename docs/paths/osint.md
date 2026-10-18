# Path · OSINT

**OSINT** (Open Source Intelligence, inteligencia de fuentes abiertas) es la disciplina de recopilar
y analizar información **pública** para responder preguntas concretas: la superficie de exposición de
una empresa, la identidad de un actor, la veracidad de una noticia o los datos que un atacante podría
encontrar sobre ti. Se usa en red team, fraude, periodismo, inteligencia y seguridad corporativa.

!!! warning "Límite legal importante"
    OSINT trabaja con información **pública**, pero eso no significa que todo valga. El **acoso**, el
    **doxxing**, la suplantación de identidad y la vigilancia de personas sin motivo legítimo son
    **delitos o faltas**, aunque uses fuentes abiertas. Practica con objetivos ficticios o con tu
    propio rastro digital.

!!! tip "Antes de empezar"
    Parte de [Nivel 1 · Principiante](../nivel-1-principiante/index.md) (redes, Linux, Git) y de la
    base de [Nivel 2 · Medio](../nivel-2-medio/index.md), donde se toca OSINT de forma introductoria.

## Qué es y cómo es el día a día

OSINT es más **investigación** que tecnología. Se trabaja con hipótesis, se anotan fuentes, se
verifica y se cruza información. La clave es el **rigor**: una fuente no es una verdad.

| Momento | Qué haces |
| --- | --- |
| Definir objetivo | ¿Qué pregunta intento responder exactamente? |
| Planificar | Elegir fuentes y herramientas; fijar límites éticos. |
| Recopilar | Buscar en web, redes sociales, registros públicos, metadatos. |
| Verificar | Confirmar cada dato con al menos dos fuentes. |
| Correlacionar | Unir piezas en un grafo o mapa de relaciones. |
| Informar | Presentar hallazgos con evidencia y nivel de confianza. |

Herramientas típicas: buscadores, **OSINT Framework**, **Shodan**, **Have I Been Pwned**,
**Maltego** y **theHarvester**.

## Habilidades clave

- **Búsqueda avanzada**: operadores de buscador, filtros, `dorks`.
- **Análisis de metadatos** (EXIF de fotos, documentos).
- **Redes sociales**: perfiles, conexiones, patrones de publicación.
- **Infraestructura**: dominios, subdominios, certificados, DNS, WHOIS.
- **Verificación**: geolocalización, cronolocalización, verificación de imágenes.
- **Documentación**: notas, fuentes, *timeline*.
- **Ética y marco legal**: qué es público, qué es dato personal.
- **Análisis**: convertir datos dispersos en conclusiones defendibles.

## Roadmap por fases

### Fase 1 — Principiante

Objetivo: saber buscar y documentar como un investigador.

- Aprende **operadores de búsqueda** y a formular preguntas concretas.
- Practica el **rastreo de tu propio rastro digital** (¿qué hay de ti en internet?).
- Aprende a leer **metadatos** de imágenes y documentos.
- Familiarízate con **OSINT Framework** para ver el mapa de fuentes por categoría.
- Haz retos de OSINT sencillos y documenta cada paso.

### Fase 2 — Medio

Objetivo: investigar infraestructura y personas con método.

- **Reconocimiento de infraestructura**: dominios, subdominios, certificados, DNS.
- **Shodan** y **Censys** para encontrar dispositivos y servicios expuestos.
- **Have I Been Pwned** y filtraciones para evaluar exposición de credenciales.
- **Maltego** para construir grafos de relaciones.
- **Verificación de imágenes y geolocalización** (geoint).
- Practica con **Trace Labs** u objetivos benéficos/de CTF, nunca con personas.

### Fase 3 — Avanzado

Objetivo: producir inteligencia accionable y a escala.

- **OSINT para red team**: perfilado de objetivos, empleados y tecnología.
- **CTI** (inteligencia de amenazas): atribución, seguimiento de actores.
- **Automatización**: scripts que recopilan y normalizan datos.
- **Colección encubierta** y *sock puppets* (siempre dentro de la legalidad).
- **Informes de inteligencia** con estimación de confianza.
- Colabora con equipos de fraude, abuso o seguridad corporativa.

## Recursos gratuitos

### Vídeos (YouTube)

- **OSINT Curious** (comunidad): charlas y técnicas de OSINT. **Gratis**, (EN).
- **John Hammond**: retos y uso de herramientas OSINT. **Gratis**, (EN).
- **NetworkChuck**: divulgación de redes y herramientas. **Gratis**, (EN).
- **TCM Security**: OSINT dentro de su formación de pentesting. **Gratis**, (EN).
- Canal raíz: [youtube.com](https://www.youtube.com).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Existen formadores y comunidades de **OSINT en español** (muy activas en Latinoamérica y España).
    Falta verificar y enlazar los canales concretos.

### Cursos y plataformas

- **OSINT Framework** — directorio de recursos por tipo de dato. **Gratis**.
  [osintframework.com](https://osintframework.com)
- **Bellingcat** — guías de investigación y verificación. **Gratis**, (EN). [www.bellingcat.com](https://www.bellingcat.com)
- **Trace Labs** — CTFs de OSINT con fines solidarios. **Gratis**. [www.tracelabs.org](https://www.tracelabs.org)
- **SANS** — whitepapers de OSINT (los cursos son de pago). **Freemium**. [www.sans.org](https://www.sans.org)
- **MITRE ATT&CK** — contexto de actores y TTPs. **Gratis**. [attack.mitre.org](https://attack.mitre.org)

### Laboratorios y herramientas

- **Shodan** — buscador de dispositivos conectados. **Freemium**. [www.shodan.io](https://www.shodan.io)
- **Have I Been Pwned** — comprobación de filtraciones. **Gratis**. [haveibeenpwned.com](https://haveibeenpwned.com)
- **Maltego** — análisis y visualización de relaciones. **Freemium**. [www.maltego.com](https://www.maltego.com)
- **Censys** — búsqueda de servicios en internet. **Freemium**. [censys.com](https://censys.com)
- **theHarvester** — recopilación de correos y subdominios. **Gratis**. [github.com](https://github.com)

## Certificaciones habituales

!!! info "Sobre las certificaciones"
    Sin precios ni detalles de examen: consulta siempre la web oficial del proveedor. Las
    certificaciones específicas de OSINT son menos comunes que en otras áreas.

| Certificación | Proveedor | Web oficial |
| --- | --- | --- |
| GOSI (Open Source Intelligence) | GIAC (SANS) | [www.giac.org](https://www.giac.org) |
| CTIA (Threat Intelligence) | EC-Council | [www.eccouncil.org](https://www.eccouncil.org) |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Las certificaciones específicas de OSINT son minoritarias y cambian de proveedor a proveedor.
    Falta verificar cuáles están vigentes y enlazar sus webs oficiales.

## Salidas laborales

- **Analista de OSINT / Intelligence**.
- **Analista de fraude** o de abuso.
- **Red Team** (OSINT como fase de reconocimiento).
- **Periodista de investigación** o verificador de hechos (fact-checking).
- **Analista de CTI** centrado en actores y campañas.

Revisa [Empleabilidad](../empleabilidad/index.md) y el [índice de Paths](index.md) para orientarte.

!!! danger "Recordatorio ético y legal"
    La información pública sigue siendo, en muchos casos, **dato personal** protegido. No la
    recopiles ni la publiques sin base legal. Nada de acosar, doxxear ni vigilar personas. Si tu
    investigación no tiene un fin legítimo y autorizado, **no la hagas**.

## Siguiente paso

- Continúa con **Cyber Threat Intelligence** si te interesa aplicar OSINT a amenazas.
- Vuelve al [índice de Paths](index.md) para comparar áreas.
