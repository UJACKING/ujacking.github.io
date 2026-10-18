# eJPT — eLearnSecurity Junior Penetration Tester

La **eJPT** es la certificación **de entrada** al pentesting profesional: un examen **práctico**
pensado para quien ya se maneja con Linux, redes y las herramientas básicas, y quiere validar su
método antes de dar el salto a certificaciones más duras. La emite **INE Security**, heredera de la
antigua **eLearnSecurity**.

!!! warning "Verifica formato, precio y vigencia en la web oficial"
    La duración, el número y tipo de máquinas, la puntuación de aprobado, el precio, el formato
    exacto y la vigencia del título **cambian con el tiempo**. Esta página **no inventa** esos
    datos: compruébalos siempre en la web oficial de INE Security antes de inscribirte.

    TODO-UJACKING: confirmar en la web oficial de INE Security el nombre comercial actual de la
    certificación, la URL exacta de su página, el formato (tipo y número de máquinas), la duración
    del examen, la puntuación mínima de aprobado, el precio y la vigencia del título.

## ¿A quién va dirigida?

| Perfil | ¿Encaja con la eJPT? |
| --- | --- |
| Persona que **empieza** en pentesting pero ya usa Linux y entiende TCP/IP | ✅ Sí, es su público natural. |
| Quien **nunca** ha abierto una terminal | ❌ Antes, completa el [Nivel 1](../nivel-1-principiante/index.md). |
| Alguien que quiere **una primera certificación práctica** sin el nivel de la OSCP | ✅ Sí. |
| Profesional con experiencia que busca un título de referencia | ⚠️ Probablemente se le queda corta. |

En resumen: es el paso lógico cuando ya has hecho tus primeras máquinas y quieres **medirte contra
un examen real** sin la exigencia (ni el coste) de las certificaciones avanzadas.

## Temario a alto nivel

A grandes rasgos, la eJPT cubre el **ciclo básico de un pentest**, con más peso en lo práctico que
en la teoría. Los bloques habituales son:

- **Fundamentos**: redes, protocolos y repaso del modelo TCP/IP.
- **Reconocimiento y footprinting**: obtener información del objetivo.
- **Enumeración**: servicios, versiones y superficies de ataque.
- **Evaluación de vulnerabilidades**: identificar fallos con criterio.
- **Ataques de red**: explotación básica de servicios de red y sistemas Windows/Linux.
- **Ataques web básicos**: las categorías más comunes del OWASP Top 10.
- **Post-explotación introductoria**: movimiento lateral y *pivoting* a nivel básico.

Herramientas que conviene dominar: `nmap`, Metasploit, Burp Suite, `netcat` y algún escáner de
vulnerabilidades.

!!! info "El temario exacto es el de la web oficial"
    Los bloques de arriba son una orientación, no el listado oficial. Contrasta la **versión vigente
    del temario** en la web de INE Security.

    TODO-UJACKING: enlazar y citar el temario oficial vigente de la eJPT y actualizar esta sección
    si cambia.

## Preparación recomendada con recursos gratuitos

No necesitas comprar un curso para preparar la eJPT. Con práctica guiada y constancia es suficiente.

1. **Consolida la base** con las páginas de esta web:
   [Nivel 1](../nivel-1-principiante/index.md) y [Nivel 2](../nivel-2-medio/index.md).
2. **Practica máquinas** en plataformas de laboratorio. Empieza por las de dificultad baja y
   documenta cada una: qué enumeraste, qué explotaste y qué aprendiste.
3. **Aprende la metodología** antes que las herramientas: haz un checklist de reconocimiento,
   enumeración, explotación y post-explotación, y aplícalo siempre en el mismo orden.
4. **Repasa web básica** en laboratorios deliberadamente vulnerables: no hace falta ser experto en
   web, solo reconocer y explotar los fallos clásicos.
5. **Cronométrate** haciendo máquinas contrarreloj para acostumbrarte a la presión del examen.

### Cómo saber si estás listo

- [ ] Encadenas reconocimiento → enumeración → explotación sin mirar chuletas.
- [ ] Te mueves por una máquina Linux y una Windows con soltura básica.
- [ ] Entiendes las vulnerabilidades web clásicas y las explotas a mano.
- [ ] Sabes documentar un hallazgo con su prueba y su remediación.
- [ ] Has resuelto varias máquinas de dificultad baja de principio a fin.

## Recursos

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Hack The Box](https://www.hackthebox.com) | Plataforma de laboratorios | EN | Freemium |
| [TryHackMe](https://tryhackme.com) | Plataforma guiada | EN | Freemium |
| [PortSwigger Web Security Academy](https://portswigger.net/web-security) | Labs de web | EN | Gratis |
| [OverTheWire](https://overthewire.org) | Wargames de Linux | EN | Gratis |
| [Página de Hack The Box en esta web](../nivel-1-principiante/06-donde-practicar/02-hack-the-box.md) | Guía interna | ES | Gratis |

!!! note "Ética y legalidad"
    Practica **solo** contra laboratorios propios o plataformas que lo autorizan expresamente.
    Atacar sistemas de terceros sin permiso por escrito es un delito.

## Siguiente paso

Cuando la eJPT te sepa a poco, sube el nivel: mira la **[CPTS](cpts.md)** o, directamente, la
**[OSCP](oscp.md)**. Si aún dudas de tu área, revisa los **[Paths](../paths/index.md)**.
