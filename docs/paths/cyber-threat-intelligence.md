# Cyber Threat Intelligence (CTI)

**CTI** (Cyber Threat Intelligence) es convertir datos sueltos sobre amenazas en **conocimiento útil para
decidir**. No es acumular feeds de indicadores: es responder a preguntas como *¿quién nos ataca?, ¿qué
quieren?, ¿cómo lo hacen? y ¿qué hacemos al respecto?*.

El producto final es un **informe o una alerta** que ayuda a un SOC a detectar mejor, a un equipo a
priorizar parches o a la dirección a entender su riesgo real. Trabaja con MITRE ATT&CK, con feeds de
IOC y, sobre todo, con **análisis y contexto**.

## Cómo es el día a día

| Bloque | Qué haces |
| --- | --- |
| **Recolección** | Recoges datos de OSINT, feeds, dark web (con cuidado legal), malware y telemetría interna. |
| **Análisis** | Correlacionas indicadores, atribuyes campañas, mapeas tácticas y técnicas a MITRE ATT&CK. |
| **Producción** | Escribes informes tácticos (IOC), operativos y estratégicos para distintos públicos. |
| **Difusión** | Compartes con el SOC, con CERTs y con comunidades (MISP, ISACs) respetando la clasificación. |
| **Retroalimentación** | Mides si tu inteligencia sirvió: ¿se detectó antes? ¿se evitó un incidente? |
| **Investigación** | Sigues nuevas campañas, grupos APT y *malware families*. |

Es un híbrido de **OSINT + análisis + redacción + coordinación**, con mucha lectura y mucho criterio.
Mira también [OSINT](osint.md) y [Forense digital e IR](forense-digital-e-ir.md).

!!! tip "Dato no es inteligencia"
    Un IOC aislado caduca en horas. La inteligencia es un IOC **con contexto**: quién, cuándo, contra
    quién, con qué objetivo y qué hacer. Sin contexto, es ruido.

## Habilidades clave

