# 03 · Tuberías, redirecciones y filtros

**Aquí es donde la línea de comandos se vuelve superpoderosa.** Cada programa tiene una entrada y
una salida; si aprendes a conectarlas, puedes construir con comandos simples algo que ningún programa
hace por sí solo: analizar miles de líneas de un log en un segundo, contar IPs, filtrar errores. Esta
página explica los tres flujos estándar, las redirecciones (`>`, `>>`, `2>`, `&>`, `<`), las tuberías
(`|`) y cómo combinarlas con filtros.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Explicar **stdin**, **stdout** y **stderr**.
- Redirigir la salida con `>`, `>>`, `2>`, `&>` y la entrada con `<`.
- Encadenar comandos con **tuberías** (`|`).
- Combinar tuberías con filtros (`grep`, `sort`, `uniq`, `wc`, `cut`, `awk`).
- Descartar errores con `/dev/null` y entender cuándo conviene.
- Construir pipelines reales de análisis de logs.

**Tiempo estimado: 60-90 min.**

## Requisitos previos

- [Comandos esenciales](02-comandos-esenciales.md) (sobre todo `grep`, `sort`, `uniq`, `wc`, `cut`,
  `awk`).
- Una terminal Linux abierta.

## Explicación

### Los tres flujos estándar

Todo proceso en Linux, cuando se ejecuta, tiene (al menos) **tres canales** abiertos:

| Canal | Nombre | Número | Para qué |
| --- | --- | --- | --- |
| Entrada estándar | **stdin** | 0 | De dónde **lee** el programa. Por defecto, tu teclado. |
| Salida estándar | **stdout** | 1 | Dónde **escribe** los resultados. Por defecto, la pantalla. |
| Salida de error | **stderr** | 2 | Dónde escribe los **mensajes de error**. Por defecto, también la pantalla. |

La clave: **stdout y stderr son canales separados**, aunque ambos se vean en pantalla. Eso permite
redirigirlos de forma independiente. Por ejemplo, puedes guardar los resultados en un fichero y dejar
los errores en pantalla, o al revés.

```text
                 ┌──────────────┐
   stdin (0) ───►│   PROGRAMA   │───► stdout (1)  ← resultados
                 │  (p. ej. ls) │───► stderr (2)  ← errores
                 └──────────────┘
```

### Redirecciones

Redirigir es **cambiar el destino u origen** de esos canales.

| Sintaxis | Qué hace | ¿Sobrescribe? |
| --- | --- | --- |
| `comando > fichero` | Manda stdout a `fichero`. | **Sí** (lo vacía antes). |
| `comando >> fichero` | **Añade** stdout al final de `fichero`. | No (añade). |
| `comando 2> fichero` | Manda **stderr** a `fichero`. | Sí. |
| `comando 2>> fichero` | Añade **stderr** al final. | No. |
| `comando &> fichero` | Manda **stdout y stderr** juntos. | Sí. |
| `comando < fichero` | Toma la **entrada** desde `fichero`. | — |

!!! warning "`>` borra sin avisar"
    `comando > fichero` **sobreescribe** el fichero por completo. Si tenías algo importante ahí, se
    pierde. Usa `>>` para **añadir**. Es una de las formas más fáciles de cargarse un log o un
    fichero de configuración sin querer.

### Tuberías: conectar programas

La **tubería** (`|`) conecta la **stdout** de un comando con la **stdin** del siguiente:

```text
comando1 | comando2 | comando3
   │  stdout ──► stdin │  stdout ──► stdin │
   ▼                   ▼                   ▼
resultado ────────► filtrado ────────► resultado final
```

Así construyes *pipelines*: pequeñas piezas encadenadas donde cada una hace una cosa bien.

### Filtros: las piezas reutilizables

Un **filtro** es un programa que lee de stdin, transforma, y escribe en stdout. Por eso se combinan
tan bien con `|`. Los que más usarás:

| Filtro | Qué hace | Ejemplo de uso |
| --- | --- | --- |
| `grep` | Deja pasar solo las líneas que coinciden. | `grep "error" fichero.log` |
| `sort` | Ordena. | `sort lista.txt` |
| `uniq -c` | Cuenta repeticiones consecutivas. | `sort lista.txt` y luego `uniq -c` |
| `wc -l` | Cuenta líneas. | `wc -l fichero.txt` |
| `cut` | Extrae columnas. | `cut -d' ' -f1 access.log` |
| `awk` | Procesa por campos. | `awk '{print $1}' access.log` |
| `head` / `tail` | Recorta. | `head -n 10 fichero.txt` |

### `/dev/null`: el agujero negro

`/dev/null` es un fichero especial que **descarta todo lo que se le escribe**. Redirigir ahí es la
forma estándar de **silenciar** algo:

```bash
comando 2>/dev/null        # calla los errores
comando >/dev/null         # calla la salida normal
comando &>/dev/null        # calla todo
```

## Ejemplos prácticos

### Ejemplo 1 · Guardar la salida en un fichero

