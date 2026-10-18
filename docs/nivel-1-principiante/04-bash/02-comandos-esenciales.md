# 02 · Comandos esenciales

**Estos veinte comandos son el 90 % de tu trabajo diario en la terminal.** No hay que memorizarlos
todos de golpe: se aprenden usándolos. En esta página repasamos navegación, gestión de ficheros,
búsqueda, inspección de texto y filtrado, **cada uno con ejemplos reales** que puedes copiar y
probar. Al terminarla tendrás soltura para moverte por cualquier sistema Linux.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Navegar por el sistema de ficheros con `pwd`, `cd`, `ls`.
- Crear, copiar, mover y borrar con `mkdir`, `cp`, `mv`, `rm`, **entendiendo el peligro de `rm -rf`**.
- Leer ficheros con `cat`, `less`, `head`, `tail`.
- Buscar ficheros por nombre con `find` y `locate`.
- Buscar dentro de ficheros con `grep`, y transformar texto con `sed`, `awk`, `cut`, `sort`, `uniq`.
- Contar y combinar comandos con `wc`, `tee`, `xargs`.

**Tiempo estimado: 90-120 min.**

## Requisitos previos

- Haber leído [Terminal, shell y consola](01-terminal-shell-y-consola.md).
- Una terminal abierta en Linux. Si no tienes, mira
  [Montar Kali y Parrot](../03-sistemas-operativos/06-montar-kali-y-parrot.md).

## Explicación

Antes de ver comandos, una idea clave: en Linux **todo cuelga de un único árbol de directorios** que
empieza en la raíz `/`. Tu carpeta personal es `/home/tu-usuario` y se abrevia `~`.

```text
/                          ← raíz del sistema
├── home/
│   └── usuario/           ← tu carpeta personal (~)
│       ├── Documentos/
│       └── Descargas/
├── etc/                   ← configuración
├── var/
│   └── log/               ← registros (logs)
├── usr/
│   └── bin/               ← programas instalados
└── tmp/                   ← ficheros temporales
```

Vamos a agrupar los comandos por para qué sirven.

### Navegación: dónde estoy y cómo me muevo

| Comando | Para qué sirve |
| --- | --- |
| `pwd` | Muestra el **directorio actual** (*print working directory*). |
| `cd` | Cambia de directorio (*change directory*). |
| `ls` | Lista el contenido de un directorio (*list*). |

Rutas clave:

| Símbolo | Significa |
| --- | --- |
| `/` | Raíz del sistema. |
| `~` | Tu carpeta personal (`/home/usuario`). |
| `.` | El directorio actual. |
| `..` | El directorio padre (subir un nivel). |
| `-` | El directorio anterior (con `cd -`). |

### Gestión de ficheros y directorios

| Comando | Para qué sirve |
| --- | --- |
| `mkdir` | Crea un directorio (*make directory*). |
| `cp` | Copia ficheros o directorios (*copy*). |
| `mv` | Mueve o renombra (*move*). |
| `rm` | Borra (*remove*). **Es irreversible: no hay papelera.** |

### Ver y leer ficheros

| Comando | Para qué sirve |
| --- | --- |
| `cat` | Muestra el fichero entero (*concatenate*). |
| `less` | Lo muestra por páginas, navegable. |
| `head` | Muestra las primeras líneas. |
| `tail` | Muestra las últimas líneas. |

### Buscar

| Comando | Para qué sirve |
| --- | --- |
| `find` | Busca ficheros **recorriendo** el disco (siempre actualizado). |
| `locate` | Busca ficheros en una **base de datos** (rapidísimo, pero puede estar desactualizada). |
| `grep` | Busca **texto dentro** de ficheros. |

### Transformar y filtrar texto

| Comando | Para qué sirve |
| --- | --- |
| `sed` | Edita texto por líneas (sustituir, borrar…). |
| `awk` | Procesa texto **por columnas/campos**. |
| `cut` | Extrae columnas o caracteres. |
| `sort` | Ordena líneas. |
| `uniq` | Elimina líneas repetidas **consecutivas**. |
| `wc` | Cuenta líneas, palabras y bytes (*word count*). |

