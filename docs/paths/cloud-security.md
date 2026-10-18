# Path · Cloud security

La **seguridad en la nube** protege los datos, aplicaciones e infraestructura que viven en
proveedores como AWS, Azure o Google Cloud. Cambia el modelo mental: ya no hay un servidor "tuyo" al
que entrar, sino **identidades, permisos y configuraciones** que hay que entender. Es una de las
áreas con más demanda y menos gente preparada.

!!! tip "Antes de empezar"
    Parte de la base de [Nivel 1 · Principiante](../nivel-1-principiante/index.md) y de
    [Nivel 2 · Medio](../nivel-2-medio/index.md) (Linux, redes, identidad). Saber algo de Docker,
    APIs y redes ayuda mucho.

## Qué es y cómo es el día a día

El trabajo es mitad **defensa** (revisar configuraciones, permisos, cumplimiento) y mitad
**seguridad ofensiva/auditoría** (buscar malas configuraciones y escaladas de privilegios en la
nube). Todo gira en torno a la **identidad**: quién puede hacer qué sobre qué recurso.

| Momento | Qué haces |
| --- | --- |
| Diseño | Definir límites, cuentas, redes y políticas de acceso (IAM). |
| Revisión | Auditar configuraciones y permisos (CIS Benchmarks). |
| Detección | Vigilar logs y alertas de la nube (CloudTrail, Defender, etc.). |
| Pentest cloud | Buscar permisos de más, buckets públicos, claves filtradas. |
| Respuesta | Contener una cuenta comprometida y rotar credenciales. |
| Cumplimiento | Encajar todo con normativas y controles internos. |

Conceptos clave: **IAM** (gestión de identidades y permisos), **bucket/objeto** (almacenamiento),
**least privilege** (privilegio mínimo), **postura de seguridad** (security posture), **CSPM**
(gestión de postura en la nube).

## Habilidades clave

- **Modelos de servicio**: IaaS, PaaS, SaaS y **responsabilidad compartida**.
- **Identidad y acceso (IAM)**: usuarios, roles, políticas, federación.
- **Redes en la nube**: VPC, subredes, grupos de seguridad, *private endpoints*.
- **Almacenamiento**: buckets, permisos, cifrado.
- **Contenedores y orquestación**: Docker, Kubernetes.
- **Infraestructura como código**: Terraform y pipelines.
- **Registro y monitorización**: logs de auditoría y de flujo.
- **Buenas prácticas**: CIS Benchmarks, centro de arquitectura segura del proveedor.
- **Scripting/CLI**: automatizar tareas con Python y las CLI oficiales.

## Roadmap por fases

### Fase 1 — Principiante

Objetivo: entender la nube y no dejar las puertas abiertas.

- Aprende el **modelo de responsabilidad compartida** de cada proveedor.
- Crea una **cuenta gratuita** (nivel gratuito) en un proveedor y trastea con consola y CLI.
- Entiende **IAM**: usuarios, roles y políticas básicas.
- Lee los **CIS Benchmarks** de la nube que elijas (son públicos).
- Aprende lo básico de **Docker** y de redes en la nube.

### Fase 2 — Medio

Objetivo: auditar y detectar malas configuraciones.

- **Postura de seguridad**: revisar IAM, almacenamiento y red frente a buenas prácticas.
- Aprende **CloudTrail**/logs de auditoría y a leer quién hizo qué.
- **Seguridad de contenedores**: imágenes, registros y Kubernetes básico.
- **Infraestructura como código**: versionar y revisar Terraform.
- Practica laboratorios de seguridad cloud (rutas específicas en plataformas de práctica).
- Empieza a automatizar auditorías con Python y las CLI.

### Fase 3 — Avanzado

Objetivo: pentest cloud y arquitectura segura a escala.

- **Pentest cloud**: escalada de privilegios por IAM, abuso de roles, *metadata*.
- **Kubernetes security** avanzado y *runtime*.
- **CSPM/CNAPP**: postura y protección de cargas de trabajo.
- **Diseño seguro**: arquitecturas multi-cuenta, *zero trust* y segmentación.
- **Respuesta a incidentes** en la nube (rotación de claves, contención).
- **Cumplimiento** y marcos (ISO, SOC 2) aplicados a la nube.

## Recursos gratuitos

### Vídeos (YouTube)

