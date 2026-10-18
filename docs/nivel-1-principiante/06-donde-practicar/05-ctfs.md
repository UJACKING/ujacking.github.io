# CTFs

**Aprender compitiendo.** Un CTF (*Capture The Flag*) es una competición de ciberseguridad donde
resuelves retos para conseguir "banderas" (flags). Son divertidos, gratis en su mayoría y la mejor
forma de practicar muchas habilidades distintas a la vez. Aquí te explicamos qué son y cómo empezar sin
frustrarte.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Explicar qué es un CTF y para qué sirve.
- Distinguir los dos formatos principales: **jeopardy** y **attack-defense**.
- Encontrar CTFs para principiantes (**picoCTF**) y un calendario de competiciones (**CTFtime**).
- Usar las herramientas básicas que aparecen en casi todos los retos.
- Afrontar tu primer CTF con estrategia y sin agobios.

**Tiempo estimado:** 35-50 min de lectura; tu primer CTF puede durar un fin de semana.

## Requisitos previos

- [Índice del módulo](index.md): comparativa de plataformas.
- [04 · Comandos esenciales](../04-bash/02-comandos-esenciales.md): los usarás en cada reto.
- [02 · Wireshark](../02-redes/11-wireshark.md): imprescindible para retos de red.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md): la base de todo lo ofensivo.

## Explicación

### ¿Qué es un CTF?

En un CTF se te plantean retos (normalmente con una dificultad y unos puntos) y, al resolverlos,
obtienes una **flag**: una cadena con un formato reconocible, del estilo `picoCTF{...}` o
`flag{...}`. Al introducirla en la plataforma, ganas puntos. Al final, gana quien más suma (o quien
resuelve antes los retos de más valor).

Un CTF toca muchísimos temas a la vez, lo que lo hace un entrenamiento completísimo.

### Tipos de CTF

| Tipo | Cómo funciona | Ejemplo |
| --- | --- | --- |
| **Jeopardy** | Retos "sueltos" por categorías y puntos; resuelves los que quieras | picoCTF, la mayoría de CTFs online |
| **Attack-Defense** | Cada equipo defiende un servidor y ataca el de los demás | CTFs avanzados, ligas de equipos |
| **King of the Hill** | Una máquina que todos intentan controlar; gana quien la domina | CTFs de nivel medio/alto |

Hablemos del de *jeopardy*: es, con diferencia, el más común y el mejor para empezar. Dentro de él hay
**categorías** típicas:

| Categoría | De qué va |
| --- | --- |
| **Web** | Vulnerabilidades en aplicaciones web |
| **Crypto (criptografía)** | Cifrados, hashes, matemáticas |
| **Forensics (forense)** | Analizar un fichero, una captura o un disco |
| **Reverse (ingeniería inversa)** | Entender qué hace un binario |
| **Pwn / Binary** | Explotación de binarios |
| **OSINT** | Encontrar información con fuentes abiertas |
| **Stego (esteganografía)** | Información oculta en imágenes o audios |
| **Misc (varios)** | Todo lo que no encaja en lo anterior |

### picoCTF: el CTF para empezar

**picoCTF** es un CTF pensado para principiantes, organizado por la **Universidad Carnegie Mellon
(CMU)** y **gratuito**. Tiene dos partes:

- Una **plataforma de práctica** abierta todo el año (los retos quedan disponibles después de cada
  competición), ideal para entrenar a tu ritmo.
- Una **competición anual**, normalmente en primavera, con categorías y dificultad creciente.