```bash
ls -l > listado.txt
cat listado.txt
```

```text
total 8
-rw-r--r-- 1 usuario usuario   0 oct 18 12:00 listado.txt   (salida de ejemplo)
```

La salida de `ls -l` ya **no** aparece en pantalla: se ha escrito en `listado.txt`. Por eso el
`cat` posterior sí la muestra.

### Ejemplo 2 · Añadir sin borrar (`>>`)

```bash
echo "primera linea" > log.txt
echo "segunda linea" >> log.txt
cat log.txt
```

```text
primera linea
segunda linea
```

El primer `>` crea el fichero; el segundo `>>` **añade** sin borrar lo anterior. Si hubieses usado
`>` en la segunda línea, verías solo "segunda linea".

### Ejemplo 3 · Separar errores (stdout vs stderr)

```bash
ls /etc /ruta/que/no/existe 2> errores.txt
cat errores.txt
```

```text
ls: cannot access '/ruta/que/no/existe': No such file or directory   (salida de ejemplo)
```

Lo que `ls` encuentra bien sale por stdout (pantalla); el error de la ruta inexistente se guarda en
`errores.txt` porque lo redirigimos con `2>`.

### Ejemplo 4 · Juntar y descartar

```bash
ls /etc /ruta/que/no/existe &> todo.txt
ls /etc /ruta/que/no/existe 2>/dev/null | head
```

- `&> todo.txt` guarda **salida y errores** en el mismo fichero.
- `2>/dev/null` tira los errores y deja pasar solo los aciertos a la tubería.

### Ejemplo 5 · La tubería clásica: contar usuarios

```bash
cat /etc/passwd | grep "/bin/bash" | wc -l
```

```text
3                              (salida de ejemplo)
```

Lee `/etc/passwd`, quédate con las líneas del shell `bash` y cuenta cuántas hay. Nota: `grep` puede
leer el fichero directamente (`grep -c "/bin/bash" /etc/passwd`), que es más eficiente; aquí usamos
la tubería para ver el mecanismo.

### Ejemplo 6 · Ranking de IPs en un log

Creamos un log de ejemplo:

```bash
cat > access.log <<'EOF'
10.0.0.5 GET /index.html 200
10.0.0.7 GET /login 401
10.0.0.5 POST /login 200
10.0.0.9 GET /admin 403
10.0.0.5 GET /img.png 200
10.0.0.7 GET /index.html 200
EOF
```

Y ahora el análisis:

```bash
cut -d' ' -f1 access.log | sort | uniq -c | sort -rn
```

```text
      3 10.0.0.5
      2 10.0.0.7
      1 10.0.0.9
```

**Línea a línea:**

1. `cut -d' ' -f1` → extrae la primera columna (la IP).
2. `sort` → agrupa las IPs iguales juntas.
3. `uniq -c` → cuenta cuántas veces seguidas aparece cada una.
4. `sort -rn` → ordena por número, de mayor a menor.

Este patrón (`cut | sort | uniq -c | sort -rn`) es **el pan de cada día** del análisis de logs.

### Ejemplo 7 · Filtrar peticiones con error y extraer la ruta

```bash
awk '$4 >= 400 { print $1, $3, $4 }' access.log
```

```text
10.0.0.7 /login 401
10.0.0.9 /admin 403
```

`awk` imprime solo las líneas cuyo cuarto campo (el código HTTP) es 400 o superior: es decir, los
accesos fallidos o prohibidos.

### Ejemplo 8 · Pipeline largo encadenado

Objetivo: de un log de logins fallidos, sacar los usuarios más atacados, top 3.

```bash
cat > auth.log <<'EOF'
Failed password for root from 10.0.0.5
Failed password for root from 10.0.0.8
Failed password for admin from 10.0.0.5
Failed password for root from 10.0.0.9
Failed password for admin from 10.0.0.2
Failed password for user from 10.0.0.5
EOF

grep "Failed password" auth.log | awk '{ print $4 }' | sort | uniq -c | sort -rn | head -n 3
```

```text
      3 root
      2 admin
      1 user
```

Léelo de izquierda a derecha como una cadena de montaje:

1. `grep "Failed password"` → solo las líneas de intentos fallidos.
2. `awk '{ print $4 }'` → el cuarto campo (el usuario).
3. `sort | uniq -c` → cuenta por usuario.
4. `sort -rn` → ordena de más a menos.
5. `head -n 3` → los tres primeros.

### Ejemplo 9 · Guardar el resultado y verlo a la vez (`tee`)

```bash
grep "Failed" auth.log | tee fallidos.txt | wc -l
```

```text
6
```

`tee` escribe en `fallidos.txt` y deja pasar el flujo a `wc -l`, que cuenta 6 líneas.

### Ejemplo 10 · Leer de un fichero con `<`

```bash
tr 'a-z' 'A-Z' < auth.log | head -n 1
```

```text
FAILED PASSWORD FOR ROOT FROM 10.0.0.5
```

