# Dónde practicar

**Teoría ya tienes. Ahora toca ensuciarse las manos.** Esta sección te da un mapa claro de las
plataformas de práctica más usadas, cuánto cuestan y en qué orden conviene atacarlas para no
perderte. La buena noticia: con lo que es **gratis** tienes para meses.

## Objetivos de aprendizaje

Al terminar esta sección serás capaz de:

- Elegir una plataforma de práctica según tu nivel, tu objetivo y tu presupuesto (que en muchos casos
  puede ser cero).
- Distinguir qué parte de cada plataforma es **gratis**, **freemium** o **de pago**.
- Seguir un **orden de práctica** razonable, semana a semana, sin saltarte los fundamentos.
- Saber cuándo una plataforma se te ha quedado pequeña y es hora de subir de nivel.

**Tiempo estimado:** 20-30 min para leer esta portada. Luego, cada plataforma tiene su propia página
(30-60 min cada una).

## Requisitos previos

Antes de lanzarte a practicar conviene tener la base y el laboratorio listos:

- [03 · Laboratorio de red virtual](../03-sistemas-operativos/07-laboratorio-red-virtual.md): tu
  entorno aislado para experimentar sin romper nada.
- [03 · Máquinas objetivo](../03-sistemas-operativos/08-maquinas-objetivo.md): las víctimas legales
  de tus pruebas.
- [04 · Comandos esenciales](../04-bash/02-comandos-esenciales.md): moverte por la terminal sin
  miedo.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md): **léelo si aún no lo has hecho**. Practicar
  sin autorización es un delito, aunque sea "solo por curiosidad".

## Explicación

### La regla de oro: practicar sin jugarte el tipo

Toda plataforma de esta sección tiene algo en común: **te autoriza explícitamente a atacarla**. Son
entornos legales *por diseño*. Eso te da una libertad enorme: puedes escanear, romper y explotar sin
mirar por encima del hombro.

!!! danger "Aviso ético (léelo de verdad)"
    Practica **solo** contra tu laboratorio propio o contra plataformas que lo autorizan por escrito
    (las de esta sección). Escanear o atacar sistemas de los que no eres responsable es un delito
    tipificado en el Código Penal español, aunque "solo mires". No hay excepciones ni "es que era una
    web de prácticas".

### Cómo elegir plataforma (criterios)

No hay una "mejor" plataforma: depende de qué buscas. Estos cuatro criterios te ayudan a decidir:

| Criterio | Pregúntate... |
| --- | --- |
| **Tu nivel** | ¿Nunca he tocado Linux? ¿Ya sé moverme por la terminal? |
| **Tu objetivo** | ¿Quiero pentesting de red, seguridad web, blue team, forense? |
| **Tu presupuesto** | ¿0 €, algo al mes, o puedo pagar una suscripción? |
| **Tu inglés** | ¿Me apaño leyendo en inglés o prefiero algo en español? |

Regla práctica: **empieza por lo gratuito y sin instalar nada**. Cuando se te quede corto, sube.

### Tabla comparativa de plataformas

!!! warning "PENDIENTE (TODO-UJACKING)"
    Los modelos de precios y las rutas de las plataformas cambian. Antes de publicar, verifica que la
    columna **"Gratis/Freemium/De pago"** sigue siendo correcta en octubre de 2026 y revisa los
    enlaces de cada sección (las URLs de planes y precios concretos se dejan fuera a propósito).

| Plataforma | Modelo | Dificultad | Enfoque | Idioma |
| --- | --- | --- | --- | --- |
| [OverTheWire](03-overthewire.md) | **Gratis** | Principiante → avanzado | Fundamentos de Linux y retos por SSH | (EN) |
| [TryHackMe](01-tryhackme.md) | **Freemium** | Principiante → medio | Rutas guiadas, todo tipo de temas | (EN) |
| [Hack The Box](02-hack-the-box.md) | **Freemium** | Medio → avanzado | Máquinas y laboratorios de pentesting | (EN) |
| [PortSwigger WSA](04-portswigger-web-security-academy.md) | **Gratis** | Principiante → avanzado | Seguridad web con laboratorios | (EN) |
| [picoCTF](05-ctfs.md) | **Gratis** | Principiante | Retos tipo CTF, muy didáctico | (EN) |
| [VulnHub](06-otras-plataformas.md) | **Gratis** | Variable | Máquinas virtuales descargables | (EN) |
| [Root-Me](06-otras-plataformas.md) | **Freemium** | Principiante → avanzado | Retos variados y CTFs | (EN/FR) |
| [LetsDefend](06-otras-plataformas.md) | **Freemium** | Principiante → medio | Blue team / SOC | (EN) |
| [Blue Team Labs Online](06-otras-plataformas.md) | **Freemium** | Principiante → medio | Blue team, forense, IR | (EN) |
| [CTFtime](05-ctfs.md) | **Gratis** | Variable | Calendario de CTFs de todo el mundo | (EN) |

