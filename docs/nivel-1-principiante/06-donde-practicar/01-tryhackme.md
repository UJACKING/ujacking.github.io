# TryHackMe

**La forma más fácil y guiada de empezar en ciberseguridad.** TryHackMe es una plataforma online con
"habitaciones" (rooms) y rutas de aprendizaje que te llevan de la mano desde cero. Buena parte del
contenido de iniciación es gratuita.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Explicar qué es TryHackMe y en qué se diferencia de un laboratorio propio.
- Identificar **qué es gratis** y qué requiere suscripción, a grandes rasgos.
- Crear tu cuenta, conectarte y entrar en tu primera habitación.
- Elegir una **ruta de aprendizaje** coherente con tu nivel de principiante.

**Tiempo estimado:** 40-60 min (incluye crear cuenta y hacer tu primera habitación).

## Requisitos previos

- [Índice del módulo](index.md): criterios para elegir plataforma.
- [04 · Tuberías, redirecciones y filtros](../04-bash/03-tuberias-redirecciones-y-filtros.md):
  lo usarás constantemente en las habitaciones.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md): qué puedes y qué no puedes hacer.

## Explicación

### ¿Qué es TryHackMe?

Imagina una plataforma de cursos donde, en vez de solo leer, **haces**: cada habitación (room) mezcla
una explicación corta con tareas prácticas que se completan dentro de la propia web. Las hay muy
guiadas (te dicen qué teclear paso a paso) y otras más abiertas.

Su gran ventaja para principiantes: **no necesitas montar nada**. Puedes lanzar una máquina desde el
navegador y practicar ahí mismo.

### ¿Cómo se practica?

Hay dos formas de conectarte a las máquinas de las habitaciones:

