# 04 · Scripts en Bash

**Un script es una receta: una lista de comandos guardados en un fichero que el shell ejecuta por
ti.** Si haces algo más de una vez, conviértelo en script: ahorras tiempo y evitas errores. En esta
página aprendes las piezas del lenguaje (variables, condiciones, bucles, funciones, argumentos) y las
aplicas en **cinco scripts reales** que puedes usar desde hoy: copia de seguridad, barrido de red,
mini escáner de puertos, análisis de logs y renombrado masivo.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Escribir un script con *shebang*, permisos y ejecución correcta.
- Usar **variables**, variables de entorno y entender el `PATH`.
- Diferenciar el uso de **comillas simples** y **dobles**.
- Escribir condicionales (`if`) y bucles (`for`, `while`).
- Definir y usar **funciones**.
- Leer **argumentos** (`$1`, `$@`, `$#`) y **códigos de salida** (`$?`).
- Automatizar tareas con **cron**.
- Aplicar **buenas prácticas**: `set -euo pipefail`, comillas y `shellcheck`.
- Escribir y entender cinco **scripts completos y funcionales**.

**Tiempo estimado: 120-150 min.**

## Requisitos previos

- [Comandos esenciales](02-comandos-esenciales.md) y
  [Tuberías, redirecciones y filtros](03-tuberias-redirecciones-y-filtros.md).

!!! danger "Ética y legalidad"
    Dos de los scripts de esta página (barrido de red y escáner de puertos) son **herramientas de
    reconocimiento**. Úsalos **solo** contra **tu propio laboratorio** (tu red local, tus máquinas
    virtuales) o contra plataformas que lo autorizan por escrito. Escanear redes o equipos que no
    son tuyos **es ilegal** en muchos países. Lo mismo vale para probarlos en casa del vecino: no.

## Explicación

### Anatomía de un script

Un script de Bash es un fichero de texto con extensión `.sh` (por convención) que empieza por el
*shebang*:

```bash
#!/usr/bin/env bash
```

El **shebang** (`#!`) le dice al sistema **con qué intérprete** ejecutar el fichero. Usar
`/usr/bin/env bash` localiza `bash` en el `PATH` del sistema, lo que lo hace más portable que poner
`#!/bin/bash` a pelo.

Para ejecutarlo, dale permiso de ejecución y llámalo:

```bash
chmod +x script.sh
./script.sh
```

Sin `./` delante, el shell busca `script.sh` en el `PATH`, no en la carpeta actual.

### Variables

Una variable guarda un valor. **No se pone espacio** alrededor del `=`:

```bash
nombre="Ana"          # correcto
nombre = "Ana"        # ERROR: intenta ejecutar el comando "nombre"
```

Para **usar** el valor, se pone `$` delante:

```bash
echo "Hola, $nombre"     # Hola, Ana
echo "Hola, ${nombre}!"  # con llaves, para delimitar el nombre de la variable
```

Las llaves `{}` son obligatorias cuando el nombre va pegado a texto: `${nombre}_backup` no es lo
mismo que `$nombre_backup` (esta última busca la variable `nombre_backup`).

### Variables de entorno y el PATH

Algunas variables son **de entorno**: las heredan todos los programas que lanzas. Las más útiles:

| Variable | Contiene |
| --- | --- |
| `$HOME` | Tu carpeta personal. |
| `$USER` | Tu nombre de usuario. |
| `$PWD` | El directorio actual. |
| `$PATH` | La lista de carpetas donde el shell busca los comandos. |
| `$SHELL` | Tu shell por defecto. |

El **`PATH`** es una lista de directorios separados por `:`. Cuando escribes `ls`, el shell recorre
esas carpetas hasta encontrarlo:

```bash
echo "$PATH"
```

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin   (salida de ejemplo)
```

Para exportar una variable a los programas hijos se usa `export`:

```bash
export EDITOR="nano"
```

!!! warning "Nunca hagas esto"
    Poner `.` (el directorio actual) al principio del `PATH` es peligroso: podrías ejecutar un
    programa malicioso llamado `ls` sin darte cuenta. Evítalo.

### Comillas simples vs dobles

Es una de las fuentes de errores más habituales:

| Comillas | Comportamiento | Ejemplo | Resultado |
| --- | --- | --- | --- |
| **Dobles** `"..."` | **Interpolan** variables y `$(...)`. | `echo "Hola $USER"` | `Hola ana` |
| **Simples** `'...'` | **Literal**: no interpretan nada. | `echo 'Hola $USER'` | `Hola $USER` |

Regla práctica: **si no quieres que se interprete nada, usa comillas simples**; si necesitas
variables, comillas dobles.

### Códigos de salida y `$?`

Cada comando devuelve un número al terminar: su **código de salida**.

- `0` → éxito.
- Cualquier otro número → error.

Se lee con `$?` (el código del **último** comando ejecutado):

```bash
ls /etc >/dev/null
echo $?          # 0  (existe)
ls /nada 2>/dev/null
echo $?          # 2  (no existe)
```

También se puede usar directamente en condiciones:

```bash
if ping -c 1 -W 1 8.8.8.8 &>/dev/null; then
  echo "Hay conexión"
fi
```

### Condicionales: `if`

```bash
if [[ condicion ]]; then
  # se ejecuta si es verdadera
elif [[ otra_condicion ]]; then
  # si la primera es falsa pero esta es verdadera
else
  # si ninguna es verdadera
fi
```

Operadores útiles dentro de `[[ ]]`:

| Operador | Significa |
| --- | --- |
| `-f fichero` | Es un fichero normal. |
| `-d fichero` | Es un directorio. |
| `-e fichero` | Existe (fichero o directorio). |
| `-z "$var"` | La variable está vacía. |
| `-n "$var"` | La variable **no** está vacía. |
| `-eq`, `-ne`, `-gt`, `-lt` | Comparan **números**. |
| `=`, `!=` | Comparan **cadenas**. |

!!! tip "Usa `[[ ]]`, no `[ ]`"
    `[[ ]]` es la forma moderna de bash: soporta comodines, `&&`, `||` y no exige escapar tanto.
    `[ ]` (que es el comando `test`) es POSIX pero más frágil.

### Bucles: `for` y `while`

**`for`** recorre una lista:

```bash
for fruta in pera manzana platano; do
  echo "Me gusta la $fruta"
done
```

**`while`** repite mientras se cumpla una condición:

```bash
contador=1
while [[ $contador -le 3 ]]; do
  echo "Vuelta $contador"
  ((contador++))
done
```

`((contador++))` incrementa la variable. Para bucles sobre las líneas de un fichero, la forma
correcta:

```bash
while IFS= read -r linea; do
  echo "Línea: $linea"
done < fichero.txt
```

`IFS= read -r` conserva los espacios y las barras invertidas: es la manera segura de leer líneas.

### Funciones

Una función agrupa comandos bajo un nombre para reutilizarlos:

```bash
saludar() {
  local nombre="$1"          # $1 = primer argumento de la función
  echo "Hola, $nombre"
}

saludar "Mundo"              # Hola, Mundo
```

- `local` hace que la variable solo exista dentro de la función (evita pisar variables globales).
- Los argumentos de una función se leen igual que los del script: `$1`, `$2`…

### Argumentos del script

| Variable | Contiene |
| --- | --- |
| `$1`, `$2`, … | El primer, segundo… argumento. |
| `$0` | El nombre del script. |
| `$#` | Número de argumentos. |
| `$@` | Todos los argumentos (como lista). |
| `"$@"` | Todos los argumentos respetando los espacios (¡usa **siempre** `"$@"`!). |

```bash
#!/usr/bin/env bash
echo "Script: $0"
echo "Argumentos: $#"
for arg in "$@"; do
  echo " - $arg"
done
```

### `set -euo pipefail`: tu cinturón de seguridad

Casi todos los scripts de esta página empiezan con:

```bash
set -euo pipefail
```

Desglosado:

| Opción | Qué hace |
| --- | --- |
| `-e` | **Aborta** el script si un comando falla. |
| `-u` | **Error** si usas una variable que no existe (evita resultados catastróficos). |
| `-o pipefail` | Un pipeline falla si **cualquiera** de sus comandos falla, no solo el último. |

Casi siempre quieres las tres. Son la diferencia entre "el script siguió adelante y borró lo que no
debía" y "el script se paró al primer error".

### Comillas: la regla de oro

**Pon comillas alrededor de todas las variables.** `rm -rf "$carpeta"` es seguro; `rm -rf $carpeta`
puede borrar lo que no toca si la variable está vacía o tiene espacios. Con `set -u` te proteges de
las variables vacías, pero las comillas siguen siendo obligatorias.

### `cron`: ejecutar scripts automáticamente

`cron` es el planificador de tareas de Linux. Editas tu tabla de tareas con:

```bash
crontab -e
```

Cada línea tiene **cinco campos de tiempo** y el comando:

```text
┌─── minuto (0-59)
│ ┌─── hora (0-23)
│ │ ┌─── día del mes (1-31)
│ │ │ ┌─── mes (1-12)
│ │ │ │ ┌─── día de la semana (0-7, donde 0 y 7 = domingo)
│ │ │ │ │
* * * * *  comando_a_ejecutar
```

| Expresión | Significa |
| --- | --- |
| `0 3 * * *` | Todos los días a las 03:00. |
| `*/15 * * * *` | Cada 15 minutos. |
| `0 9 * * 1` | Todos los lunes a las 09:00. |
| `30 6 1 * *` | El día 1 de cada mes a las 06:30. |

Ejemplo real:

```cron
0 3 * * * /home/ana/scripts/backup.sh /home/ana/Documentos /home/ana/backups >> /home/ana/backups/backup.log 2>&1
```

!!! warning "`cron` tiene un `PATH` mínimo"
    Cuando `cron` ejecuta tu script, el `PATH` es muy reducido. Usa **rutas absolutas** a los
    comandos o define el `PATH` al principio del script. También conviene redirigir la salida a un
    log (`>> log 2>&1`), porque si no, no verás qué pasó.

### `shellcheck`: tu revisor automático