!!! tip "¿Solo quieres un consejo?"
    Empieza por **[OverTheWire Bandit](03-overthewire.md)** para soltarte con Linux y sigue con
    **[TryHackMe](01-tryhackme.md)** para las rutas guiadas. Con esas dos tienes meses de trabajo
    **sin pagar nada**.

### Orden de práctica recomendado (por semanas)

Este es el orden que mejor funciona para alguien que empieza desde cero. Adáptalo a tu ritmo.

| Semanas | Qué practicar | Por qué ahora |
| --- | --- | --- |
| 1-2 | **OverTheWire · Bandit** | Te obliga a usar la terminal de verdad. |
| 3-4 | **TryHackMe · rutas de iniciación** | Aprendizaje guiado, sin frustración. |
| 5-6 | **PortSwigger · fundamentos web** | Seguridad web desde el principio, gratis. |
| 7-8 | **TryHackMe · nivel medio** + **HTB Starting Point** | Puente hacia retos menos guiados. |
| 9-10 | **picoCTF** y CTFs para principiantes | Practicas bajo presión de tiempo y en equipo. |
| 11-12 | **VulnHub** o una máquina de **HTB** | Primer reto "de verdad", de principio a fin. |

!!! note "Esto no es una carrera"
    Lo de "semanas" es orientativo. Repetir una plataforma no es perder el tiempo: es consolidar.
    Mejor una máquina resuelta por ti que diez copiadas de un writeup.

## Ejemplos prácticos

Estos no son "comandos de hacking" (todavía): son los pasos reales para **empezar hoy**.

**1. Practicar Linux sin instalar nada (OverTheWire Bandit).** Te conectas por SSH a su servidor:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Si te pide la contraseña y no lo recuerdas, la del nivel inicial está indicada en la web de
OverTheWire (es el propio nombre del usuario; confírmalo allí). Sal con `exit`.

**2. Comprobar que tu máquina de laboratorio responde** antes de ir a una plataforma online. Desde tu
distro de hacking:

```bash
ping -c 4 192.168.56.101
```

```text
PING 192.168.56.101 (192.168.56.101) 56(84) bytes of data.
64 bytes from 192.168.56.101: icmp_seq=1 ttl=64 time=0.412 ms
... (salida de ejemplo)
```

Que responda significa que tu red virtual funciona. Si no responde, revisa el
[módulo 03](../03-sistemas-operativos/07-laboratorio-red-virtual.md) antes de seguir.

**3. Guardar todo lo que aprendes.** Abre un repositorio y apunta cada reto con Git. Mañana eso será
tu portfolio (lo veremos en [Git y GitHub](../05-git-y-github/index.md)):

```bash
mkdir -p ~/apuntes-ciberseguridad && cd ~/apuntes-ciberseguridad
git init
printf '# Mis apuntes de ciberseguridad\n' > README.md
git add README.md && git commit -m "Primer apunte"
```

## Errores comunes

| Error | Qué pasa | Solución |
| --- | --- | --- |
| Pagar una suscripción el primer día | Te agobias con contenido de nivel medio | Empieza por lo gratis (Bandit + PortSwigger) |
| Saltar OverTheWire "porque es aburrido" | Te atascas en HTB porque no sabes Linux | Haz Bandit primero, son horas bien invertidas |
| Copiar el writeup sin entenderlo | Aprendes cero y no puedes repetirlo | Inténtalo tú; mira la pista, no la solución |
| Solo leer, nunca teclear | No se te queda nada | Ejecuta cada comando de cada reto |
| Perseguir todos los CTF del calendario | Cambias de tema sin profundizar | Elige uno por mes y terminalo |

## Ejercicios

1. **Decide tu punto de partida.** Escribe en un fichero `plan.md` tu nivel actual (nunca he usado
   Linux / me manejo un poco / sé programar) y elige, según la tabla, tu primera plataforma.

    ??? success "Solución"
        No hay respuesta única, pero sí una forma de justificarla. Ejemplo de entrada válida en
        `plan.md`:

        ```markdown
        Nivel: nunca he usado Linux.
        Objetivo: pentesting.
        Presupuesto: 0 € este trimestre.
        Primera plataforma: OverTheWire Bandit (semanas 1-2),
        después TryHackMe (rutas de iniciación).
        ```

        Lo importante es que la elección **encaje con tu nivel y presupuesto**, no que sea "la mejor".

