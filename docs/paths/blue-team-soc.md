# Path · Blue Team y SOC

El **blue team** defiende. El **SOC** (Security Operations Center) es el centro desde el que se
vigila, detecta y responde a incidentes de seguridad las 24 horas. Si te tira más entender el ataque
para **detenerlo** que para ejecutarlo, este es tu camino.

!!! tip "Antes de empezar"
    Parte de la base de [Nivel 1 · Principiante](../nivel-1-principiante/index.md) y de cosas del
    [Nivel 2 · Medio](../nivel-2-medio/index.md) como redes, logs de Linux/Windows y hardening.

## Qué es y cómo es el día a día

El SOC trabaja por **turnos** y con **procesos**. Todo gira en torno a las alertas: llegan, se
clasifican (triage), se investigan y se escalan o cierran. La calidad de una detección depende de
tener buenos logs y reglas bien afinadas.

| Momento | Qué haces |
| --- | --- |
| Turno | Revisar el panel de alertas del SIEM. |
| Triage | Decidir si una alerta es ruido o amenaza real, con prisa y criterio. |
| Investigación | Correlacionar eventos, revisar endpoints, consultar inteligencia (CTI). |
| Respuesta | Aislar un equipo, bloquear un dominio, avisar al usuario. |
| Escalado | Pasar el caso a nivel 2/3 o a IR si es grave. |
| Mejora | Crear o ajustar reglas de detección para reducir falsos positivos. |

Vocabulario habitual: **SIEM** (plataforma que centraliza logs y genera alertas), **EDR**
(protección de endpoints), **IOC** (indicador de compromiso), **TTP** (tácticas, técnicas y
procedimientos del adversario).

## Habilidades clave

- **Redes y logs**: saber leer tráfico y eventos de sistema.
- **Windows y Linux** a nivel de administración y forense básico.
- **SIEM**: consultas, correlación y creación de reglas (Splunk, Elastic, Wazuh…).
- **MITRE ATT&CK** para mapear detecciones.
- **Análisis de tráfico** con Wireshark y Zeek.
- **Threat hunting** proactivo más allá de las alertas.
- **Scripting** (Python, PowerShell) para automatizar.
- **Comunicación clara** bajo presión: reportar incidentes con precisión.
- **Trabajo en equipo y turnos**: el SOC es un deporte de equipo.

## Roadmap por fases

### Fase 1 — Principiante

Objetivo: entender qué es una alerta y cómo se investiga.

- Repasa **redes** y aprende a leer **logs** de Linux y Windows.
- Familiarízate con **MITRE ATT&CK**: qué es y para qué sirve.
- Haz laboratorios de SOC guiados en **LetsDefend** y **Blue Team Labs Online**.
- Aprende **Wireshark** para distinguir tráfico normal de sospechoso.
- Practica el *triage*: clasificar alertas por severidad.

### Fase 2 — Medio

Objetivo: manejar un SIEM y consultar como un analista.

- Aprende un **SIEM**: consultas, paneles y reglas (Splunk, Elastic, Wazuh).
- Entiende **detección**: firmas, comportamiento y correlación.
- Practica **threat hunting** sobre datasets públicos de seguridad.
- Aprende respuesta básica: aislamiento, bloqueo, recogida de evidencia.
- Empieza a automatizar tareas repetitivas con **Python/PowerShell**.

### Fase 3 — Avanzado

Objetivo: diseñar detecciones y liderar investigaciones.

- **Ingeniería de detección**: crear reglas robustas y medir su eficacia.
- **Purple team**: colaborar con el red team para mejorar detecciones.
- Análisis de **cadena de ataque** completo con ATT&CK.
- **Forensia de hosts** y respuesta a incidentes (enlaza con el Path de **Forense digital e IR**).
- Liderazgo de turno y mejora continua del SOC.

## Recursos gratuitos

### Vídeos (YouTube)

- **John Hammond**: análisis y retos de seguridad, muy útil para entender ataques. **Gratis**, (EN).
- **NetworkChuck**: divulgación de redes, Linux y herramientas. **Gratis**, (EN).
- **Professor Messer**: preparación de certificaciones de fundamentos (Security+). **Gratis**, (EN).
- **13Cubed**: DFIR y artefactos forenses de Windows. **Gratis**, (EN).
- **TCM Security**: charlas divulgativas, también de defensa. **Gratis**, (EN).
- Canal raíz: [youtube.com](https://www.youtube.com).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Existen creadores y academias de **blue team y SOC en español**. Falta verificar y añadir sus
    enlaces concretos.

### Cursos y plataformas

- **LetsDefend** — simulador de SOC con alertas reales. **Freemium**. [letsdefend.io](https://letsdefend.io)
- **Blue Team Labs Online** — retos de defensa y análisis. **Freemium**. [blueteamlabs.online](https://blueteamlabs.online)
- **TryHackMe** — rutas defensivas y de SOC. **Freemium**. [tryhackme.com](https://tryhackme.com)
- **Wazuh** — SIEM/XDR open source para practicar. **Gratis**. [wazuh.com](https://wazuh.com)
- **MITRE ATT&CK** — base para mapear detecciones. **Gratis**. [attack.mitre.org](https://attack.mitre.org)
- **OWASP** — guías de seguridad aplicables a defensa. **Gratis**. [owasp.org](https://owasp.org)

### Laboratorios

- **LetsDefend** y **Blue Team Labs Online** — escenarios guiados. **Freemium**.
- **Wazuh**, **Elastic** ([elastic.co](https://www.elastic.co)) o **Splunk** ([splunk.com](https://www.splunk.com))
  para montar tu propio SIEM. **Gratis / Freemium**.
- **Wireshark** ([wireshark.org](https://www.wireshark.org)) y **Zeek** ([zeek.org](https://zeek.org))
  para análisis de tráfico. **Gratis**.

## Certificaciones habituales

!!! info "Sobre las certificaciones"
    No damos precios ni detalles de examen: consulta la web oficial de cada proveedor.

| Certificación | Proveedor | Web oficial |
| --- | --- | --- |
| BTL1 / BTL2 | Security Blue Team | [www.securityblue.team](https://www.securityblue.team) |
| CDSA | Hack The Box | [www.hackthebox.com](https://www.hackthebox.com) |
| CySA+ / Security+ | CompTIA | [www.comptia.org](https://www.comptia.org) |
| SC-200 (Security Operations Analyst) | Microsoft | [learn.microsoft.com](https://learn.microsoft.com) |
| GCIH / GCIA | GIAC (SANS) | [www.giac.org](https://www.giac.org) |
| Splunk Core Certified User | Splunk | [www.splunk.com](https://www.splunk.com) |

## Salidas laborales

- **Analista SOC N1/N2/N3** (el primer empleo más común en defensa).
- **Threat Hunter**.
- **Ingeniero de detección**.
- **Analista de respuesta a incidentes** (con IR, ver el Path de forense).
- **Analista de CTI** (inteligencia de amenazas).

Buena parte de estas ofertas se gestionan por portales: mira [Empleabilidad](../empleabilidad/index.md)
y el [índice de Paths](index.md).

!!! tip "Nota ética"
    La defensa no necesita el recordatorio ofensivo, pero sí **respetar la privacidad y las leyes**:
    los logs contienen datos personales. Trátalos con confidencialidad y sigue los procedimientos de
    tu organización.

## Siguiente paso

- Continúa con **Forense digital e IR** para el análisis en profundidad tras un incidente.
- Vuelve al [índice de Paths](index.md) para comparar áreas.
