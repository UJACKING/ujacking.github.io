# Path · Forense digital e IR

La **forense digital** es la disciplina de adquirir, preservar y analizar evidencias digitales para
reconstruir qué ha pasado. La **respuesta a incidentes (IR, Incident Response)** es el proceso de
contener, erradicar y recuperarse de un incidente de seguridad. Van de la mano: tras detectar y
contener un ataque (blue team), la forense explica el *qué*, el *cómo* y el *hasta dónde*.

!!! tip "Antes de empezar"
    Parte de [Nivel 1 · Principiante](../nivel-1-principiante/index.md) (sistemas, redes, Bash) y de
    la base defensiva de [Nivel 2 · Medio](../nivel-2-medio/index.md) (logs, forense básico y OSINT).

## Qué es y cómo es el día a día

Un forense trabaja con **evidencias**: imágenes de disco, volcados de memoria, logs, tráfico de red.
La regla de oro es **no contaminar** la evidencia: se documenta la cadena de custodia y se trabaja
sobre copias.

| Momento | Qué haces |
| --- | --- |
| Preparación | Tener kit, procedimientos y herramientas listas antes de que pase algo. |
| Identificación | Determinar qué sistemas están afectados y qué evidencia recoger. |
| Preservación | Adquirir copias forenses (disco, memoria) sin alterar el original. |
| Análisis | Examinar artefactos: procesos, persistencia, registros, navegación. |
| Documentación | Cadena de custodia, *timeline* y hallazgos reproducibles. |
| Informe | Explicar qué pasó con evidencia y responder a preguntas legales/negocio. |

Vocabulario clave: **imagen forense** (copia bit a bit), **artefacto** (rastro que deja una acción),
**timeline** (línea temporal de eventos), **IOC** (indicador de compromiso), **cadena de custodia**.

## Habilidades clave

- **Sistemas operativos**: artefactos de Windows y Linux.
- **Adquisición forense**: discos, memoria, dispositivos móviles.
- **Herramientas**: Autopsy, Sleuth Kit, Volatility, FTK Imager, KAPE.
- **Análisis de logs**: eventos de Windows, Sysmon, logs de servidor.
- **Análisis de memoria**: procesos, conexiones, inyecciones.
- **Timeline y correlación** de eventos.
- **Respuesta a incidentes**: contención, erradicación, recuperación.
- **Redacción legal**: informes que puedan usarse en un procedimiento.
- **Rigor y método**: la forense es tan fuerte como su documentación.

## Roadmap por fases

### Fase 1 — Principiante

Objetivo: entender la evidencia y los artefactos básicos.

- Aprende **conceptos forenses**: cadena de custodia, integridad (`hash`), orden de volatilidad.
- Familiarízate con **Windows**: registro, eventos, prefetch, `MFT`.
- Usa **Autopsy** y **Sleuth Kit** para examinar una imagen de disco de práctica.
- Practica en **CyberDefenders** y **Blue Team Labs Online** (retos guiados).
- Aprende a generar hashes y a documentar cada paso.

### Fase 2 — Medio

Objetivo: analizar un incidente completo de principio a fin.

- **Análisis de memoria** con **Volatility**: procesos, `malfind`, conexiones.
- **Timeline** de eventos con herramientas de triaje (**KAPE**, **Plaso** en concepto).
- **Sysmon** y eventos de Windows a fondo.
- **Respuesta a incidentes**: fases PICERL (Preparación, Identificación, Contención, Erradicación,
  Recuperación, Lecciones) o equivalentes.
- Analiza **tráfico de red** con Wireshark para localizar C2 y exfiltración.
- Escribe tu primer informe forense formal.

### Fase 3 — Avanzado

Objetivo: liderar investigaciones y responder a incidentes complejos.

- **Threat hunting** sobre memoria y disco a gran escala.
- Forense de **entornos cloud y AD**.
- **Malware**: colabora con el Path de análisis de malware para casos reales.
- Herramientas **DFIR** avanzadas y automatización de triaje.
- **Peritaje** y presentación de resultados; cuidado con el lenguaje legal.
- Coordinación con equipos legales, de negocio y de comunicación.

