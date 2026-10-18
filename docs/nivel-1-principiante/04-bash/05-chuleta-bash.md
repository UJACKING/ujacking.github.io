# 05 · Chuleta de Bash

**Referencia rápida para tener a mano.** Esta página es una *chuleta*: no se lee de principio a fin,
se consulta. Reúne los comandos, redirecciones, atajos de teclado y *one-liners* que más vas a usar.
Puedes copiarla a tu propio Markdown y guardarla o imprimirla.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Localizar de un vistazo el comando que necesitas.
- Recordar la sintaxis correcta de las redirecciones y tuberías.
- Conocer los atajos de teclado que aceleran el trabajo en la terminal.
- Tener ejemplos de una línea listos para copiar.

**Tiempo estimado: 15 min (consulta).**

## Requisitos previos

- Haber trabajado [Comandos esenciales](02-comandos-esenciales.md),
  [Tuberías, redirecciones y filtros](03-tuberias-redirecciones-y-filtros.md) y
  [Scripts en Bash](04-scripts-bash.md). Esta página es el resumen de todas ellas.

## Explicación

### Navegación

| Comando | Qué hace |
| --- | --- |
| `pwd` | Muestra el directorio actual. |
| `cd /ruta` | Cambia al directorio `/ruta`. |
| `cd ..` | Sube un nivel. |
| `cd ~` | Va a tu carpeta personal. |
| `cd -` | Vuelve al directorio anterior. |
| `ls` | Lista el contenido. |
| `ls -lah` | Formato largo, todo (incluidos ocultos), tamaños legibles. |
| `tree` | Muestra el árbol de directorios. |

### Ficheros y directorios

| Comando | Qué hace |
| --- | --- |
| `mkdir -p a/b/c` | Crea toda la ruta de directorios. |
| `touch f.txt` | Crea un fichero vacío (o actualiza su fecha). |
| `cp origen destino` | Copia un fichero. |
| `cp -r dir1 dir2` | Copia un directorio entero. |
| `mv origen destino` | Mueve o renombra. |
| `rm f.txt` | Borra un fichero. |
| `rm -r dir` | Borra un directorio y su contenido. |
| `ln -s real enlace` | Crea un enlace simbólico. |

!!! danger "`rm -rf` borra sin confirmar y sin papelera"
    Revisa el comando **dos veces** antes de pulsar `++enter++`. Un espacio de más lo cambia todo.

### Ver y leer ficheros

| Comando | Qué hace |
| --- | --- |
| `cat f.txt` | Muestra el fichero completo. |
| `cat -n f.txt` | Lo muestra con números de línea. |
| `less f.txt` | Visor navegable (`++q++` para salir). |
| `head -n 20 f.txt` | Las 20 primeras líneas. |
| `tail -n 20 f.txt` | Las 20 últimas líneas. |
| `tail -f log.txt` | Sigue las líneas nuevas en vivo. |
| `wc -l f.txt` | Cuenta líneas. |
| `file f` | Muestra el tipo de fichero. |

### Buscar

| Comando | Qué hace |
| --- | --- |
| `find . -name "*.txt"` | Busca por nombre desde el directorio actual. |
| `find / -type f -size +10M` | Ficheros mayores de 10 MB. |
| `find . -mtime -7` | Modificados en los últimos 7 días. |
| `locate fichero` | Búsqueda instantánea por índice. |
| `grep patron f.txt` | Busca texto en un fichero. |
| `grep -rin patron dir/` | Recursivo, ignora mayúsculas, con número de línea. |
| `which comando` | Ruta del ejecutable. |
| `type comando` | Qué es (alias, función, ejecutable…). |

### Texto: transformar y filtrar

| Comando | Qué hace |
| --- | --- |
| `cut -d: -f1 f` | Extrae el campo 1 usando `:` como separador. |
| `cut -c1-5 f` | Extrae los caracteres 1 a 5. |
| `sort f` | Ordena alfabéticamente. |
| `sort -n f` | Ordena numéricamente. |
| `sort -rn f` | Ordena numérico descendente. |
| `uniq -c f` | Cuenta repeticiones consecutivas. |
| `sed 's/a/b/g' f` | Sustituye `a` por `b` en todo el fichero. |
| `awk '{print $1}' f` | Imprime la primera columna. |
| `awk -F: '{print $1}' f` | Igual, separando por `:`. |
| `tr 'a-z' 'A-Z' f` | Traduce caracteres (aquí, a mayúsculas). |
| `tee out.txt` | Escribe en pantalla y en fichero a la vez. |
| `xargs cmd` | Convierte la entrada en argumentos de `cmd`. |

