# OSCP — Offensive Security Certified Professional (OffSec)

La **OSCP** es, probablemente, **la certificación ofensiva de referencia** del sector. La emite
**OffSec** y su exigencia es alta: no se aprueba estudiando teoría, sino **demostrando** que sabes
comprometer máquinas por tu cuenta. Es un objetivo a medio-largo plazo, no una certificación de
entrada.

!!! warning "Verifica formato, precio y vigencia en la web oficial"
    El número de máquinas, la duración, la puntuación, el precio, si hay informe obligatorio y las
    reglas de aprobado **cambian con el tiempo**. Esta página **no inventa** ninguno de esos datos:
    todos deben confirmarse en la web oficial de OffSec antes de inscribirte.

    TODO-UJACKING: confirmar en la web oficial de OffSec el formato vigente del examen (tipo y
    número de máquinas, si es proctored, duración), la puntuación mínima de aprobado, si se exige
    informe, el precio, el plan de suscripción (por ejemplo, si incluye intentos) y la vigencia del
    título. No copiar datos de terceros: usar solo la fuente oficial.

## ¿A quién va dirigida?

| Perfil | ¿Encaja con la OSCP? |
| --- | --- |
| Quien ya pentestea con soltura Linux y Windows y quiere el título de referencia | ✅ Es su público natural. |
| Quien acaba de empezar | ❌ Demasiado pronto; primero [Nivel 1](../nivel-1-principiante/index.md) y [Nivel 2](../nivel-2-medio/index.md). |
| Quien busca trabajo en pentesting ofensivo / red team junior | ✅ Un gran aval en el CV. |
| Quien solo quiere "un título" sin practicar | ❌ No funciona: el examen es 100 % práctico. |

La OSCP no se aprueba memorizando: se aprueba **habiendo roto muchas máquinas antes**. Por eso la
clásica máxima **«try harder»** (inténtalo más fuerte) resume bien su filosofía.

## Filosofía del examen (sin detalles inventados)

No vamos a describir aquí el examen al detalle porque **cambia y no es necesario para prepararlo**.
Lo que sí es estable es su filosofía:

- **Es práctico y contrarreloj**: demuestras comprometer máquinas reales, no rellenas un test.
- **Exige autonomía**: no hay ayudas ni pistas; la enumeración metódica es la clave.
- **Premia la constancia y la documentación**: hay que entender cada paso y saber explicarlo.
- **Es un reto de resistencia**: se aprueba aguantando la presión y no rindiéndose.

!!! tip "Prepárate para el proceso, no para el examen"
    La mejor preparación para la OSCP es **haber resuelto muchas máquinas difíciles** y saber
    documentarlas. El día del examen solo reproduces lo que ya hiciste decenas de veces.

## Preparación con recursos gratuitos (nivel general)

No necesitas un curso de pago para empezar a prepararte, aunque la práctica intensiva es obligatoria.

1. **Base sólida** con [Nivel 1](../nivel-1-principiante/index.md) y
   [Nivel 2](../nivel-2-medio/index.md): Linux, Windows, redes, web y metodología.
2. **Máquinas de laboratorio** en plataformas como HTB o TryHackMe, subiendo de dificultad.
3. **Laboratorios de práctica ofensiva** del propio proveedor, pensados para ensayar el formato del
   examen (comprueba en la web de OffSec cuál es el vigente).
4. **Enumeración obsesiva**: es el 80 % del trabajo real. Practícala hasta que sea automática.
5. **Documentación**: escribe siempre un informe de cada máquina; te servirá también para tu
   [portfolio](../empleabilidad/index.md).

### Checklist de preparación

- [ ] Comprometo máquinas Linux y Windows de dificultad media-alta sin ayuda.
- [ ] Mi enumeración es metódica y la registro por escrito.
- [ ] Sé escalar privilegios en ambos sistemas.
- [ ] Documento cada máquina como si fuera un informe para el cliente.
- [ ] Trabajo bien bajo presión y con tiempo limitado.

## Recursos

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [OffSec](https://www.offsec.com) | Web oficial y labs | EN | De pago (con labs de pago) |
| [Hack The Box](https://www.hackthebox.com) | Plataforma de máquinas | EN | Freemium |
| [TryHackMe](https://tryhackme.com) | Plataforma guiada | EN | Freemium |
| [Guía de Hack The Box en esta web](../nivel-1-principiante/06-donde-practicar/02-hack-the-box.md) | Guía interna | ES | Gratis |

!!! warning "No inventes datos de examen"
    Si alguien te da "el formato exacto" de la OSCP: desconfía y **verifícalo en la web oficial**.
    Las condiciones cambian y lo que funcionaba hace dos años puede no valer hoy.

!!! note "Ética y legalidad"
    La OSCP se aprueba en un **entorno de examen autorizado**. Fuera de ahí, atacar sistemas sin
    permiso por escrito es ilegal.

## Siguiente paso

Si la OSCP es tu meta a largo plazo, quizá te convenga antes la **[eJPT](ejpt.md)** o la
**[CPTS](cpts.md)** como escalones. Y si quieres otras opciones, mira
**[Otras certificaciones](otras-certificaciones.md)**.