## Recursos gratuitos

### Vídeos (YouTube)

- **13Cubed**: la referencia gratuita en DFIR de Windows; explicaciones minuciosas. **Gratis**, (EN).
- **John Hammond**: retos y análisis de artefactos y malware. **Gratis**, (EN).
- **IppSec**: menos forense, pero útil para entender el ataque que luego investigas. **Gratis**, (EN).
- **TCM Security**: introducción a la forense dentro de sus cursos gratuitos. **Gratis**, (EN).
- Canal raíz: [youtube.com](https://www.youtube.com).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Existen creadores y academias de **forense e IR en español**. Falta verificar y enlazar los canales
    concretos.

### Cursos y plataformas

- **CyberDefenders** — retos DFIR por categorías. **Freemium**. [cyberdefenders.org](https://cyberdefenders.org)
- **Blue Team Labs Online** — retos de análisis y forense. **Freemium**. [blueteamlabs.online](https://blueteamlabs.online)
- **LetsDefend** — escenarios de IR simulados. **Freemium**. [letsdefend.io](https://letsdefend.io)
- **SANS** — whitepapers y recursos gratuitos (los cursos son de pago). **Freemium**.
  [www.sans.org](https://www.sans.org)
- **MITRE ATT&CK** — para mapear el comportamiento del atacante. **Gratis**. [attack.mitre.org](https://attack.mitre.org)

### Laboratorios y herramientas

- **Autopsy / Sleuth Kit** — análisis de discos. **Gratis**.
  [www.autopsy.com](https://www.autopsy.com) · [www.sleuthkit.org](https://www.sleuthkit.org)
- **Volatility** — análisis de memoria. **Gratis**. [www.volatilityfoundation.org](https://www.volatilityfoundation.org)
- **Wireshark** — análisis de tráfico. **Gratis**. [www.wireshark.org](https://www.wireshark.org)
- **CyberDefenders** — imágenes y retos listos para analizar. **Freemium**.
- **Tu laboratorio**: VMs de [VirtualBox](https://www.virtualbox.org) o [VMware](https://www.vmware.com).
  **Gratis**.

## Certificaciones habituales

!!! info "Sobre las certificaciones"
    Sin precios ni detalles de examen: consulta siempre la web oficial del proveedor.

| Certificación | Proveedor | Web oficial |
| --- | --- | --- |
| GCFA / GCFE | GIAC (SANS) | [www.giac.org](https://www.giac.org) |
| CSFA | Security Blue Team | [www.securityblue.team](https://www.securityblue.team) |
| CDSA | Hack The Box | [www.hackthebox.com](https://www.hackthebox.com) |
| CFCE | IACIS | [www.iacis.com](https://www.iacis.com) |
| EnCE | OpenText | [www.opentext.com](https://www.opentext.com) |

## Salidas laborales

- **Analista forense digital** (DFIR).
- **Analista de respuesta a incidentes** en SOC o proveedor externo.
- **Perito informático** (ámbito judicial, requiere titulación específica).
- **Threat Hunter** con foco forense.
- **Consultor DFIR** en casos de ransomware y fraude.

Revisa [Empleabilidad](../empleabilidad/index.md) para el CV y el portfolio, y el
[índice de Paths](index.md) para comparar áreas.

!!! tip "Nota ética y legal"
    La forense maneja **datos personales** y evidencia con valor legal. Trabaja solo sobre sistemas
    que estás autorizado a analizar, respeta la privacidad y documenta la cadena de custodia. Un
    análisis mal hecho puede invalidar pruebas o perjudicar a personas.

## Siguiente paso

- Continúa con **Análisis de malware e ingeniería inversa** para entender qué ejecutó el atacante.
- Vuelve al [índice de Paths](index.md) para seguir explorando.
