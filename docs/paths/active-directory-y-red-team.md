# Path · Active Directory y Red Team

**Active Directory (AD)** es el sistema de directorio de Microsoft que gestiona usuarios, equipos y
permisos en la mayoría de redes corporativas. El **red team** es el equipo ofensivo que simula a un
atacante real contra una organización, encadenando fallos hasta alcanzar objetivos críticos. Este
Path combina ambos: aprender a atacar entornos de dominio y hacerlo con mentalidad de adversario.

!!! tip "Antes de empezar"
    Requiere base sólida de [Nivel 1 · Principiante](../nivel-1-principiante/index.md) y de
    [Nivel 2 · Medio](../nivel-2-medio/index.md), sobre todo Windows, redes y metodología de
    pentesting. No empieces por aquí: AD se entiende mal sin fundamentos.

## Qué es y cómo es el día a día

En un entorno de dominio, el atacante busca **credenciales** y **relaciones de confianza** para
moverse lateralmente y escalar hasta el control total (el "Domain Admin"). Kerberos, SMB, LDAP, GPOs y
delegaciones son el terreno de juego.

| Fase | Qué haces |
| --- | --- |
| Reconocimiento | Mapear el dominio, usuarios, equipos y relaciones de confianza. |
| Enumeración | Usar `BloodHound`, LDAP y herramientas de dominio para ver "el grafo". |
| Acceso inicial | Conseguir un primer usuario/equipo (phishing simulado, password spraying). |
| Movimiento lateral | Reutilizar credenciales y sesiones por la red. |
| Escalada | Abusar de Kerberos, ACLs y delegaciones para llegar a DA. |
| Objetivos | Alcanzar los "objetivos" acordados con el cliente y documentar todo. |

El trabajo de red team incluye mucha **planificación operativa**: reglas de enfrentamiento (*rules of
engagement*), ventanas autorizadas, coordinación con el blue team y un informe final muy cuidado.

## Habilidades clave

- **Windows y dominios**: estructura de AD, OUs, GPOs, confianzas.
- **Kerberos** (tickets, SPN, delegaciones) y **NTLM**.
- **Enumeración de dominio** con `BloodHound`, `PowerView`, LDAP.
- **Ataques de credenciales**: `responder`, `ntlmrelayx`, password spraying.
- **Movimiento lateral**: `PsExec`, WMI, WinRM, RDP, SMB.
- **PowerShell** y ofuscación básica.
- **C2 (Command & Control)** y operaciones encubiertas.
- **Evasion** frente a AV/EDR (conceptos, no magia).
- **Informe y coordinación** con el cliente y el equipo defensivo.

## Roadmap por fases

### Fase 1 — Principiante

Objetivo: entender la estructura de un dominio y enumerarlo.

- Repasa **Windows** y conceptos de dominio: qué son usuarios, grupos, OUs y GPOs.
- Aprende **Kerberos** a alto nivel: cómo se piden y usan los tickets.
- Monta un **laboratorio de AD** con máquinas de práctica (TryHackMe, Hack The Box).
- Enumeración básica: `net`, `whoami /all`, LDAP y primeros `BloodHound`.
- Completa rutas introductorias de AD de tu plataforma favorita.

### Fase 2 — Medio

Objetivo: explotar ataques clásicos de dominio.

- **Kerberoasting**, **AS-REP Roasting** y abuso de permisos delegados.
- **Password spraying** y reutilización de credenciales con criterio y sigilo.
- **Relay de autenticación** con `responder`/`ntlmrelayx` (en laboratorio).
- **Movimiento lateral** con credenciales y hashes.
- Interpretar el grafo de **BloodHound** y priorizar el camino a Domain Admin.
- Preparar la certificación **CRTP** de Altered Security o **CPTS** de Hack The Box.

### Fase 3 — Avanzado

Objetivo: operar como un red team completo.

- **Ataques a confianzas** entre bosques y dominios.
- **ADCS** (servicios de certificados) y sus fallos típicos.
- **C2 frameworks** y operaciones con infraestructura de ataque.
- **Evasion** de EDR y opsec (limpieza de evidencias, gestión de artefactos).
- **Red team vs. blue team**: coordinación, reglas de enfrentamiento, informe ejecutivo.
- Escritura de *tradecraft* propio y automatización de operaciones.

## Recursos gratuitos

### Vídeos (YouTube)

- **IppSec**: máquinas con AD y su resolución comentada. **Gratis**, (EN).
- **TCM Security**: curso gratuito de introducción a AD y a pentesting de dominio. **Gratis**, (EN).
- **John Hammond**: ataques y retos con AD y Kerberos. **Gratis**, (EN).
- **The Cyber Mentor** (mismo equipo que TCM): charlas y directos. **Gratis**, (EN).
- Canal raíz: [youtube.com](https://www.youtube.com).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Existen formadores y comunidades de **AD y red team en español**. Falta verificar y enlazar los
    canales concretos.

### Cursos y plataformas

- **Hack The Box Academy** — módulos de AD y un laboratorio de *Pro Labs*. **Freemium / De pago**.
  [www.hackthebox.com](https://www.hackthebox.com)
- **TryHackMe** — rutas y salas de Active Directory. **Freemium**. [tryhackme.com](https://tryhackme.com)
- **BloodHound** — herramienta clave para mapear AD. **Gratis**.
  [github.com](https://github.com)
- **MITRE ATT&CK** — catálogo de tácticas y técnicas de adversarios. **Gratis**, (EN).
  [attack.mitre.org](https://attack.mitre.org)

### Laboratorios

- **Entornos de dominio** de Hack The Box y TryHackMe. **Freemium**.
- **Laboratorio propio** con Windows Server + Windows cliente en [VirtualBox](https://www.virtualbox.org)
  o [VMware](https://www.vmware.com). **Gratis**.
- **GOAD** (Game of Active Directory): laboratorio de AD vulnerable en local. **Gratis**.
  [github.com](https://github.com)

## Certificaciones habituales

!!! info "Sobre las certificaciones"
    Sin precios ni detalles de examen: consulta siempre la web oficial del proveedor.

| Certificación | Proveedor | Web oficial |
| --- | --- | --- |
| CRTP / CRTE | Altered Security | [www.alteredsecurity.com](https://www.alteredsecurity.com) |
| PNPT | TCM Security | [www.tcm-sec.com](https://www.tcm-sec.com) |
| CPTS / CAPE | Hack The Box | [www.hackthebox.com](https://www.hackthebox.com) |
| OSCP / OSEP | OffSec | [www.offsec.com](https://www.offsec.com) |

## Salidas laborales

- **Red Team Operator** en consultoras y equipos internos.
- **Pentester de Active Directory** en auditorías internas.
- **Adversary Simulation / Purple Team**.
- **Especialista en evasion** y desarrollo de tooling ofensivo.
- **Malware/exploit developer** si te tira el bajo nivel (ver Path de **Análisis de malware**).

Prepara el salto profesional con [Empleabilidad](../empleabilidad/index.md) y compara áreas en el
[índice de Paths](index.md).

!!! danger "Recordatorio ético y legal"
    Los ataques a Active Directory son **muy** sensibles. Practica exclusivamente en tu laboratorio
    (GOAD, VMs propias) o en plataformas que lo autorizan. Atacar un dominio ajeno, incluso "en
    pruebas", es un delito grave. Nada de guías para atacar empresas reales.

## Siguiente paso

- ¿Prefieres el lado defensivo del mismo juego? Lee **Blue Team y SOC**.
- Vuelve al [índice de Paths](index.md) para seguir explorando.