### Combinar

| Comando | Para qué sirve |
| --- | --- |
| `tee` | Escribe la salida en pantalla **y** en un fichero a la vez. |
| `xargs` | Convierte la salida de un comando en argumentos de otro. |

## Ejemplos prácticos

!!! info "Antes de empezar"
    Todos los ejemplos usan una carpeta de prácticas. Créala así y no tocarás nada importante:
    ```bash
    mkdir -p ~/lab-bash && cd ~/lab-bash
    ```

### `pwd`, `ls` y `cd` — navegar

```bash
pwd
ls
ls -l
ls -lah
cd /tmp
cd -
cd ~
```

```text
/home/usuario/lab-bash              (salida de ejemplo)
                                    (vacío: la carpeta está recién creada)
total 0                             (salida de ejemplo)
drwxr-xr-x 2 usuario usuario 4096 oct 18 12:00 .   (salida de ejemplo)
```

- `ls` lista nombres. `ls -l` da el formato largo (permisos, dueño, tamaño, fecha). `ls -lah` añade
  `-a` (incluye ocultos, los que empiezan por `.`) y `-h` (tamaños "humanos": KB, MB).
- `cd -` vuelve al directorio anterior; muy útil para ir y volver.

### `mkdir` — crear directorios

```bash
mkdir proyectos
mkdir -p proyectos/web/css
ls -R proyectos
```

```text
proyectos:
web

proyectos/web:
css
```

`-p` crea **toda la ruta** de una vez (padres incluidos) y no falla si ya existe.

### `cp`, `mv` y `rm` — copiar, mover, borrar

Primero creamos un fichero de prueba:

```bash
echo "hola" > nota.txt
cp nota.txt nota-copia.txt
cp -r proyectos proyectos-backup
mv nota-copia.txt copia.txt
mv copia.txt proyectos/
rm nota.txt
ls -R
```

```text
.:
nota.txt  proyectos  proyectos-backup

nota.txt  proyectos  proyectos-backup
```

(Después de los comandos, `nota.txt` ya no existe.)

- `cp -r` copia **recursivamente** directorios enteros (`-r` = recursivo).
- `mv` sirve tanto para **mover** como para **renombrar**.
- `rm` borra. `rm -r` borra un directorio y su contenido. `rm -f` fuerza sin preguntar.

!!! danger "Cuidado con `rm -rf`"
    `rm -rf` significa **borrar recursivamente y sin confirmación**. Un espacio mal puesto cambia
    todo:

    ```bash
    rm -rf ~/lab-bash      # borra TU carpeta de prácticas (esperado)
    rm -rf ~ /lab-bash     # ¡ESPACIO DE MÁS! intenta borrar toda tu carpeta personal
    rm -rf /               # ¡destruye el sistema entero!
    ```

    Reglas de oro:

    1. **Nunca** ejecutes `rm -rf` sobre `/` ni sobre `~` sin un motivo muy claro.
    2. **Revisa el comando antes de pulsar Enter.** Mejor `ls` primero para ver qué vas a borrar.
    3. Usa `rm -ri carpeta/` para que te pregunte **fichero a fichero** mientras aprendes.
    4. En un sistema de producción, `rm -rf` es la receta del desastre: hay que pensarlo dos veces.

### `cat`, `less`, `head`, `tail` — leer ficheros

```bash
printf 'linea1\nlinea2\nlinea3\nlinea4\nlinea5\n' > diario.txt
cat diario.txt
head -n 2 diario.txt
tail -n 2 diario.txt
less diario.txt
```

```text
linea1
linea2
linea3
linea4
linea5
```