2. **Reconoce el modelo de cada plataforma.** Clasifica estas tres como Gratis, Freemium o De pago:
   OverTheWire, TryHackMe, PortSwigger Web Security Academy.

    ??? success "Solución"
        - **OverTheWire:** Gratis.
        - **TryHackMe:** Freemium (hay contenido gratuito y suscripción).
        - **PortSwigger Web Security Academy:** Gratis.

3. **Diseña tu semana.** Con 6 horas semanales y la tabla de orden de práctica, reparte las horas
   entre dos plataformas y justifica el reparto.

    ??? success "Solución"
        Ejemplo para semanas 1-2:

        ```text
        Lunes   1 h  Bandit (niveles 0-3)
        Miércoles 1 h Bandit (niveles 4-6)
        Sábado  2 h Bandit (niveles 7-10) + apuntes
        Domingo 2 h Repasar y escribir el writeup semanal
        ```

        La clave: **horas fijas** y dejar un hueco para escribir lo aprendido.

4. **Monta tu registro de progreso.** Crea una tabla en `plan.md` con columnas:
   Plataforma, Reto/máquina, Fecha, Estado, Qué aprendí.

    ??? success "Solución"
        Ejemplo válido:

        ```markdown
        | Plataforma | Reto | Fecha | Estado | Qué aprendí |
        | --- | --- | --- | --- | --- |
        | Bandit | Nivel 5 | 2026-10-19 | Hecho | Buscar ficheros por permisos con `find` |
        | Bandit | Nivel 6 | 2026-10-20 | En curso | `find / -user X -group Y` |
        ```

5. **Aplica tu plan de laboratorio.** Desde tu distro de hacking, comprueba que al menos una máquina
   objetivo responde (usa `ping` y luego `nmap -sn` sobre tu red de laboratorio).

    ??? success "Solución"
        ```bash
        ping -c 2 192.168.56.101
        sudo nmap -sn 192.168.56.0/24
        ```

        En la salida de `nmap -sn` debe aparecer la IP de tu máquina objetivo como "Host is up"
        (salida de ejemplo). Si no aparece, revisa el adaptador de red de la VM (módulo 03).

6. **Evalúa el idioma.** Abre la web de TryHackMe y de Root-Me y anota en qué idiomas está disponible
   cada una. Marca cuál te resultaría más cómoda.

    ??? success "Solución"
        - **TryHackMe:** principalmente en inglés (EN).
        - **Root-Me:** inglés y francés (EN/FR).
        - Comodidad: subjetiva. Si el inglés te cuesta, apóyate en documentación en español y en el
          traductor para el primer contacto, pero **practica con el vocabulario técnico en inglés**:
          es el que te encontrarás en el trabajo.

## Resumen

- Practica **solo** en plataformas que te autorizan o en tu propio laboratorio.
- Empieza por lo **gratuito**: OverTheWire y PortSwigger dan para mucho.
- Elige plataforma según **nivel, objetivo, presupuesto e idioma**.
- Orden recomendado: **Bandit → TryHackMe → PortSwigger → HTB/picoCTF → VulnHub/HTB**.
- Documenta cada reto: tus apuntes son tu mejor activo.

## Checklist

- [ ] He leído (o releído) la página de ética y legalidad.
- [ ] Tengo mi laboratorio funcionando y una máquina objetivo que responde.
- [ ] Sé qué plataforma voy a empezar y por qué.
- [ ] He creado un `plan.md` con mi nivel, objetivo y presupuesto.
- [ ] Tengo un repositorio/Markdown donde apuntar mis retos.
- [ ] He entendido que el inglés es parte del trabajo, no un obstáculo.

## Para ir más allá

- **OverTheWire** — Retos por SSH. Nivel: principiante. Idioma: (EN). **Gratis**.
  [https://overthewire.org](https://overthewire.org)
- **TryHackMe** — Rutas guiadas. Nivel: principiante-medio. Idioma: (EN). **Freemium**.
  [https://tryhackme.com](https://tryhackme.com)
- **Hack The Box** — Máquinas y Academy. Nivel: medio-avanzado. Idioma: (EN). **Freemium**.
  [https://www.hackthebox.com](https://www.hackthebox.com)
- **PortSwigger Web Security Academy** — Seguridad web. Nivel: principiante-avanzado. Idioma: (EN).
  **Gratis**. [https://portswigger.net/web-security](https://portswigger.net/web-security)
- **Ruta perfecta de UJACKING** — Cómo encajar todo esto con tu calendario.
  [Ruta perfecta](../../ruta-perfecta.md)

## Siguiente paso

Empezamos por la plataforma más "amable": **[TryHackMe](01-tryhackme.md)**.