[ShellCheck](https://www.shellcheck.net) analiza tus scripts y te avisa de errores y malas prácticas
(variables sin comillas, comparaciones mal hechas, etc.). Es la mejor inversión de cinco minutos:

```bash
shellcheck mi-script.sh
```

Salida de ejemplo cuando hay un problema:

```text
In mi-script.sh line 3:
rm -rf $carpeta
       ^------^ SC2086: Double quote to prevent globbing and word splitting.
```

Cópialo a tu rutina: escribe el script, pasa `shellcheck`, corrige avisos.

## Ejemplos prácticos

### Script 1 · Copia de seguridad con `tar`

Hace un backup comprimido y con fecha de la carpeta que le indiques.

```bash
#!/usr/bin/env bash
# backup.sh · Crea un backup .tar.gz con fecha.
# Uso: ./backup.sh [origen] [destino]
set -euo pipefail

ORIGEN="${1:-$HOME/Documentos}"
DESTINO="${2:-$HOME/backups}"
FECHA="$(date +%Y-%m-%d_%H%M%S)"
ARCHIVO="$DESTINO/backup_$FECHA.tar.gz"

if [[ ! -d "$ORIGEN" ]]; then
  echo "Error: el origen '$ORIGEN' no existe o no es un directorio." >&2
  exit 1
fi

mkdir -p "$DESTINO"

tar -czf "$ARCHIVO" -C "$ORIGEN" .
echo "Backup creado: $ARCHIVO ($(du -h "$ARCHIVO" | cut -f1))"
```

**Línea a línea:**

- `ORIGEN="${1:-$HOME/Documentos}"` → usa el primer argumento; si no hay, la carpeta por defecto
  `${1:-valor}`.
- `FECHA="$(date +...)"` → `$(...)` ejecuta un comando y guarda su salida.
- `>&2` → manda el mensaje de error a **stderr**.
- `tar -czf archivo -C origen .` → empaqueta (`-c`), comprime con gzip (`-z`), escribe en un fichero
  (`-f`), cambia a `origen` (`-C`) y mete su contenido (`.`).

### Script 2 · Barrido de red (ping sweep)

Descubre qué equipos están activos en tu red local. **Solo en tu laboratorio.**

```bash
#!/usr/bin/env bash
# ping-sweep.sh · Busca hosts activos en una red /24.
# Uso: ./ping-sweep.sh [prefijo]   p. ej.: ./ping-sweep.sh 192.168.56
set -uo pipefail

RED="${1:-192.168.56}"
activos=0

echo "Barriendo $RED.1 - $RED.254 ..."
for i in $(seq 1 254); do
  ip="$RED.$i"
  if ping -c 1 -W 1 "$ip" &>/dev/null; then
    echo "[+] Activo: $ip"
    ((activos++))
  fi
done

echo "Total de hosts activos: $activos"
```

**Notas:**

- `seq 1 254` genera los números del 1 al 254.
- `ping -c 1` manda **un** paquete; `-W 1` espera como máximo 1 segundo.
- `&>/dev/null` silencia toda la salida del `ping`; solo importa el código de salida.
- Aquí **no** usamos `set -e` a propósito: que un ping falle es normal, no un error del script.

!!! tip "Hazlo más rápido"
    Un barrido secuencial tarda ~4 minutos (254 × ~1 s). Para acelerarlo, lanza los pings en
    paralelo o usa `nmap -sn` (ver el [Nivel 2](../../nivel-2-medio/05-nmap-en-profundidad.md)), que
    está pensado exactamente para esto.

### Script 3 · Mini escáner de puertos con `/dev/tcp`

Comprueba si hay puertos abiertos usando una función **nativa de bash**: `/dev/tcp`.

```bash
#!/usr/bin/env bash
# port-scan.sh · Comprueba puertos TCP abiertos con /dev/tcp.
# Uso: ./port-scan.sh <host> [puerto ...]
set -uo pipefail

HOST="${1:-127.0.0.1}"
shift || true

if [[ $# -gt 0 ]]; then
  PUERTOS=("$@")
else
  PUERTOS=(22 80 443 3306 8080)
fi

echo "Escaneando $HOST ..."
for p in "${PUERTOS[@]}"; do
  if timeout 2 bash -c "echo > /dev/tcp/$HOST/$p" 2>/dev/null; then
    echo "[+] Puerto $p ABIERTO"
  else
    echo "[-] Puerto $p cerrado o filtrado"
  fi
done
```

**Línea a línea:**

- `shift` descarta el primer argumento (`$1`, el host); ahora `$@` son solo los puertos.
- `timeout 2 bash -c "echo > /dev/tcp/$HOST/$p"` → intenta abrir una conexión TCP; si funciona en
  menos de 2 segundos, el puerto está abierto.
- `/dev/tcp/host/puerto` es una **característica de bash** (no existe en otros shells): escribir en
  esa ruta abre una conexión TCP.

!!! warning "Recuerda la ética"
    Este script es **didáctico**. Escanear puertos de equipos que no controlas puede constituir
    delito. Practica contra `127.0.0.1`, tus VMs, [tryhackme.com](https://tryhackme.com) o
    [www.hackthebox.com](https://www.hackthebox.com). Para escaneos serios, usa `nmap`.

!!! note "¿Por qué `/dev/tcp` y no `nc`?"
    `/dev/tcp` funciona en cualquier bash **sin instalar nada**, lo que es perfecto para aprender cómo
    funciona una conexión. Herramientas como `nmap` o `netcat` son mucho más completas para trabajo
    real.

### Script 4 · Análisis de logs

Saca las IPs y los códigos HTTP más frecuentes de un log de servidor web (formato *combined*
típico de Apache/Nginx).

```bash
#!/usr/bin/env bash
# analiza-log.sh · Top IPs y códigos de estado de un access log.
# Uso: ./analiza-log.sh [fichero.log] [topN]
set -euo pipefail

LOG="${1:-/var/log/nginx/access.log}"
TOPN="${2:-10}"

if [[ ! -f "$LOG" ]]; then
  echo "Error: no existe el fichero de log '$LOG'." >&2
  exit 1
fi

echo "=== Top $TOPN IPs por número de peticiones ==="
awk '{ print $1 }' "$LOG" | sort | uniq -c | sort -rn | head -n "$TOPN"

echo
echo "=== Códigos de estado HTTP ==="
awk '{ print $9 }' "$LOG" | sort | uniq -c | sort -rn

echo
echo "=== Peticiones con error (4xx / 5xx) ==="
awk '$9 ~ /^[45][0-9][0-9]$/ { print $1, $7, $9 }' "$LOG" | head -n "$TOPN"
```

**Línea a línea:**

- `$LOG` por defecto apunta al log de Nginx; le pasas otro como argumento si quieres.
- `awk '{ print $1 }'` extrae la IP del cliente.
- `sort | uniq -c | sort -rn` cuenta y ordena de mayor a menor (ya lo conoces).
- `awk '$9 ~ /^[45][0-9][0-9]$/ ...'` imprime las peticiones cuyo noveno campo empieza por 4 o 5
  (errores de cliente y de servidor).

!!! tip "Prueba sin log real"
    Si no tienes un access log, crea uno de prueba en formato *combined*:
    ```bash
    cat > access.log <<'EOF'
    10.0.0.5 - - [18/Oct/2026:12:00:01 +0200] "GET /index.html HTTP/1.1" 200 1043
    10.0.0.7 - - [18/Oct/2026:12:00:02 +0200] "GET /login HTTP/1.1" 401 512
    10.0.0.5 - - [18/Oct/2026:12:00:03 +0200] "POST /login HTTP/1.1" 200 900
    10.0.0.9 - - [18/Oct/2026:12:00:04 +0200] "GET /admin HTTP/1.1" 403 233
    EOF
    ```
    El script extrae la IP del campo 1 y el código de estado del campo 9, como en los logs reales de
    Apache/Nginx en formato *combined*.

### Script 5 · Renombrado masivo

Renombra en bloque: sustituye espacios por guiones bajos y puede añadir un prefijo.

```bash
#!/usr/bin/env bash
# renombra.sh · Reemplaza espacios por "_" y añade un prefijo opcional.
# Uso: ./renombra.sh <directorio> [prefijo]
set -euo pipefail

DIR="${1:-.}"
PREFIJO="${2:-}"
shopt -s nullglob

if [[ ! -d "$DIR" ]]; then
  echo "Error: '$DIR' no es un directorio." >&2
  exit 1
fi

for ruta in "$DIR"/*; do
  [[ -f "$ruta" ]] || continue
  base="$(basename -- "$ruta")"
  limpio="${base// /_}"                 # sustituye espacios por _
  destino="$(dirname -- "$ruta")/${PREFIJO}${limpio}"

  if [[ "$ruta" != "$destino" ]]; then
    mv -n -- "$ruta" "$destino"
    echo "Renombrado: '$base' -> '${PREFIJO}${limpio}'"
  fi
done
```

**Línea a línea:**

- `shopt -s nullglob` → si el directorio está vacío, el bucle no se ejecuta (en vez de tratar el
  literal `*` como un fichero).
- `${base// /_}` → sustitución de cadenas: reemplaza **todas** las apariciones de espacio por `_`.
- `[[ -f "$ruta" ]] || continue` → salta todo lo que no sea un fichero normal (subdirectorios, etc.).
- `mv -n` → *no clobber*: no sobrescribe si el destino ya existe. Con `--` evitas que un nombre que
  empieza por `-` se interprete como opción.

!!! danger "Prueba siempre en una copia antes"
    Los renombrados masivos son irreversibles. Hazlo primero sobre una carpeta de prueba, revisa el
    resultado y solo entonces aplícalo a tus datos reales.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| `Permission denied` al ejecutar | Falta permiso de ejecución. | `chmod +x script.sh`. |
| `command not found` del script | No pusiste `./` o la ruta. | Ejecuta `./script.sh` (la carpeta actual no suele estar en el `PATH`). |
| `nombre = "Ana"` falla | Espacios alrededor del `=`. | `nombre="Ana"` sin espacios. |
| El `if` nunca entra | Comillas mal puestas o comando que devuelve otro código. | Usa `[[ ]]` y revisa con `echo $?`. |
| `unbound variable` | `set -u` y usaste una variable vacía. | Asigna un valor por defecto: `"${var:-por_defecto}"`. |
| El script borra más de la cuenta | Variables sin comillas. | Pon **siempre** comillas: `"$var"`. |
| `cron` no ejecuta el script | `PATH` reducido o rutas relativas. | Rutas absolutas y redirige salida a un log. |
| Errores silenciosos | No usas `set -e`. | Empieza con `set -euo pipefail`. |

## Ejercicios

1. Escribe un script `hola.sh` que salude usando una variable con tu nombre y se ejecute con
   `./hola.sh`.
2. Escribe un script que reciba un directorio como argumento y diga si existe y cuántos ficheros
   contiene.
3. Escribe un script con un bucle `for` que imprima los números del 1 al 10 y marque los pares.
4. Convierte el código del barrido de red en una función `host_activo()` que devuelva 0 o 1, y úsala
   en el bucle.
5. Añade a `backup.sh` un mensaje de error a `stderr` y un `exit 1` si **no** se puede escribir en el
   destino; comprueba el código de salida con `echo $?`.
6. *(Difícil)* Escribe un script que recorra todos los `.log` de una carpeta, cuente cuántas líneas
   con la palabra `ERROR` tiene cada uno, y guarde un resumen ordenado en `resumen.txt`.

??? success "Solución"

    **1. `hola.sh`:**
    ```bash
    #!/usr/bin/env bash
    set -euo pipefail
    nombre="Ana"
    echo "Hola, $nombre"
    ```
    ```bash
    chmod +x hola.sh && ./hola.sh
    ```

    **2. Comprobar directorio y contar ficheros:**
    ```bash
    #!/usr/bin/env bash
    set -euo pipefail
    dir="${1:-.}"
    if [[ ! -d "$dir" ]]; then
      echo "'$dir' no es un directorio." >&2
      exit 1
    fi
    n=$(find "$dir" -maxdepth 1 -type f | wc -l)
    echo "'$dir' existe y contiene $n ficheros."
    ```

    **3. Números del 1 al 10 marcando pares:**
    ```bash
    #!/usr/bin/env bash
    set -euo pipefail
    for ((i = 1; i <= 10; i++)); do
      if (( i % 2 == 0 )); then
        echo "$i (par)"
      else
        echo "$i"
      fi
    done
    ```

    **4. Función `host_activo`:**
    ```bash
    #!/usr/bin/env bash
    set -uo pipefail
    host_activo() {
      ping -c 1 -W 1 "$1" &>/dev/null
    }
    red="192.168.56"
    for i in $(seq 1 254); do
      if host_activo "$red.$i"; then
        echo "[+] Activo: $red.$i"
      fi
    done
    ```
    La función devuelve el código de salida de `ping`, que `if` interpreta directamente.

    **5. Comprobar permiso de escritura en el destino:**
    ```bash
    if [[ ! -w "$DESTINO" && ! -w "$(dirname "$DESTINO")" ]]; then
      echo "Error: no se puede escribir en '$DESTINO'." >&2
      exit 1
    fi
    ```
    Tras ejecutarlo, `echo $?` devuelve `1` si falló.

    **6. Resumen de errores por log:**
    ```bash
    #!/usr/bin/env bash
    set -euo pipefail
    carpeta="${1:-.}"
    shopt -s nullglob
    : > resumen.txt
    for log in "$carpeta"/*.log; do
      n=$(grep -c "ERROR" "$log" || true)
      printf '%6d  %s\n' "$n" "$(basename "$log")" >> resumen.txt
    done
    sort -rn resumen.txt -o resumen.txt
    cat resumen.txt
    ```
    `grep -c` devuelve código 1 cuando no encuentra nada; con `|| true` evitamos que `set -e`
    aborte el script.

## Resumen

- Shebang `#!/usr/bin/env bash`, `chmod +x` y ejecuta con `./script.sh`.
- Variables sin espacios (`var="valor"`); se usan con `$var` o `${var}`.
- `PATH` es dónde el shell busca los comandos; `export` hereda variables.
- Comillas **simples** = literal; **dobles** = interpretan variables.
- `$?` es el código de salida (0 = éxito). `$1`, `$@`, `$#` son los argumentos.
- `if [[ ]]`, `for`, `while [[ ]]` y funciones (`local`) son el esqueleto del lenguaje.
- `set -euo pipefail` + **comillas siempre** + `shellcheck` = scripts fiables.
- `cron` automatiza tareas (`crontab -e`), pero con rutas absolutas y salida a un log.

## Checklist

- [ ] Sé crear, dar permisos y ejecutar un script.
- [ ] Uso variables y entiendo el `PATH`.
- [ ] Distingo comillas simples de dobles.
- [ ] Escribo condicionales con `[[ ]]` y bucles `for`/`while`.
- [ ] Defino funciones y leo argumentos (`$1`, `"$@"`, `$#`).
- [ ] Compruebo códigos de salida con `$?`.
- [ ] Empiezo mis scripts con `set -euo pipefail` y los paso por `shellcheck`.
- [ ] Sé programar una tarea con `cron`.
- [ ] He probado al menos tres de los cinco scripts en mi laboratorio.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [GNU Bash Manual](https://www.gnu.org/software/bash/manual/) | Referencia oficial del lenguaje | EN | Gratis |
| [ShellCheck](https://www.shellcheck.net) | Analizador de scripts (web y local) | EN | Gratis |
| [Linux man pages](https://man7.org) | `man bash`, `man cron`, `man crontab` | EN | Gratis |
| [Google Shell Style Guide](https://google.github.io/styleguide/shellguide.html) | Guía de estilo para scripts bash | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta una recopilación de **scripts de ejemplo comentados** en español apta para principiantes,
    con enlace verificado. Debe añadirla un redactor.

## Siguiente paso

Para no memorizarlo todo, ten a mano la referencia rápida:
**[05 · Chuleta de Bash](05-chuleta-bash.md)**.