- `cat` imprime todo el fichero de golpe (útil si es corto).
- `head -n 2` muestra las **2 primeras** líneas; `tail -n 2` las **2 últimas**.
- `less` abre un visor navegable: `++space++`/`++b++` para avanzar/retroceder, `/texto` para buscar,
  `++q++` para salir.

!!! tip "`tail -f`: vigilar logs en vivo"
    `tail -f /var/log/syslog` muestra el final del fichero y **sigue** escribiendo las líneas
    nuevas a medida que llegan. Es la forma estándar de observar un log en tiempo real.

### `find` — buscar ficheros por nombre, tamaño, fecha

```bash
find . -name "*.txt"
find /home -type d -name "Descargas"
find . -type f -size +1M
find . -name "*.log" -mtime -7
```

```text
./diario.txt
./proyectos/copia.txt
```

- `-name "*.txt"` filtra por nombre (el `*` es un comodín).
- `-type f` solo ficheros; `-type d` solo directorios.
- `-size +1M` ficheros mayores de 1 MB.
- `-mtime -7` modificados en los **últimos 7 días**.

!!! warning "El comodín y las comillas"
    Escribe `-name "*.txt"` **con comillas**. Si lo escribes sin comillas, el shell intenta expandir
    el `*` antes de que `find` lo reciba y el resultado puede ser incorrecto.

### `locate` — buscar al instante

```bash
locate diario.txt
locate -i bashrc
```

`locate` consulta una base de datos de rutas y es casi instantáneo. La base de datos se actualiza
periódicamente (normalmente con `updatedb`, que requiere permisos). Por eso puede **no encontrar algo
recién creado**. `-i` ignora mayúsculas/minúsculas.

| | `find` | `locate` |
| --- | --- | --- |
| Velocidad | Lenta (recorre el disco) | Muy rápida (consulta índice) |
| Datos frescos | Siempre | Puede no estar actualizado |
| Búsqueda por tamaño/fecha | Sí | No |

### `grep` — buscar texto dentro de ficheros

```bash
printf 'root:x:0:0:root:/root:/bin/bash\nuser:x:1000:1000::/home/user:/bin/bash\n' > passwdfake.txt
grep "root" passwdfake.txt
grep -i "USER" passwdfake.txt
grep -c "bash" passwdfake.txt
grep -rn "error" /var/log 2>/dev/null | head
```

```text
root:x:0:0:root:/root:/bin/bash
user:x:1000:1000::/home/user:/bin/bash
2
```

- `grep patron fichero` busca el patrón en el fichero.
- `-i` ignora mayúsculas; `-c` cuenta coincidencias; `-r` busca **recursivamente** en directorios;
  `-n` añade el número de línea; `-v` invierte (muestra lo que **no** coincide).
- `2>/dev/null` descarta los mensajes de error (lo veremos en la página siguiente).

### `sed` — sustituir y editar texto

```bash
sed 's/linea/LINEA/' diario.txt
sed -n '2,3p' diario.txt
sed -i 's/LINEA/linea/' diario.txt
```

```text
LINEA1
LINEA2
linea3
linea4
linea5
```

- `s/antiguo/nuevo/` sustituye **la primera** coincidencia de cada línea. Con `g` al final
  (`s/a/b/g`) sustituye **todas**.
- `-n '2,3p'` imprime solo las líneas 2 y 3.
- `-i` edita **el fichero en su sitio** (¡haz copia antes de probar!). Para probar sin riesgo, deja
  fuera `-i`: solo imprime el resultado.

### `awk` — procesar por columnas

```bash
printf 'ana 25 madrid\nluis 31 sevilla\nmarta 22 bilbao\n' > personas.txt
awk '{ print $1 }' personas.txt
awk '{ print $2, $1 }' personas.txt
awk '$2 > 30 { print $1 }' personas.txt
```

```text
ana
luis
marta
25 ana
31 luis
22 marta
luis
```

