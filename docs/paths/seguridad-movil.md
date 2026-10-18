# Seguridad móvil

La **seguridad móvil** cubre Android e iOS: analizar aplicaciones, revisar cómo guardan los datos,
comprobar cómo se comunican con el servidor y evaluar la seguridad del propio dispositivo. Es un área
ofensiva y defensiva a la vez, con estándares muy maduros y una demanda creciente (banca, salud,
*fintech*).

Se apoya en dos pilares que conviene memorizar: **MASTG** (la guía de pruebas) y **MASVS** (el estándar de
verificación), ambos de OWASP.

## Cómo es el día a día

| Bloque | Qué haces |
| --- | --- |
| **Análisis estático** | Descompilas el APK/IPA, lees el manifiesto, revisas permisos y buscas secretos. |
| **Análisis dinámico** | Instrumentas la app con **Frida**, interceptas tráfico con **Burp**, fuerzas rutas ocultas. |
| **Pruebas de almacenamiento** | Compruebas qué se guarda en disco, en preferencias y en el *keychain/keystore*. |
| **Seguridad de red** | Verificas TLS, *certificate pinning*, y si permite downgrades o HTTP en claro. |
| **Anti-tampering** | Evalúas detección de root/jailbreak y ofuscación. |
| **Informe** | Documentas el riesgo según el **MASVS** y propones remediación. |

Herramientas típicas: **MobSF**, **Frida**, **apktool**, **jadx**, **objection**, **Ghidra**, **Burp
Suite** y emuladores/dispositivos con root o jailbreak.

!!! warning "Solo con autorización"
    Instrumentar una app con Frida o interceptar su tráfico ataca directamente a la app y a sus datos.
    Hazlo **solo** sobre apps propias, laboratorios o auditorías con **autorización por escrito**.

## Habilidades clave