### Redirecciones y tuberías

| Sintaxis | Qué hace |
| --- | --- |
| `cmd > f` | Salida a `f` (sobrescribe). |
| `cmd >> f` | Salida a `f` (añade). |
| `cmd 2> f` | Errores a `f`. |
| `cmd &> f` | Salida y errores a `f`. |
| `cmd < f` | Entrada desde `f`. |
| `cmd 2>/dev/null` | Descarta los errores. |
| `cmd >/dev/null 2>&1` | Descarta todo (forma clásica). |
| `cmd &` | Ejecuta en segundo plano. |

Tuberías y encadenado lógico (los propios símbolos, en un bloque de código):

```bash
cmd1 | cmd2      # tubería: salida de cmd1 -> entrada de cmd2
cmd1 && cmd2     # cmd2 solo si cmd1 tiene éxito
cmd1 || cmd2     # cmd2 solo si cmd1 falla
```

### Procesos y sistema

| Comando | Qué hace |
| --- | --- |
| `ps aux` | Lista todos los procesos. |
| `top` / `htop` | Monitor de procesos en vivo. |
| `kill PID` | Envía señal de fin a un proceso. |
| `kill -9 PID` | Fuerza la terminación. |
| `jobs` / `fg` / `bg` | Gestiona trabajos en segundo plano. |
| `df -h` | Espacio en disco (legible). |
| `du -sh dir` | Tamaño total de una carpeta. |
| `free -h` | Memoria libre y usada. |
| `uptime` | Tiempo encendido y carga media. |
| `uname -a` | Información del sistema. |
| `date` | Fecha y hora. |
| `whoami` | Usuario actual. |

### Permisos

| Comando | Qué hace |
| --- | --- |
| `chmod +x f` | Añade permiso de ejecución. |
| `chmod 644 f` | Permisos `rw-r--r--`. |
| `chmod 755 f` | Permisos `rwxr-xr-x`. |
| `chown usuario:grupo f` | Cambia dueño y grupo. |
| `sudo cmd` | Ejecuta como root. |

### Comprimir y transferir

| Comando | Qué hace |
| --- | --- |
| `tar -czf a.tar.gz dir/` | Comprime un directorio. |
| `tar -xzf a.tar.gz` | Descomprime. |
| `gzip f` | Comprime `f` (lo deja como `f.gz`). |
| `zip -r a.zip dir/` | Empaqueta en zip. |
| `unzip a.zip` | Descomprime un zip. |
| `wget URL` | Descarga un fichero. |
| `curl -O URL` | Descarga con curl. |
| `scp f usuario@host:/ruta` | Copia por SSH. |

### Atajos de teclado

| Atajo | Qué hace |
| --- | --- |
| `++tab++` | Autocompleta (púlsalo dos veces para ver opciones). |
| `++up++` / `++down++` | Recorre el historial. |
| `++ctrl+r++` | Busca en el historial. |
| `++ctrl+c++` | Interrumpe el comando en curso. |
| `++ctrl+d++` | Fin de entrada (cierra la sesión si el prompt está vacío). |
| `++ctrl+l++` | Limpia la pantalla. |
| `++ctrl+a++` / `++ctrl+e++` | Ir al principio / final de la línea. |
| `++ctrl+u++` / `++ctrl+k++` | Borra hasta el principio / final. |
| `++ctrl+w++` | Borra la palabra anterior. |
| `++alt+.++` | Inserta el último argumento del comando anterior. |
| `!!` | Repite el último comando. |
| `!n` | Repite el comando número `n` del historial. |

## Ejemplos prácticos

One-liners listos para copiar y adaptar:

```bash
# Tamaño de cada carpeta del directorio actual, ordenado
du -sh */ | sort -h

# Los 10 procesos que más CPU consumen
ps aux --sort=-%cpu | head -n 11

# Contar cuántas líneas tiene cada .txt de la carpeta
wc -l *.txt

# Ranking de IPs en un log (top 10)
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head

# Buscar ficheros duplicados por contenido (mismo hash md5)
find . -type f -exec md5sum {} + | sort | uniq -w32 -D

# Sustituir recursivamente "foo" por "bar" en ficheros .conf
grep -rl "foo" --include="*.conf" . | xargs sed -i 's/foo/bar/g'

# Descargar y mirar solo las cabeceras HTTP
curl -I https://example.com

# Listar puertos a la escucha (necesita permisos para detalles)
ss -tulnp

# Qué ficheros han cambiado en las últimas 24 h
find . -type f -mtime -1

# Comprobar si un puerto está abierto con bash puro
timeout 2 bash -c "echo > /dev/tcp/127.0.0.1/22" && echo "abierto" || echo "cerrado"
```

Salida de ejemplo del primer *one-liner*:

```text
4.0K    Descargas/
128K    Documentos/
2.1M    proyectos/
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| `cmd > f` sobre el mismo fichero que lees | El shell lo vacía antes. | Usa un temporal y luego `mv`. |
| Los errores no se guardan | `>` no captura stderr. | Usa `2>` o `&>`. |
| `uniq` no agrupa | Falta `sort` antes. | `sort f` y luego `uniq -c`. |
| Comillas que rompen el comando | Comillas simples no interpolan. | Usa dobles si necesitas `$var`. |
| `rm` borró de más | Variable sin comillas o ruta mal escrita. | Pon comillas y revisa antes de ejecutar. |

!!! tip "Cuando dudes, pide ayuda en el momento"
    `man comando` abre el manual; `comando --help` suele dar un resumen rápido; `apropos palabra`
    busca en las descripciones de los manuales.

## Ejercicios

1. Muestra las 5 carpetas que más ocupan en tu `$HOME` (`du -sh */ | sort -h | tail -5`).
2. Cuenta cuántos ficheros `.md` hay en tu `$HOME` (`find ~ -name "*.md" | wc -l`).
3. Del fichero `access.log` de ejemplo, saca el top 5 de IPs.
4. Lista los procesos ordenados por memoria.
5. Comprueba en una línea si tu equipo tiene abierto el puerto 80.

??? success "Solución"

    **1.** `du -sh ~/*/ 2>/dev/null | sort -h | tail -5`

    **2.** `find ~ -name "*.md" | wc -l` (o `find ~ -name "*.md" -printf 'x\n' | wc -l` si los nombres
    llevan saltos de línea).

    **3.** `awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -5`

    **4.** `ps aux --sort=-%mem | head -n 11`

    **5.** `timeout 2 bash -c "echo > /dev/tcp/127.0.0.1/80" && echo "abierto" || echo "cerrado"`

## Resumen

- Esta página es una **referencia**: vuelve a ella cuando olvides una sintaxis.
- Domina sobre todo **redirecciones** (`>`, `>>`, `2>`, `&>`), tuberías (`|`) y el patrón
  `sort | uniq -c | sort -rn`.
- Los **atajos** (`++tab++`, `++ctrl+r++`, `++ctrl+c++`) multiplican tu velocidad.
- Para todo lo demás: `man`, `--help` y `apropos`.

## Checklist

- [ ] Tengo esta chuleta guardada o impresa.
- [ ] Sé redirigir salida y errores sin mirar.
- [ ] Uso los atajos de historial y autocompletado con soltura.
- [ ] Puedo escribir de memoria el patrón de ranking de logs.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [explainshell](https://explainshell.com) | Explica cualquier comando línea a línea | EN | Gratis |
| [Linux man pages](https://man7.org) | Manuales oficiales | EN | Gratis |
| [The Linux Command Line](https://linuxcommand.org) | Libro gratuito sobre la línea de comandos | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta una versión **imprimible en PDF** de esta chuleta. Debe generarla y publicarla el equipo
    de la web.

## Siguiente paso

Con Bash bajo el brazo, el siguiente paso es **guardar y versionar** tu trabajo. Sigue con el módulo
**[05 · Git y GitHub](../05-git-y-github/index.md)**.
