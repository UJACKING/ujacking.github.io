# CPTS — Certified Penetration Testing Specialist (Hack The Box)

La **CPTS** es la certificación ofensiva de **Hack The Box (HTB)**, orientada a un nivel
**medio-alto**: cubre pentesting de infraestructura, **Active Directory** y web con un enfoque muy
práctico. Es una de las alternativas modernas a la OSCP y su preparación está íntimamente ligada a
la propia plataforma **HTB Academy**.

!!! warning "Verifica formato, precio y vigencia en la web oficial"
    El número de máquinas, la duración, la puntuación, el precio y las reglas de aprobado **cambian
    con el tiempo**. Esta página no los inventa: compruébalos en la web oficial de Hack The Box
    antes de inscribirte.

    TODO-UJACKING: confirmar en la web oficial de Hack The Box el nombre exacto del examen, el
    formato (tipo y número de máquinas), la duración, la puntuación mínima, el precio, los
    requisitos previos (por ejemplo, si hay que completar módulos de HTB Academy) y la vigencia del
    título.

## ¿A quién va dirigida?

| Perfil | ¿Encaja con la CPTS? |
| --- | --- |
| Quien ya domina el pentest básico y quiere un examen **exigente pero no de élite** | ✅ Sí. |
| Quien busca un título **muy orientado a Active Directory** | ✅ Encaja bien. |
| Quien empieza de cero | ❌ Antes, [Nivel 1](../nivel-1-principiante/index.md) y [Nivel 2](../nivel-2-medio/index.md). |
| Quien ya tiene la OSCP | ⚠️ Puede resultar redundante, aunque AD es un punto fuerte. |

Es el salto natural después de una **eJPT** o de haber hecho bastantes máquinas: aquí se te pide
encadenar vulnerabilidades y comprometer entornos completos, no resolver ejercicios sueltos.

## Temario a alto nivel

La CPTS gira en torno al **pentesting de infraestructura real**, con mucho peso en Windows y
entornos corporativos. Los grandes bloques son:

- **Metodología y reconocimiento**: enumeración profunda de servicios y sistemas.
- **Pentesting web**: fallos de aplicación, APIs y superficies web comunes.
- **Pentesting de infraestructura**: servicios de red, Linux y Windows.
- **Active Directory**: enumeración del dominio, abuso de configuraciones, movimiento lateral y
  escalada hasta el control del dominio.
- **Pivoting y evasión**: atravesar segmentos de red y sortear defensas básicas.
- **Post-explotación y reporting**: documentar hallazgos y proponer remediación.

Herramientas habituales: `nmap`, NetExec, Impacket, BloodHound, Responder, Metasploit y Burp Suite.

!!! info "El temario exacto es el de la web oficial"
    Estos bloques son una orientación. El listado oficial y la ruta recomendada de módulos están en
    la web de HTB.

    TODO-UJACKING: enlazar el temario y la ruta oficial de módulos de la CPTS y actualizar esta
    sección si cambian.

## Preparación con recursos gratuitos

La propia **HTB Academy** es el mejor punto de partida, y su capa gratuita permite aprender mucho
antes de pagar nada.

1. **Fundamentos**: repasa [Nivel 1](../nivel-1-principiante/index.md) y
   [Nivel 2](../nivel-2-medio/index.md) de esta web.
2. **Academy (nivel general)**: avanza por los módulos introductorios de la propia plataforma,
   incidiendo en enumeración y web antes de tocar AD.
3. **Máquinas HTB**: resuelve máquinas de dificultad creciente; las de *Active Directory* son las
   más rentables para esta certificación.
4. **Active Directory**: no te saltes AD. Domina BloodHound, Kerberos y el abuso de permisos
   delegados; es el núcleo de la CPTS.
5. **Cadena completa**: practica rutas que empiecen en un host y terminen en el **controlador de
   dominio**, porque es el escenario típico del examen.

### Checklist de preparación

- [ ] Resuelvo una fase de enumeración completa sin ayuda.
- [ ] Exploto tanto Linux como Windows.
- [ ] Me orienta un grafo de BloodHound y sé qué atacar primero.
- [ ] Hago *pivoting* entre dos redes.
- [ ] Comprendo cada hallazgo y sé escribir su remediación.

## Recursos

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Hack The Box](https://www.hackthebox.com) | Plataforma + Academy | EN | Freemium |
| [Guía de Hack The Box en esta web](../nivel-1-principiante/06-donde-practicar/02-hack-the-box.md) | Guía interna | ES | Gratis |
| [TryHackMe](https://tryhackme.com) | Plataforma guiada | EN | Freemium |

!!! note "Ética y legalidad"
    Toda la práctica de explotación debe hacerse **solo** en entornos propios o plataformas que lo
    autorizan. Nunca contra sistemas de terceros sin autorización por escrito.

## Siguiente paso

Compara con la certificación de referencia: lee la página de la **[OSCP](oscp.md)**. Si buscas
orientación de carrera, mira **[Empleabilidad](../empleabilidad/index.md)**.