- **Android**: APK, DEX, `AndroidManifest.xml`, keystore, permisos, *intents*.
- **iOS**: IPA, Mach-O, *keychain*, *entitlements*, jailbreak.
- **Instrumentación dinámica** con **Frida** ([frida.re](https://frida.re)).
- **Análisis de tráfico** y *certificate pinning* con **Burp Suite**.
- **Ingeniería inversa** básica: **jadx**, **Ghidra**.
- **Estándares OWASP**: **MASTG** y **MASVS** en [mas.owasp.org](https://mas.owasp.org).
- **Lectura de código** (Java/Kotlin, Swift/Objective-C, nativo).
- **Buenos informes**: pasos, evidencia y remediación por control del MASVS.

## Roadmap por fases

### Fase 1 · Principiante (0–3 meses)

1. Repasa [Nivel 2 · Medio](../nivel-2-medio/index.md), sobre todo redes, Burp Suite y seguridad web.
2. Familiarízate con **Android** y su modelo de seguridad: [source.android.com](https://source.android.com) **(EN, Gratis)**.
3. Prueba una **app vulnerable de laboratorio** (por ejemplo, las apps de práctica de OWASP en [owasp.org](https://owasp.org)).
4. Instala un **emulador con root** o un dispositivo de pruebas.
5. Usa **MobSF** para un análisis estático y dinámico inicial: [MobSF en GitHub](https://github.com/MobSF/Mobile-Security-Framework-MobSF) **(EN, Gratis)**.

### Fase 2 · Medio (3–12 meses)

1. Domina el **MASTG**: sigue su metodología de pruebas por capítulos en [mas.owasp.org](https://mas.owasp.org) **(EN, Gratis)**.
2. Aprende **apktool** ([apktool.org](https://apktool.org)) y **jadx** (proyecto en [github.com](https://github.com)) para descompilar.
3. Practica **Frida** para enganchar funciones y burlar comprobaciones: [frida.re](https://frida.re) **(EN, Gratis)**.
4. Intercepta tráfico y aprende a vencer *certificate pinning* con Burp.
5. Comprueba almacenamiento (preferencias, bases de datos, keychain/keystore) y cifrado en reposo.

### Fase 3 · Avanzado (12 meses+)

1. Analiza **código nativo** (JNI, librerías `.so`) con Ghidra: [ghidra-sre.org](https://ghidra-sre.org).
2. Evalúa *anti-root*, detección de Frida, ofuscación y *RASP*.
3. Audita **backend** de apps móviles (APIs, autenticación, control de acceso).
4. Automatiza pruebas en el pipeline (MobSF en CI) y define *gates* de seguridad móvil.
5. Investiga en **iOS** a fondo (jailbreak, *entitlements*, análisis de Mach-O).

## Recursos gratuitos

### Estándares y documentación

| Recurso | Tipo | Idioma | Coste | Enlace |
| --- | --- | --- | --- | --- |
| OWASP MASTG (guía de pruebas) | Guía | EN | Gratis | [mas.owasp.org](https://mas.owasp.org) |
| OWASP MASVS (verificación) | Estándar | EN | Gratis | [mas.owasp.org](https://mas.owasp.org) |
| Android Security | Documentación | EN | Gratis | [source.android.com](https://source.android.com) |
| Frida | Herramienta | EN | Gratis | [frida.re](https://frida.re) |
| MobSF | Herramienta | EN | Gratis | [GitHub](https://github.com/MobSF/Mobile-Security-Framework-MobSF) |
| apktool | Herramienta | EN | Gratis | [apktool.org](https://apktool.org) |
| Ghidra | Herramienta | EN | Gratis | [ghidra-sre.org](https://ghidra-sre.org) |

### Cursos y laboratorios

- **OWASP MASTG**: guía completa con pruebas y *crackmes* de práctica **(EN, Gratis)**.
- **Hack The Box** y **TryHackMe** incluyen retos de análisis móvil: [hackthebox.com](https://www.hackthebox.com) · [tryhackme.com](https://tryhackme.com) **(EN, Freemium)**.
- **OWASP** apps de práctica para Android/iOS: [owasp.org](https://owasp.org) **(EN, Gratis)**.
- TODO-UJACKING: verificar y enlazar laboratorios/cursos de seguridad móvil en español vigentes.

### Vídeos

- **LiveOverflow** — análisis de apps e ingeniería inversa con criterio: [@LiveOverflow](https://www.youtube.com/@LiveOverflow) **(EN, Gratis)**.
- **John Hammond** — reversing y retos móviles: [@_JohnHammond](https://www.youtube.com/@_JohnHammond) **(EN, Gratis)**.
- Charlas de **OWASP** y **DEF CON** sobre móvil en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar listas de reproducción verificadas.

## Certificaciones habituales

Consulta siempre la web oficial: sin precios ni temario de examen aquí.

- **eMAPT** (eLearnSecurity Mobile Application Penetration Tester) — INE Security · [ine.com](https://ine.com).
- **GMOB** (GIAC Mobile Device Security Analyst) — SANS/GIAC · [giac.org](https://www.giac.org).
- **OSWE / OSCP** como base ofensiva general: [offsec.com](https://www.offsec.com).

## Salidas laborales

- **Mobile Application Penetration Tester**.
- **Analista de seguridad móvil** en banca, fintech o salud.
- **AppSec Engineer** con foco móvil: ver [AppSec y desarrollo seguro](appsec-y-desarrollo-seguro.md).
- **Ingeniero/a de seguridad de producto** en equipos de apps móviles.
- **Investigador/a de malware móvil** (puente a forense/reversing).

Casa bien con [Pentesting web](pentesting-web.md) y con [Análisis de malware e ingeniería inversa](analisis-de-malware-e-ingenieria-inversa.md).
Ver también [Empleabilidad](../empleabilidad/index.md).

## Siguiente paso

- Refuerza la base web y de redes: [Nivel 2 · Medio](../nivel-2-medio/index.md).
- Salta a hardware: [Hardware e IoT](hardware-iot.md).
- Índice de áreas: [Paths](index.md).