- **Marcos y modelos**: MITRE ATT&CK ([attack.mitre.org](https://attack.mitre.org)) y la *Cyber Kill Chain*.
- **OSINT avanzado** y verificación de fuentes.
- **Análisis de malware ligero** (sin llegar a ingeniería inversa completa).
- **Redes y sistemas**: entender logs, protocolos y tráfico para dar contexto.
- **Redacción de inteligencia**: informes claros para perfiles técnicos y de negocio.
- **Estándares de intercambio**: STIX/TAXII, MISP, OpenCTI.
- **Pensamiento crítico**: distinguir señal de ruido y resistir la desinformación.
- **Idiomas**: inglés casi imprescindible para fuentes y comunidades.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Estudia **MITRE ATT&CK** de arriba abajo: [attack.mitre.org](https://attack.mitre.org) **(EN, Gratis)**.
2. Aprende qué es un **IOC** (hash, IP, dominio) y sus límites.
3. Familiarízate con el **ciclo de inteligencia** (dirección → recolección → procesamiento → análisis → difusión → feedback).
4. Haz OSINT básico para contexto: revisa [OSINT](osint.md) y [Forense y OSINT](../nivel-2-medio/11-forense-y-osint.md).
5. Crea cuenta en un feed comunitario como **AlienVault OTX**: [otx.alienvault.com](https://otx.alienvault.com) **(EN, Freemium)**.

### Fase 2 · Medio (3–12 meses)

1. Aprende a **mapear** una noticia o un informe de un vendor a técnicas ATT&CK.
2. Practica con **MISP** y **OpenCTI**: [misp-project.org](https://www.misp-project.org) · [opencti.io](https://www.opencti.io) **(EN, Gratis/Freemium)**.
3. Consulta reputación y pivota con **VirusTotal** ([virustotal.com](https://www.virustotal.com)) y **Shodan** ([shodan.io](https://www.shodan.io)).
4. Escribe tus primeros **informes** (tácticos y estratégicos) y pide feedback.
5. Sigue CERTs y organismos: [enisa.europa.eu](https://www.enisa.europa.eu), [cisa.gov](https://www.cisa.gov) **(EN, Gratis)**.

### Fase 3 · Avanzado (12 meses+)

1. Analiza campañas a fondo: atribución, infraestructura, TTPs y *diamond model*.
2. Automatiza recolección y enriquecimiento (Python, STIX/TAXII, APIs).
3. Integra CTI en detección: convierte inteligencia en **reglas de detección** y en *threat hunting*.
4. Especialízate en un sector (banca, industria, salud) o en un tipo de adversario (ransomware, APT, *hacktivismo*).
5. Comparte en comunidades e ISACs y, si puedes, habla en conferencias.

## Recursos gratuitos

### Marcos y plataformas

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| MITRE ATT&CK | Marco | EN | Gratis | [attack.mitre.org](https://attack.mitre.org) |
| MISP (plataforma de intercambio) | Herramienta | EN | Gratis | [misp-project.org](https://www.misp-project.org) |
| OpenCTI | Herramienta | EN | Freemium | [opencti.io](https://www.opencti.io) |
| AlienVault OTX | Feed | EN | Freemium | [otx.alienvault.com](https://otx.alienvault.com) |
| VirusTotal | Análisis/reputación | EN | Freemium | [virustotal.com](https://www.virustotal.com) |
| Shodan | Motor de búsqueda | EN | Freemium | [shodan.io](https://www.shodan.io) |
| abuse.ch (MalwareBazaar, URLhaus) | Feeds | EN | Gratis | [abuse.ch](https://abuse.ch) |
| ENISA / CISA (avisos) | Fuente oficial | EN | Gratis | [enisa.europa.eu](https://www.enisa.europa.eu) · [cisa.gov](https://www.cisa.gov) |

### Cursos y laboratorios

- **MITRE** publica formación y recursos de ATT&CK: [mitre.org](https://www.mitre.org) **(EN, Gratis)**.
- **TryHackMe** y **Hack The Box** tienen rutas de *threat intel* y *SOC*: [tryhackme.com](https://tryhackme.com) · [hackthebox.com](https://www.hackthebox.com) **(EN, Freemium)**.
- **SANS** *reading room* y webcasts de CTI: [sans.org](https://www.sans.org) **(EN, Freemium)**.
- TODO-UJACKING: verificar cursos de CTI en español (INTECO/INCIBE y universidades) y enlazar los vigentes.

### Vídeos

- **John Hammond** — análisis de campañas y malware en directo: [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
- **LiveOverflow** — pensamiento crítico y análisis técnico: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.
- Charlas de **conferencias de seguridad** (DEF CON, BSides, RSA) disponibles en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlaces de listas de reproducción concretas.

## Certificaciones habituales

Sin precios ni detalles de examen; comprueba siempre la web oficial.

- **GCTI** (GIAC Cyber Threat Intelligence) — SANS/GIAC · [giac.org](https://www.giac.org).
- **CTIA** (Certified Threat Intelligence Analyst) — EC-Council · [eccouncil.org](https://www.eccouncil.org).
- **CREST** tiene certificaciones de inteligencia en su catálogo: [crest-approved.org](https://www.crest-approved.org).
- **CompTIA Security+** como base: [comptia.org](https://www.comptia.org).

## Salidas laborales

- **Analista de Cyber Threat Intelligence**.
- **CTI Analyst** en un **CSIRT/CERT** o en un **SOC**.
- **Threat Hunter** (búsqueda proactiva de amenazas).
- **Analista de inteligencia** en banca, industria o sector público.
- **Research Analyst** en vendors de seguridad.
- Puente hacia **Incident Response** y **Forense digital**: [Forense digital e IR](forense-digital-e-ir.md).

Trabaja codo con codo con el [Blue Team y SOC](blue-team-soc.md). Revisa también [Empleabilidad](../empleabilidad/index.md).

## Recordatorio ético

Trabajarás con datos sensibles y, a veces, con fuentes de la dark web. Recoge información **solo** por
medios lícitos, respeta la **clasificación** de la información, no la compartas fuera de los canales
autorizados y nunca accedas a sistemas o mercados ilegales. Ante la duda, pregunta a legal.

## Siguiente paso

- Cimientos: [Nivel 2 · Medio](../nivel-2-medio/index.md) (módulos de forense, OSINT y redes).
- Áreas hermanas: [Blue Team y SOC](blue-team-soc.md) · [OSINT](osint.md).
- Índice de áreas: [Paths](index.md).