`< auth.log` le dice a `tr` que lea de ahí en vez del teclado.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| El fichero que redirigía se quedó vacío | Usaste `>` sobre el mismo fichero que leías (`cmd f.txt > f.txt`). El shell lo vacía antes de leer. | Escribe a otro fichero temporal y luego muévelo, o usa `>>`. |
| Los errores no se guardan con `>` | `2>` es **otra** redirección. `>` solo captura stdout. | Usa `2>` o `&>`. |
| `uniq` no cuenta bien | Falta `sort` antes. | Encadena `sort` y luego `uniq -c`. |
| El pipeline "no hace nada" | El primer comando no produce salida o `grep` no encuentra coincidencias. | Ejecuta por partes para depurar. |
| `Permission denied` al redirigir | Escribes en un sitio sin permisos (p. ej. `/etc`). | Escribe en tu carpeta y luego mueve con permisos. |
| `head` no corta el pipeline | El comando anterior sigue generando datos (p. ej. `tail -f`). | `++ctrl+c++` para parar. |

!!! tip "Depura pipelines por partes"
    Si un pipeline largo no da el resultado esperado, córtalo y ejecuta solo las primeras etapas.
    Añade `| head` para ver una muestra sin inundar la pantalla.

## Ejercicios

1. Guarda la lista de procesos en un fichero `procesos.txt` y muestra sus 5 primeras líneas.
2. Añade (sin borrar) la fecha actual al final de `procesos.txt` con `date >>`.
3. Redirige solo los errores del comando `ls /etc /nada` a `err.txt` y comprueba su contenido.
4. Del fichero `access.log`, muestra solo las peticiones que devolvieron **200**, con la IP y la ruta.
5. Cuenta cuántas peticiones hizo cada IP en `access.log` y muéstralas ordenadas de mayor a menor.
6. *(Difícil)* Del fichero `auth.log`, obtén los **usuarios atacados exactamente 1 vez**, y guarda el
   resultado en `poco-atacados.txt` a la vez que lo ves en pantalla.

??? success "Solución"

    **1. Guardar procesos y ver las primeras 5:**
    ```bash
    ps aux > procesos.txt
    head -n 5 procesos.txt
    ```

    **2. Añadir la fecha:**
    ```bash
    date >> procesos.txt
    tail -n 1 procesos.txt
    ```

    **3. Solo errores a `err.txt`:**
    ```bash
    ls /etc /nada 2> err.txt
    cat err.txt
    ```

    **4. Peticiones 200, IP y ruta:**
    ```bash
    awk '$4 == 200 { print $1, $3 }' access.log
    ```

    **5. Ranking de IPs:**
    ```bash
    cut -d' ' -f1 access.log | sort | uniq -c | sort -rn
    ```

    **6. Usuarios atacados una sola vez, viendo y guardando:**
    ```bash
    grep "Failed password" auth.log | awk '{ print $4 }' \
      | sort | uniq -c | awk '$1 == 1 { print $2 }' \
      | tee poco-atacados.txt
    ```
    La segunda llamada a `awk` filtra las líneas cuyo contador es exactamente 1 e imprime el usuario.

## Resumen

- Tres flujos: **stdin (0)**, **stdout (1)** y **stderr (2)**; stdout y stderr van separados.
- Redirecciones: `>` (sobrescribe), `>>` (añade), `2>` (errores), `&>` (todo), `<` (entrada).
- `/dev/null` descarta lo que se le manda: ideal para silenciar.
- `|` conecta la salida de un comando con la entrada del siguiente.
- Los **filtros** (`grep`, `sort`, `uniq`, `wc`, `cut`, `awk`…) se encadenan de maravilla.
- El patrón de análisis por excelencia: `... | cut/awk | sort | uniq -c | sort -rn`.

## Checklist

- [ ] Distingo stdin, stdout y stderr y sé redirigir cada uno.
- [ ] Sé cuándo usar `>` y cuándo `>>`.
- [ ] Sé capturar errores con `2>` y juntarlos con `&>`.
- [ ] Uso `/dev/null` para silenciar salidas.
- [ ] Construyo pipelines con `|` y varios filtros.
- [ ] Sé leer un pipeline de izquierda a derecha y depurarlo por partes.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [GNU Bash · Redirections](https://www.gnu.org/software/bash/manual/) | Manual oficial del shell (redirecciones y tuberías) | EN | Gratis |
| [Linux man pages](https://man7.org) | `man bash`, `man grep`, `man awk` | EN | Gratis |
| [OverTheWire · Bandit](https://overthewire.org) | Juego para practicar comandos y tuberías | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta un ejemplo guiado de análisis de un log **real y descargable** (con enlace verificado) para
    practicar pipelines. Debe añadirlo un redactor.

## Siguiente paso

Ya sabes encadenar comandos. El siguiente paso es automatizar: convertir esas cadenas en programas
reutilizables con **[04 · Scripts en Bash](04-scripts-bash.md)**.
