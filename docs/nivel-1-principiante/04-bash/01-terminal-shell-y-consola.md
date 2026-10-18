# 01 · Terminal, shell y consola

**La terminal es la ventana; el shell es el programa que interpreta lo que escribes.** Casi todo el
trabajo técnico en ciberseguridad se hace desde aquí, así que merece la pena entender bien qué es
cada pieza. En esta página aclaramos los cuatro términos que se mezclan todo el rato (terminal,
consola, shell y línea de comandos), vemos qué tipos de shell existen y abrimos la nuestra.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Distinguir con claridad **terminal**, **consola**, **shell** y **línea de comandos**.
- Entender el papel del **shell** como intérprete de comandos.
- Conocer las diferencias prácticas entre `sh`, `bash` y `zsh`.
- Abrir la terminal en Linux, macOS y Windows, y saber qué shell estás usando.
- Leer el **prompt** y lo que te está diciendo.

**Tiempo estimado: 30-45 min.**

## Requisitos previos

- Un sistema Linux operativo (físico o virtual). Si aún no tienes uno, empieza por
  [Montar Kali y Parrot](../03-sistemas-operativos/06-montar-kali-y-parrot.md).
- Saber encender una máquina virtual y hacer login. Nada de comandos, todavía.

## Explicación

### Cuatro palabras que se confunden

| Término | Qué es | Analogía |
| --- | --- | --- |
| **Terminal** | El **programa** que muestra texto en pantalla y envía lo que tecleas. Ejemplos: GNOME Terminal, Konsole, Windows Terminal, la app "Terminal" de macOS. | El teléfono. |
| **Consola** | Originalmente, el **hardware** físico (teclado + pantalla) conectado a un ordenador grande. Hoy se usa como sinónimo de terminal. | El aparato antiguo de la foto en blanco y negro. |
| **Shell** | El **programa intérprete** que lee tus comandos, los ejecuta y te devuelve el resultado. Ejemplos: `bash`, `zsh`, `sh`. | La persona que atiende la llamada y hace lo que pides. |
| **Línea de comandos** | La forma de **interactuar**: escribes texto en vez de pulsar botones. Es un modo de uso, no un programa. | Hablar, en lugar de usar una app con botones. |

En el día a día la gente dice "abre la terminal" o "abre el shell" y se refiere a lo mismo. Lo
importante es que no son un único programa: **la terminal es una aplicación gráfica, y dentro de
ella corre un shell**.

### Cómo encajan las piezas

```text
┌─────────────────────────────────────────────┐
│  TÚ (el usuario)                            │
└───────────────┬─────────────────────────────┘
                │ teclado
                ▼
┌─────────────────────────────────────────────┐
│  TERMINAL (programa con ventana)            │
│  p. ej. GNOME Terminal, Konsole, iTerm      │
└───────────────┬─────────────────────────────┘
                │ texto que escribes
                ▼
┌─────────────────────────────────────────────┐
│  SHELL (intérprete de comandos)             │
│  p. ej. bash, zsh                            │
└───────────────┬─────────────────────────────┘
                │ orden al sistema operativo
                ▼
┌─────────────────────────────────────────────┐
│  KERNEL + programas del sistema             │
│  (los comandos ls, cp, grep… que ejecutas)  │
└─────────────────────────────────────────────┘
```

El flujo es: tú escribes en la terminal → la terminal se lo pasa al shell → el shell interpreta y
lanza el programa → el resultado vuelve por el mismo camino.

### ¿Qué es exactamente un shell?

Un shell es un **intérprete de comandos**: un programa que lee una línea de texto, la traduce a
acciones (ejecutar un programa, cambiar de directorio, crear una variable…) y muestra la salida.
Shell, en inglés, significa "concha" o "envoltorio": es la capa que envuelve al sistema operativo
para que tú no tengas que hablar directamente con el kernel.

Un shell típico hace cuatro cosas:

1. **Lee** lo que escribes.
2. **Interpreta** caracteres especiales (comodines, tuberías, variables…).
3. **Ejecuta** el programa correspondiente.
4. **Devuelve** la salida y vuelve a pedirte una orden (el *prompt*).

### Tipos de shell

Existen varios shells. Estos son los que te vas a encontrar:

| Shell | Ruta habitual | Qué es | Cuándo lo usas |
| --- | --- | --- | --- |
| **`sh`** | `/bin/sh` | El shell **estándar POSIX**, el mínimo común. En muchos Linux `sh` es en realidad un enlace a `bash` o a `dash`. | Scripts que deben funcionar en cualquier sistema. |
| **`bash`** | `/bin/bash` | **Bourne Again SHell**. El shell por defecto en la mayoría de distribuciones Linux (Ubuntu, Debian, Kali…). Es el protagonista de este módulo. | Uso diario y scripts en Linux. |
| **`dash`** | `/bin/dash` | Shell pequeño y rápido, compatible con POSIX. Es el `/bin/sh` en Debian y Ubuntu. | Scripts de arranque del sistema. |
| **`zsh`** | `/bin/zsh` | Shell muy potente y configurable. Shell por defecto en macOS desde hace años. | Quien quiere autocompletado y temas avanzados. |
| **`fish`** | `/usr/bin/fish` | Shell "amigable" con sintaxis distinta a la de bash. | Uso interactivo cómodo. |
| **PowerShell** | `pwsh` | Shell de Microsoft, orientado a objetos. | Windows y administración moderna. |

!!! note "¿Por qué casi todo se enseña en bash?"
    Porque `bash` está en todas partes: es el shell por defecto de la mayoría de servidores Linux,
    el que usan las máquinas de hacking (Kali, Parrot) y el idioma común de los scripts que
    encontrarás. Si dominas `bash`, lo demás son variaciones.

### El prompt: leer la línea que te saluda

Cuando abres la terminal, ves algo parecido a esto:

```text
usuario@maquina:~$
```

Ese texto es el **prompt** (indicador). Te está diciendo varias cosas:

| Parte | Significado |
| --- | --- |
| `usuario` | El nombre del usuario con el que estás conectado. |
| `@` | Separador (léelo como "en"). |
| `maquina` | El nombre del equipo (hostname). |
| `~` | El directorio actual. `~` significa "mi carpeta personal" (`/home/usuario`). |
| `$` | Eres un **usuario normal**. |
| `#` | Eres **root** (administrador). Cuidado: aquí no hay red de seguridad. |

El prompt es configurable, así que puede verse distinto en cada sistema (con colores, con la rama de
Git, etc.). Lo importante es que **todo lo que escribes se lee hasta que pulsas `++enter++`**; solo
entonces el shell lo ejecuta.

### Abrir la terminal

=== "Linux (escritorio)"

    Tres formas rápidas:

    1. Busca "Terminal" en el menú de aplicaciones.
    2. Atajo habitual: `++ctrl+alt+t++`.
    3. Clic derecho en el escritorio → *Abrir en terminal* (según el entorno).

    Desde otro terminal, puedes abrir uno nuevo con:
    ```bash
    x-terminal-emulator &
    ```

=== "Linux (servidor, sin escritorio)"

    Cuando no hay entorno gráfico, ya estás en una terminal al iniciar sesión (una *TTY*). Puedes
    cambiar entre consolas virtuales con `++ctrl+alt+f1++` … `++ctrl+alt+f6++` y volver a la gráfica
    con `++ctrl+alt+f7++`. Comprueba en qué terminal estás:
    ```bash
    tty
    ```

=== "macOS"

    1. Finder → *Aplicaciones* → *Utilidades* → **Terminal**.
    2. O con Spotlight (`++cmd+espacio++`), escribe `Terminal`.
    3. El shell por defecto en macOS moderno es `zsh`.