Es la recomendación número uno para tu primer CTF: retos bien explicados y pensados para gente que
empieza.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Las fechas exactas de la competición anual de picoCTF cambian cada año. Consulta el calendario
    vigente en [https://picoctf.org](https://picoctf.org) antes de publicar.

### CTFtime: el calendario de todo

**CTFtime** es el agregador de CTFs más usado. Ahí ves:

- Un **calendario** con las competiciones próximas y pasadas de todo el mundo.
- El **ranking** de equipos y jugadores.
- Los **writeups** (soluciones) que publica la gente al terminar.

No es una plataforma donde jugar, sino el sitio donde **enterarte** de qué CTF hay. Filtra por nivel
buscando CTFs "for beginners".

### Cómo empezar (y no frustrarte)

1. **Elige un CTF de principiantes.** No empieces por un CTF puntero: te sentirás tonto sin motivo.
2. **Forma equipo.** Un CTF en solitario es duro. Con 2-4 personas se cubren más categorías.
3. **Elige tus categorías fuertes.** No hace falta resolver todo. Empieza por las que mejor lleves
   (web, forensics suelen ser las más accesibles).
4. **Lee el enunciado dos veces.** Muchas pistas están en la propia descripción del reto.
5. **Pon un cronómetro.** Si llevas 30 min atascado, salta a otro reto y vuelve luego.
6. **Mira el writeup *después*.** Copiar la flag no enseña; leer la solución **al terminar** sí.
7. **No te compares.** Gente con años de experiencia sacará más puntos. Tu objetivo es **aprender**.

!!! tip "El éxito en tu primer CTF no son los puntos"
    Si terminas tu primer CTF habiendo resuelto **un solo reto** por ti mismo y entendiendo por qué,
    has ganado. En serio.

### Herramientas básicas

Casi todo lo que necesitas ya viene en tu distro de hacking
([módulo 03](../03-sistemas-operativos/05-elegir-distro-de-hacking.md)) o se instala fácil:

| Herramienta | Para qué |
| --- | --- |
| `curl`, `wget` | Peticiones web y descargas |
| `nc` (netcat) | Conexiones simples, puertos (`nc -lvnp 1234`) |
| `file`, `strings` | Averiguar qué es un fichero y sacarle texto |
| `xxd`, `hexdump`, `exiftool` | Ver datos crudos y metadatos |
| `binwalk`, `steghide` | Forense y esteganografía |
| `python3` | Automatizar y resolver retos de crypto |
| `john`, `hashcat` | Crackear hashes |
| **Wireshark** | Analizar capturas de red `.pcap` |
| **CyberChef** | "Navaja suiza" para decodificar/cifrar (web) |

!!! danger "Aviso ético"
    Los CTF y sus plataformas te autorizan a atacar **sus** retos. Ese es el único blanco. Usar
    técnicas de un CTF contra sistemas reales, tu universidad o tu empresa sigue siendo delito.

## Ejemplos prácticos

**1. Instalar/comprobar las herramientas básicas** en tu Kali o Parrot:

```bash
sudo apt update
sudo apt install -y netcat-openbsd curl wget binwalk steghide john
```

Explicación: `apt update` refresca la lista de paquetes; `-y` acepta la instalación sin preguntar.
Muchas de ellas ya vendrán instaladas.

**2. Inspectar un fichero "misterioso"** (típico reto de forensics). Suponiendo que el reto te da un
fichero `misterio`:

```bash
file misterio
strings misterio | grep -i flag
```

```text
misterio: PNG image data, 640 x 480, 8-bit/color RGBA   (salida de ejemplo)
... picoCTF{ejemplo_no_real}                            (salida de ejemplo)
```

- `file` — mira la "firma" del fichero y dice qué tipo es (aunque la extensión engañe).
- `strings` — extrae texto legible de un binario.
- `grep -i flag` — busca la palabra "flag" sin distinguir mayúsculas.

**3. Escuchar una conexión** (retos de "conéctate aquí"):

```bash
nc -lvnp 4444
```

- `-l` — modo escucha (listen).
- `-v` — verboso.
- `-n` — no resolver nombres DNS.
- `-p 4444` — en el puerto 4444.

**4. Analizar una captura de red** (retos de red):

```bash
wireshark captura.pcap
```

O, sin interfaz gráfica, para una búsqueda rápida:

```bash
tshark -r captura.pcap | grep -i flag
```

`tshark` es la versión de línea de comandos de Wireshark.

**5. Registrar tu progreso** en el CTF para no perderte:

```bash
printf '## picoCTF 2026 - Retos\n- [x] Web: <nombre> -> flag resuelta\n- [ ] Forensics: <nombre>\n' > ~/apuntes-ciberseguridad/ctf.md
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "No resuelvo nada y me desanimo" | CTF demasiado difícil para empezar | Pásate a picoCTF o a un CTF "for beginners" |
| "La flag no la acepta" | Formato incorrecto (mayúsculas, espacios) | Copia exactamente el texto, sin espacios |
| "Solo lo intento solo" | Un CTF es mucho para una persona | Busca equipo (foros, Discord de la comunidad) |
| "Miro el writeup al minuto" | Impaciencia | Resiste al menos 30 min; el esfuerzo es el aprendizaje |
| "Voy a por el reto de pwn" | Salta a lo más difícil | Empieza por web/forensics/misc |
| "No sé qué es un `.pcap`" | Falta base de red | Repasa el [módulo 02](../02-redes/index.md) |

## Ejercicios

1. **Define un CTF.** Explica en dos frases qué es un CTF y para qué sirve una flag.

    ??? success "Solución"
        "Un CTF es una competición de ciberseguridad con retos de distintas categorías (web, crypto,
        forensics…). La flag es una cadena que demuestra que has resuelto el reto; al introducirla,
        sumas puntos."

2. **Clasifica el formato.** ¿Cuál es la diferencia entre un CTF *jeopardy* y uno *attack-defense*?

    ??? success "Solución"
        - **Jeopardy:** retos independientes por categorías y puntos; haces los que quieras.
        - **Attack-defense:** cada equipo defiende su(s) servidor(es) y ataca los de los rivales; el
          juego es continuo y en tiempo real.

3. **Busca tu primer CTF.** Entra en [https://ctftime.org](https://ctftime.org), mira el calendario y
   anota el próximo CTF etiquetado para principiantes.

    ??? success "Solución"
        Respuesta válida = el nombre y la fecha del próximo CTF "for beginners" que aparezca **hoy**.
        No hay una respuesta fija: el calendario cambia cada semana.

4. **Practica con picoCTF.** Crea cuenta, entra en la zona de práctica y resuelve un reto de la
   categoría que prefieras. Apunta la flag y el método.

    ??? success "Solución"
        Se comprueba en la plataforma (reto marcado como resuelto). Guarda en tu repositorio:
        categoría, nombre del reto, comando o técnica usada y la flag.

5. **Usa las herramientas.** Se te da un fichero cualquiera de tu sistema y debes averiguar su tipo
   real y si contiene texto legible. Escribe los comandos.

    ??? success "Solución"
        ```bash
        file /ruta/al/fichero
        strings /ruta/al/fichero | head
        ```

        `file` da el tipo real; `strings` muestra las cadenas legibles (salida variable según el
        fichero).

6. **Plan de equipo.** Escribe cómo organizaríais un CTF de 8 horas entre 3 personas para cubrir más
   terreno.

    ??? success "Solución"
        Ejemplo válido:

        ```markdown
        Persona A: web + misc
        Persona B: forensics + crypto
        Persona C: reverse + OSINT
        Reglas: cada 60 min, puesta en común; si uno se atasca 30 min, cambia de reto;
        al final, escribir un writeup entre todos.
        ```

## Resumen

- Un **CTF** es una competición de ciberseguridad con retos y flags.
- Casi todos son **jeopardy** (retos por categorías y puntos); también hay **attack-defense**.
- **picoCTF** es gratis y el mejor para empezar; **CTFtime** es el calendario de referencia.
- Las categorías típicas: web, crypto, forensics, reverse, pwn, stego, OSINT, misc.
- Empieza por lo fácil, en equipo y sin miedo a mirar el writeup **al final**.

## Checklist

- [ ] Sé qué es un CTF, una flag y los tipos principales.
- [ ] Tengo cuenta en picoCTF.
- [ ] He mirado el calendario de CTFtime.
- [ ] Conozco las herramientas básicas (`file`, `strings`, `nc`, Wireshark…).
- [ ] He resuelto al menos un reto de principiantes.
- [ ] Tengo un plan para mi primer CTF (categorías, equipo, tiempo).

## Para ir más allá

- **picoCTF** — CTF para principiantes. Nivel: principiante. Idioma: (EN). **Gratis**.
  [https://picoctf.org](https://picoctf.org)
- **CTFtime** — Calendario y ranking de CTFs. Nivel: todos. Idioma: (EN). **Gratis**.
  [https://ctftime.org](https://ctftime.org)
- **Wireshark** (UJACKING) — Para los retos de red. [Wireshark](../02-redes/11-wireshark.md)
- **Writeups** (UJACKING) — Convierte cada CTF en una entrada de portfolio.
  [Writeups](../../empleabilidad/writeups.md)
- **Introducción a Metasploit** (Nivel 2 de UJACKING) — Para retos más avanzados.
  [Introducción a Metasploit](../../nivel-2-medio/09-introduccion-a-metasploit.md)

## Siguiente paso

Hay más plataformas donde practicar (blue team, máquinas descargables, laboratorios propios):
**[Otras plataformas](06-otras-plataformas.md)**.