- **NetworkChuck**: tutoriales de nube (AWS/Azure) y Linux. **Gratis**, (EN).
- **John Hammond**: retos y seguridad cloud. **Gratis**, (EN).
- **TCM Security**: charlas divulgativas, con contenido cloud. **Gratis**, (EN).
- **IppSec**: útil para entender ataques que luego trasladas a la nube. **Gratis**, (EN).
- Canal raíz: [youtube.com](https://www.youtube.com).

!!! warning "PENDIENTE (TODO-UJACKING)"
    Existen creadores y academias de **cloud y DevSecOps en español**. Falta verificar y enlazar los
    canales concretos.

### Cursos y plataformas

- **AWS Skill Builder** — formación oficial gratuita y de pago. **Freemium**.
  [aws.amazon.com](https://aws.amazon.com)
- **Microsoft Learn** — rutas gratuitas, incluidas de seguridad (SC-900/SC-200/AZ-500). **Gratis**,
  (EN). [learn.microsoft.com](https://learn.microsoft.com)
- **Google Cloud Skills Boost** — laboratorios y rutas, con opciones gratuitas. **Freemium**.
  [cloud.google.com](https://cloud.google.com)
- **Docker** — documentación oficial para contenedores. **Gratis**. [docs.docker.com](https://docs.docker.com)
- **Kubernetes** — documentación oficial de orquestación. **Gratis**. [kubernetes.io](https://kubernetes.io)
- **Cloud Security Alliance** — guías de seguridad cloud. **Gratis**.
  [cloudsecurityalliance.org](https://cloudsecurityalliance.org)
- **CIS** — benchmarks de configuración segura. **Gratis** (requiere registro).
  [www.cisecurity.org](https://www.cisecurity.org)
- **OWASP** — incluye el Top 10 y proyectos cloud/Kubernetes. **Gratis**. [owasp.org](https://owasp.org)

### Laboratorios y herramientas

- **Niveles gratuitos** de AWS, Azure y Google Cloud para practicar. **Freemium**.
- **Contenedores locales** con Docker + Kubernetes (minikube) en tu máquina. **Gratis**.
- **Escáneres de postura**: herramientas open source de CSPM. **Gratis/Freemium**.
- **TryHackMe / Hack The Box** — retos y rutas de seguridad cloud. **Freemium**.
  [tryhackme.com](https://tryhackme.com) · [www.hackthebox.com](https://www.hackthebox.com)

## Certificaciones habituales

!!! info "Sobre las certificaciones"
    Sin precios ni detalles de examen: consulta siempre la web oficial del proveedor. Las
    certificaciones de nube suelen combinar fundamentos + especialidad de seguridad.

| Certificación | Proveedor | Web oficial |
| --- | --- | --- |
| AWS Certified Security – Specialty | Amazon Web Services | [aws.amazon.com](https://aws.amazon.com) |
| AZ-500 (Azure Security Engineer) | Microsoft | [learn.microsoft.com](https://learn.microsoft.com) |
| Professional Cloud Security Engineer | Google Cloud | [cloud.google.com](https://cloud.google.com) |
| CCSP | ISC2 | [www.isc2.org](https://www.isc2.org) |
| CCSK | Cloud Security Alliance | [cloudsecurityalliance.org](https://cloudsecurityalliance.org) |

## Salidas laborales

- **Cloud Security Engineer** (diseño y postura de seguridad).
- **Cloud Security Analyst / SOC cloud**.
- **Pentester de cloud** (auditorías y red team cloud).
- **DevSecOps Engineer** (seguridad en el ciclo de desarrollo).
- **Kubernetes / Container Security Engineer**.
- **Arquitecto de seguridad cloud**.

Para preparar el perfil profesional, pasa por [Empleabilidad](../empleabilidad/index.md) y vuelve al
[índice de Paths](index.md) para comparar.

!!! danger "Recordatorio ético y legal"
    Todo pentest cloud se hace **solo** contra tu propia cuenta o con **autorización por escrito** del
    propietario. Las cuentas gratuitas de laboratorio existen precisamente para esto. Escanear o
    atacar la infraestructura de un proveedor o de un cliente sin permiso es un delito y, además,
    viola los términos de servicio.

## Siguiente paso

- Cruza este Path con **Pentesting de infraestructura** para la parte on-premise.
- Vuelve al [índice de Paths](index.md) para elegir tu siguiente área.