=== "Windows"

    1. Instala **Windows Terminal** desde la Microsoft Store (o usa `cmd`/PowerShell).
    2. Para tener un shell tipo Linux, instala **WSL** (Windows Subsystem for Linux) y abre "Ubuntu"
       desde el menú.
    3. El shell nativo de Windows es `cmd` o **PowerShell**; no es bash.

### Saber qué shell estás usando

Dos comandos útiles:

```bash
echo $SHELL        # ruta del shell por defecto de tu usuario
echo $0            # nombre del shell que está ejecutando este comando
```

```text
/bin/bash                          (salida de ejemplo)
bash                               (salida de ejemplo)
```

`$SHELL` es una **variable de entorno** (lo veremos a fondo en la página de scripts); guarda la ruta
de tu shell. `$0` es el nombre del propio shell en ejecución.

## Ejemplos prácticos

### Ejemplo 1 · Ver quién eres y dónde estás

```bash
whoami
pwd
hostname
```

```text
usuario                            (salida de ejemplo)
/home/usuario                      (salida de ejemplo)
maquina                             (salida de ejemplo)
```

Aunque estos comandos se estudian en detalle en la página siguiente, aquí sirven para entender el
prompt: `whoami` te dice el usuario, `pwd` el directorio actual y `hostname` el nombre del equipo.
Son exactamente los datos que aparecen en `usuario@maquina:~$`.

### Ejemplo 2 · Ejecutar y salir de un shell anidado

Puedes lanzar un shell dentro de otro:

```bash
bash
```

El prompt cambia ligeramente (a veces añade un nivel). Para volver al anterior, sal:

```bash
exit
```

`exit` cierra el shell actual y te devuelve al que lo lanzó.

### Ejemplo 3 · Interrumpir y cancelar

Escribe un comando que no termine (por ejemplo, `sleep 100`) y prueba:

- `++ctrl+c++` → **interrumpe** el comando que está corriendo. Es el "botón de pánico".
- `++ctrl+d++` → envía *fin de fichero*; en un prompt vacío **cierra la sesión**.

```bash
sleep 100
# pulsa Ctrl+C para cancelarlo
```

```text
^C                                 (salida de ejemplo)
```

### Ejemplo 4 · Historial y autocompletado

El shell recuerda lo que has escrito:

- `++tab++` → **autocompleta** comandos y rutas. Púlsalo dos veces para ver opciones.
- `++up++` / `++down++` → recorre comandos anteriores.
- `++ctrl+r++` → busca en el historial (escribe parte del comando).

```bash
history
history | tail -n 5
```

```text
  501  whoami                           (salida de ejemplo)
  502  pwd                              (salida de ejemplo)
  503  bash                             (salida de ejemplo)
  504  exit                             (salida de ejemplo)
  505  history                          (salida de ejemplo)
```

`history` lista los comandos anteriores con su número; puedes repetir el número 501 escribiendo
`!501`.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "El comando no aparece" | Escribiste un comando y no pasó nada hasta pulsar `++enter++`. | Pulsa `++enter++`: el shell no ejecuta nada hasta que confirmas la línea. |
| `bash: command not found` | El programa no está instalado o no está en el `PATH`. | Revisa el nombre y si está instalado (lo veremos en la página de scripts). |
| Cierro la sesión sin querer | Pulsaste `++ctrl+d++` en un prompt vacío. | Vuelve a abrir la terminal. |
| "No me deja escribir" | Había un proceso en marcha ocupando la línea. | `++ctrl+c++` para interrumpir. |
| La terminal está en otro idioma/rara | Variables de entorno (`LANG`, `LC_*`) o config del shell. | No pasa nada por ahora; se resuelve en la configuración del shell. |
| Confundir terminal con shell | Decir "el terminal es bash". | Recuerda: la terminal es la ventana, bash es quien interpreta. |