- `awk` divide cada línea en campos: `$1`, `$2`, `$3`…, y `$0` es la línea completa.
- `$2 > 30 { print $1 }` imprime el nombre de quienes tienen la segunda columna mayor que 30.
- Por defecto el separador es cualquier espacio en blanco; se cambia con `-F` (por ejemplo
  `awk -F: '{print $1}' /etc/passwd` para separar por `:`).

### `cut` — extraer columnas o caracteres

```bash
cut -d' ' -f1 personas.txt
cut -c1-3 personas.txt
```

```text
ana
luis
marta
ana
lui
mar
```

- `-d' '` define el delimitador (un espacio) y `-f1` pide el campo 1.
- `-c1-3` extrae los **caracteres** 1 a 3 de cada línea.

### `sort`, `uniq` y `wc` — ordenar, deduplicar, contar

```bash
printf 'pera\nmanzana\npera\nplatano\nmanzana\npera\n' > frutas.txt
sort frutas.txt
sort frutas.txt | uniq
sort frutas.txt | uniq -c
sort frutas.txt | uniq -c | sort -rn
wc -l frutas.txt
```

```text
manzana
manzana
pera
pera
pera
platano
manzana
pera
platano
      3 pera
      2 manzana
      1 platano
6 frutas.txt
```

- `sort` ordena alfabéticamente. `sort -n` ordena numéricamente; `sort -rn` ordena numérico y
  **descendente** (el `-r` = reverse).
- `uniq` **solo** elimina repetidos **consecutivos**, por eso hay que ordenar antes con `sort`.
- `uniq -c` cuenta cuántas veces aparece cada línea.
- `wc -l` cuenta líneas. También `wc -w` (palabras) y `wc -c` (bytes).

!!! tip "El patrón `sort | uniq -c | sort -rn`"
    Memorízalo: es la forma clásica de obtener un **ranking** de elementos repetidos en un fichero
    (IPs en un log, usuarios, etc.). Lo usarás constantemente en análisis de logs.

### `tee` — ver y guardar a la vez

```bash
echo "ip 10.0.0.5" | tee salida.txt
cat salida.txt
```

```text
ip 10.0.0.5
ip 10.0.0.5
```

`tee` imprime en pantalla **y** escribe en el fichero indicado. Con `tee -a` añade en lugar de
sobreescribir. Se llama "tee" por la forma de la pieza en T de fontanería: divide el flujo en dos.

### `xargs` — convertir salida en argumentos

```bash
printf 'a.txt\nb.txt\n' | xargs touch
ls
find . -name "*.txt" | xargs wc -l
```

```text
a.txt  b.txt  diario.txt  ...   (salida de ejemplo)
```

- `xargs` coge la salida del comando anterior (una lista de líneas) y la pasa como **argumentos** al
  comando siguiente. Aquí, `touch` crea `a.txt` y `b.txt`.
- Con espacios en los nombres hay que usar `xargs -0` junto a `find ... -print0` (evita problemas con
  nombres que contienen espacios).

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| `rm: cannot remove 'x': Is a directory` | Intentaste borrar un directorio sin `-r`. | Usa `rm -r x` (con cuidado) o `rm -ri x` para que pregunte. |
| `No such file or directory` | Ruta mal escrita o no existe. | Comprueba con `ls` antes; usa `++tab++` para autocompletar. |
| `find` no encuentra nada | Comillas mal puestas o directorio equivocado. | Escribe `find . -name "*.txt"` **con comillas**. |
| `uniq` no elimina repetidos | No ordenaste antes. | Ordena primero: `sort fichero`, luego pasa el resultado a `uniq -c`. |
| `sed -i` rompió el fichero | `-i` edita sin copia. | Prueba sin `-i`; si lo usas, haz copia antes. |
| `Permission denied` | No tienes permisos sobre ese fichero. | Revisa permisos (`ls -l`) o usa `sudo` **si** procede. |
| Comando no encontrado | `PATH` o el programa no está instalado. | Lo veremos en [Scripts en Bash](04-scripts-bash.md). |

## Ejercicios