| Método | Cómo funciona | Cuándo usarlo |
| --- | --- | --- |
| **Máquina del navegador** (AttackBox) | Lanzas un escritorio Linux desde el navegador | Cuando no tienes distro de hacking a mano |
| **Tu propia máquina + VPN** | Descargas un fichero de configuración OpenVPN y conectas tu Kali | Cuando ya tienes tu laboratorio ([módulo 03](../03-sistemas-operativos/06-montar-kali-y-parrot.md)) |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Los límites de tiempo diario de la máquina del navegador en el plan gratuito y las condiciones
    exactas de la VPN cambian con frecuencia. Verifica los detalles vigentes en la web oficial de
    TryHackMe antes de publicar: [https://tryhackme.com](https://tryhackme.com).

### ¿Qué parte es gratis?

Resumen honesto, sin inventar cifras:

- Existe un **plan gratuito** con acceso a muchas habitaciones y parte de las rutas.
- Gran parte del contenido **de iniciación** (los primeros pasos, redes, Linux básico) suele ser
  gratuito. Es justo lo que necesitas ahora.
- Las rutas **más avanzadas** y muchas habitaciones de nivel medio/alto requieren **suscripción**.

!!! tip "Empieza por lo gratis"
    Con el plan gratuito tienes material de sobra para varias semanas. Cuando se te quede corto, ya
    sabrás si te compensa la suscripción. No pagues el primer día.

### Rutas recomendadas para principiantes

TryHackMe organiza el contenido en rutas (*paths*). Algunas muy conocidas y adecuadas para empezar
son: **Pre Security**, **Introduction to Cyber Security** (antes "Complete Beginner") y, más adelante,
**Jr Penetration Tester** y **Web Fundamentals**.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Los nombres y el orden de las rutas cambian cuando la plataforma se actualiza. Confirma los
    nombres vigentes y cuáles son gratuitas en [https://tryhackme.com](https://tryhackme.com) antes
    de dar esta lista por definitiva.

Orden sugerido para ti, que vienes del Nivel 1:

1. **Pre Security** (si existe en tu cuenta): red, hardware, sistemas operativos y web a nivel muy
   básico.
2. **Introduction to Cyber Security / Complete Beginner:** los fundamentos con práctica guiada.
3. **Web Fundamentals** (si vas hacia seguridad web) o el bloque ofensivo de iniciación.

!!! danger "Aviso ético"
    Practica **solo** dentro de las habitaciones de TryHackMe y de tu propio laboratorio. Escanear o
    atacar cualquier otro sistema, aunque sea "para probar lo que he aprendido", es delito. Las
    habitaciones te autorizan; Internet no.

## Ejemplos prácticos

**1. Conectarte a TryHackMe con tu propia máquina (VPN).** Descarga el fichero `.ovpn` desde tu
perfil de TryHackMe y conéctalo. El nombre exacto del fichero puede variar:

```bash
sudo openvpn --config ~/Descargas/tun0.ovpn
```

```text
... Initialization Sequence Completed
```

Cuando ves `Initialization Sequence Completed` (salida de ejemplo), la VPN está lista. **Déjalo
abierto en esa terminal** mientras trabajas en otra.

**2. Comprobar la conexión.** Averigua tu IP en la VPN y luego comprueba que ves la IP de la máquina
de la habitación:

```bash
ip a show tun0 | grep inet
```

```text
inet 10.10.14.23/16 ... (salida de ejemplo)
```

El rango `10.10.x.x` es típico de la VPN de TryHackMe. La IP exacta que te toque **cambia en cada
sesión**.

**3. Hacer tu primera habitación.** El flujo es siempre parecido:

1. Inicia sesión y busca una habitación de iniciación (por ejemplo, la primera de la ruta elegida).
2. Pulsa "Start Machine" si la habitación tiene máquina.
3. Responde las **preguntas** de cada tarea: suele ser un dato que descubres con un comando.
4. Al terminar, mira tu racha diaria (*streak*) y tu ranking.

**4. Guardar tus notas.** Cada habitación respondida deja una "respuesta" (a menudo un hash o una
palabra). Apúntalas, te servirán para el repaso final:

```bash
printf '## Habitacion 1\nFlag: THM{ejemplo_no_real}\n' >> ~/apuntes-ciberseguridad/tryhackme.md
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "No me conecta a la máquina" | VPN caída o IP cambiada | Reconecta la VPN y revisa tu `tun0` |
| "La flag no me cuadra" | Copiaste espacios o mayúsculas mal | La flag suele ser exacta: copia y pega |
| "No entiendo nada de la habitación" | Es de un nivel superior | Baja a una de iniciación |
| Se me olvida la contraseña de la VPN | Cambia por sesión | Vuelve a descargar el `.ovpn` |
| Pierdo las notas | No apuntas | Usa un Markdown en Git, como en el módulo 05 |

## Ejercicios

1. **Crea la cuenta y haz el recorrido inicial.** Abre una cuenta, completa el perfil y encuentra la
   sección de rutas (*paths*). Anota los nombres de las rutas que aparezcan.

    ??? success "Solución"
        No hay una única respuesta: los nombres cambian. Una respuesta válida sería una lista como
        `Pre Security`, `Introduction to Cyber Security`, `Jr Penetration Tester`, `SOC Level 1`,
        verificada en la web. Lo evaluable es que **hayas identificado las rutas reales de hoy**, no
        las de un tutorial viejo.

2. **Conecta tu Kali por VPN.** Descarga el `.ovpn` y conéctate. Verifica con `ip a show tun0` que
   tienes una IP.

    ??? success "Solución"
        ```bash
        sudo openvpn --config ~/Descargas/tun0.ovpn
        # en otra terminal:
        ip a show tun0 | grep inet
        ```

        Debes ver una IP `10.10.x.x` (salida de ejemplo). Si `openvpn` no existe:
        `sudo apt update && sudo apt install openvpn`.

3. **Completa una habitación de iniciación.** Elige la primera de tu ruta y complétala, respondiendo
   todas las preguntas.

    ??? success "Solución"
        El resultado se comprueba en la propia plataforma: la habitación debe aparecer como completada
        al 100 %. Guarda en tus apuntes cada respuesta y **un comando clave** que hayas aprendido.

4. **Documenta con el método "una habitación = un writeup".** Escribe en tu repositorio un fichero
   con: objetivo, comandos usados y qué aprendiste.

    ??? success "Solución"
        Ejemplo de plantilla mínima:

        ````markdown
        # Habitación: <nombre>
        ## Objetivo
        ## Comandos usados
        ```bash
        <pega aquí los comandos>
        ```
        ## Qué aprendí
        ## Dudas pendientes
        ````

        Esto es exactamente lo que necesitarás para el módulo de
        [writeups](../../empleabilidad/writeups.md).

5. **Compara con tu laboratorio.** Enumera dos cosas que sea **más fácil** hacer en TryHackMe que en
   tu laboratorio propio, y dos que sean más cómodas en tu laboratorio.

    ??? success "Solución"
        Ejemplo válido:
        - Más fácil en TryHackMe: empezar sin montar nada; tener las respuestas verificadas.
        - Más cómodo en local: control total del entorno; practicar sin depender de tu conexión o de
          los límites del plan gratuito.

6. **Planifica dos semanas.** Con lo que has visto, escribe en `plan.md` qué habitaciones harás en
   14 días y cuántas horas les dedicarás.

    ??? success "Solución"
        Ejemplo:

        ```markdown
        Semana 1: 3 habitaciones de "Pre Security" (4 h)
        Semana 2: 3 habitaciones + 1 reto web básico (5 h)
        Repaso domingo: releer apuntes y rehacer 1 tarea sin mirar.
        ```

## Resumen

- TryHackMe es una plataforma **guiada**, ideal para empezar sin montar nada.
- Hay **plan gratuito** con material de iniciación suficiente para semanas.
- Te conectas con el **escritorio del navegador** o con **tu Kali + VPN**.
- Sigue una **ruta** (Pre Security / Introduction to Cyber Security) en orden.
- Documenta cada habitación: tus apuntes son el verdadero premio.

## Checklist

- [ ] Tengo cuenta en TryHackMe.
- [ ] Sé qué rutas hay disponibles hoy y cuál me toca.
- [ ] Me he conectado (por VPN o con la máquina del navegador).
- [ ] He completado al menos una habitación de iniciación.
- [ ] He guardado mis respuestas en un Markdown dentro de un repositorio.
- [ ] Tengo un plan de dos semanas escrito.

## Para ir más allá

- **TryHackMe** — Plataforma oficial. Nivel: principiante-medio. Idioma: (EN). **Freemium**.
  [https://tryhackme.com](https://tryhackme.com)
- **OverTheWire** — Refuerzo de Linux por SSH. Nivel: principiante. Idioma: (EN). **Gratis**.
  [https://overthewire.org](https://overthewire.org)
- **Cómo hacer writeups** (UJACKING) — Convierte tus apuntes en portfolio.
  [Writeups](../../empleabilidad/writeups.md)

## Siguiente paso

Cuando te sientas cómodo con lo guiado, toca dar el salto a retos menos dirigidos:
**[Hack The Box](02-hack-the-box.md)**.