!!! danger "No ejecutes lo que no entiendes"
    Pegar comandos copiados de internet sin leerlos es una de las formas más habituales de romper un
    sistema o de infectarse. **Lee siempre primero**. Si ves algo como `rm -rf /` o
    `curl ... | bash`, para y piensa.

## Ejercicios

1. Abre la terminal y descubre **qué shell** estás usando (ruta y nombre).
2. Averigua **qué usuario** eres y **cómo se llama** tu equipo.
3. Lanza un shell anidado con `bash` y sal de él. ¿Cuántos niveles de shell encadenas como máximo?
4. Usa `++ctrl+r++` para recuperar el primer comando que ejecutaste en esta sesión.
5. Encuentra en tu sistema la ruta real del binario `bash` (pista: el comando `which` te ayuda) y
   comprueba si `/bin/sh` es un enlace simbólico y a qué apunta.
6. *(Opcional)* Averigua la versión de tu shell.

??? success "Solución"

    **1. Qué shell usas:**
    ```bash
    echo $SHELL
    echo $0
    ```
    Verás algo como `/bin/bash` y `bash` (o `zsh` en macOS).

    **2. Usuario y máquina:**
    ```bash
    whoami
    hostname
    ```

    **3. Shell anidado:**
    ```bash
    bash
    bash
    exit
    exit
    ```
    Cada `bash` abre un nivel nuevo; cada `exit` cierra uno. El límite depende del sistema, pero no
    es una buena idea anidar más de dos o tres.

    **4. Buscar en el historial:**
    Pulsa `++ctrl+r++` y empieza a escribir. El shell muestra la coincidencia más reciente.

    **5. Ruta del binario y enlace de `sh`:**
    ```bash
    which bash
    ls -l /bin/sh
    ```
    Salida típica (ejemplo): `/usr/bin/bash` y `lrwxrwxrwx ... /bin/sh -> dash` en Debian/Ubuntu.

    **6. Versión del shell:**
    ```bash
    bash --version | head -n 1
    ```
    Salida de ejemplo: `GNU bash, version 5.x.x`

## Resumen

- **Terminal** = el programa con ventana; **shell** = el intérprete que ejecuta tus comandos.
- **Consola** era el hardware físico; hoy es sinónimo de terminal.
- **Línea de comandos** es el modo de uso (texto en lugar de botones).
- `sh` es el estándar POSIX; `bash` el shell dominante en Linux; `zsh` el de macOS.
- El **prompt** muestra usuario, máquina, directorio actual y si eres usuario (`$`) o root (`#`).
- `++ctrl+c++` interrumpe, `++ctrl+d++` cierra la sesión, `++tab++` autocompleta y `++ctrl+r++`
  busca en el historial.

## Checklist

- [ ] Sé explicar la diferencia entre terminal, shell, consola y línea de comandos.
- [ ] Sé qué shell uso por defecto y cómo comprobarlo.
- [ ] Sé abrir la terminal en mi sistema.
- [ ] Entiendo qué me está diciendo el prompt.
- [ ] Sé interrumpir un comando (`++ctrl+c++`) y cerrar la sesión (`++ctrl+d++`).
- [ ] Uso el autocompletado con `++tab++` y el historial con `++ctrl+r++`.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [GNU Bash](https://www.gnu.org/software/bash/) | Documentación oficial del shell | EN | Gratis |
| [Linux man pages](https://man7.org) | Referencia de comandos y manuales | EN | Gratis |
| [The Linux Command Line (William Shotts)](https://linuxcommand.org) | Libro gratuito en PDF | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta una recomendación de recurso en **español** sobre introducción a la terminal. Debe
    añadirlo un redactor que verifique que el enlace sigue vivo.

## Siguiente paso

Ahora que sabes qué es el shell, vamos a hacerlo trabajar:
**[02 · Comandos esenciales](02-comandos-esenciales.md)**.