1. Crea dentro de `~/lab-bash` una estructura `practicas/recursos/notas` en un solo comando.
2. Crea un fichero `lista.txt` con 5 nombres de fruta (uno por línea) usando `printf` o `echo`.
3. Cuenta cuántas líneas tiene `lista.txt` y muestra solo las 2 últimas.
4. Busca en `/etc` todos los ficheros que contengan la palabra `root` y muestra la salida paginada.
5. Usando el fichero `personas.txt`, muestra solo los nombres ordenados alfabéticamente y sin
   repetidos.
6. *(Difícil)* Encuentra en todo tu sistema (o en `/home`) los ficheros `.txt` modificados en los
   últimos 7 días que midan más de 10 KB, y pásalos a `wc -l` con `xargs`.

??? success "Solución"

    **1. Estructura de directorios:**
    ```bash
    mkdir -p ~/lab-bash/practicas/recursos/notas
    ```

    **2. Crear `lista.txt`:**
    ```bash
    printf 'pera\nmanzana\nplatano\nkiwi\nnaranja\n' > lista.txt
    ```

    **3. Contar y ver las dos últimas:**
    ```bash
    wc -l lista.txt
    tail -n 2 lista.txt
    ```

    **4. Buscar `root` en `/etc` paginado:**
    ```bash
    grep -rn "root" /etc 2>/dev/null | less
    ```
    El `2>/dev/null` evita los errores de permisos.

    **5. Nombres ordenados y sin repetidos:**
    ```bash
    cut -d' ' -f1 personas.txt | sort | uniq
    ```

    **6. Ficheros grandes y recientes:**
    ```bash
    find ~ -type f -name "*.txt" -size +10k -mtime -7 -print0 | xargs -0 wc -l
    ```
    `-print0` y `xargs -0` manejan correctamente los nombres con espacios.

## Resumen

- Navegar: `pwd`, `cd`, `ls` (con `-l`, `-a`, `-h`).
- Gestionar: `mkdir -p`, `cp -r`, `mv`, `rm` (¡ojo con `rm -rf`!).
- Leer: `cat`, `less`, `head -n`, `tail -n`, `tail -f`.
- Buscar: `find` (por nombre/tipo/tamaño/fecha), `locate` (rápido, índice), `grep` (`-i`, `-r`,
  `-c`, `-n`, `-v`).
- Transformar: `sed`, `awk`, `cut`, `sort`, `uniq`, `wc`.
- Combinar: `tee` (ver y guardar), `xargs` (salida → argumentos).
- El patrón estrella: `sort | uniq -c | sort -rn`.

## Checklist

- [ ] Me muevo por el sistema sin perderme (`pwd`, `cd`, `ls`).
- [ ] Creo, copio, muevo y borro ficheros y carpetas con seguridad.
- [ ] Sé por qué `rm -rf` es peligroso y cómo evitarlo.
- [ ] Leo ficheros grandes con `less` y sigo logs con `tail -f`.
- [ ] Busco ficheros con `find` y `locate`, y texto con `grep`.
- [ ] Extraigo columnas con `cut`/`awk` y ordeno/cuento con `sort`/`uniq`/`wc`.
- [ ] Reconozco el patrón `sort | uniq -c | sort -rn`.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Linux man pages](https://man7.org) | Manuales oficiales de cada comando | EN | Gratis |
| [The Linux Command Line](https://linuxcommand.org) | Libro gratuito (PDF) sobre la línea de comandos | EN | Gratis |
| [GNU Coreutils](https://www.gnu.org/software/coreutils/) | Documentación de `ls`, `cp`, `sort`, `wc`… | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta un recurso en **español** para practicar los comandos básicos de Linux de forma
    interactiva (tipo juego o laboratorio guiado). Debe verificarlo un redactor.

## Siguiente paso

Ahora que manejas comandos sueltos, unámoslos para que se pasen información entre ellos:
**[03 · Tuberías, redirecciones y filtros](03-tuberias-redirecciones-y-filtros.md)**.
