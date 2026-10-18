# 04 · GitHub, forks y Pull Requests

**GitHub es donde tu código deja de ser privado y se vuelve colaborativo (y visible).** Aquí
aprendes a conectar tu repositorio local con GitHub, a trabajar con remotos, a hacer *fork* de un
proyecto ajeno, a proponer cambios mediante **Pull Requests** y a escribir Markdown. Y una sección
crítica que puede salvarte de un disgusto serio: **qué nunca subir y qué hacer si subes un secreto**.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Explicar qué es GitHub y qué añade a Git.
- Trabajar con **repositorios remotos**: `clone`, `remote`, `push`, `pull`/`fetch`.
- Diferenciar **fork** y **clone**.
- Completar el flujo de un **Pull Request** de principio a fin.
- Escribir **Markdown** y un buen `README.md`.
- Contribuir a **esta web** con un PR.
- Identificar **qué nunca subir** y **reaccionar** si publicas un secreto.

**Tiempo estimado: 90-120 min.**

## Requisitos previos

- [Git básico](02-git-basico.md) y [Ramas, merge y conflictos](03-ramas-merge-y-conflictos.md).
- Cuenta en [GitHub](https://github.com) y acceso SSH configurado.

## Explicación

!!! danger "Lo más importante de toda la página"
    **Nunca subas a GitHub contraseñas, claves privadas, tokens ni ficheros `.env`.** Un repositorio
    público lo ve cualquiera, y un bot puede encontrar un secreto en **segundos**. Al final de esta
    página tienes la sección completa sobre qué hacer si te pasa.

### ¿Qué es GitHub?

GitHub es una **plataforma en la nube** para alojar repositorios Git y colaborar. Git es la
herramienta local; GitHub pone encima:

| Función | Para qué sirve |
| --- | --- |
| **Repositorios remotos** | Guardar tu proyecto en la nube (y respaldarlo). |
| **Pull Requests (PR)** | Proponer cambios y que otros los revisen antes de fusionarlos. |
| **Issues** | Reportar fallos, proponer mejoras, discutir. |
| **Actions** | Automatizar tareas (tests, despliegues). |
| **Pages** | Publicar webs estáticas (lo vemos en la [página 05](05-github-pages-y-perfil.md)). |
| **Wikis, Releases, Projects** | Documentación, versiones y gestión de tareas. |

GitHub es **gratuito** para repositorios públicos (y con plan gratuito también para privados, dentro
de unos límites). Hay alternativas como GitLab o Gitea, pero usaremos GitHub por ser el estándar de
facto.

### Repositorios remotos

Un **remoto** es una copia del repositorio en un servidor, con un nombre corto. El habitual es
**`origin`** (tu repo en GitHub) y a veces **`upstream`** (el repo original del que hiciste fork).

| Comando | Qué hace |
| --- | --- |
| `git clone URL` | Copia un repo remoto completo a tu máquina. |
| `git remote -v` | Lista los remotos configurados. |
| `git remote add origin URL` | Vincula tu repo local con uno remoto. |
| `git push` | Sube tus commits al remoto. |
| `git pull` | Trae y fusiona los cambios del remoto. |
| `git fetch` | Trae los cambios del remoto **sin** fusionarlos. |

!!! note "`push` sube, `pull` baja"
    En un equipo, lo normal es: `git pull` al empezar (traer lo de los demás), trabajar, `git add`,
    `git commit` y `git push` al terminar (subir lo tuyo).

### Fork vs clone

| | **Clone** | **Fork** |
| --- | --- | --- |
| Qué es | Copia local de un repo remoto. | Copia **en tu cuenta de GitHub** de un repo ajeno. |
| Dónde vive | En tu máquina. | En tu cuenta de GitHub. |
| Para qué | Trabajar en un repo al que tienes acceso. | Proponer cambios a un repo que **no** es tuyo. |

Flujo típico de contribución a un proyecto ajeno:

```text
 (1) Fork en GitHub        (2) Clone local         (3) Rama + commits
 ┌──────────────┐          ┌──────────────┐        ┌──────────────┐
 │ repo original│ ──fork──►│ TU copia     │─clone─►│ tu máquina   │
 └──────────────┘          └──────────────┘        └──────┬───────┘
                                                          │ (4) push
                                                          ▼
 (6) merge ◄── (5) Pull Request ◄──────────────────────────────────
```

### Pull Requests: el corazón de la colaboración

Un **Pull Request** es una **petición para que se acepten tus cambios**. No es un comando de Git: es
una función de GitHub. Se llama "pull" porque pides que el proyecto "tire" de tu rama para
incorporarla.

Ciclo completo:

1. **Fork** del repositorio (si no tienes permiso de escritura).
2. **Clone** de tu fork a tu máquina.
3. Crea una **rama** con nombre descriptivo (`fix/typo-readme`).
4. Haz tus **commits**.
5. **Push** de la rama a tu fork.
6. Abre el **Pull Request** en GitHub hacia el repo original.
7. **Revisión**: los mantenedores comentan; tú corriges con más commits.
8. **Merge**: si se aprueba, tus cambios se fusionan.

!!! tip "Buenas prácticas para un PR"
    - Un PR = **un tema**. No mezcles arreglos distintos.
    - Commits pequeños y con mensajes claros.
    - Sincroniza tu rama con el original (`git pull upstream main`) para evitar conflictos.
    - Explica **qué** cambias y **por qué** en la descripción del PR.

### Markdown y `README.md`

**Markdown** es un lenguaje de marcado ligero convertido a HTML. Es el idioma de los `README.md`, los
Issues y los comentarios de GitHub.

| Quieres… | Escribes… |
| --- | --- |
| Título | `# Título`, `## Subtítulo` |
| Negrita | `**texto**` |
| Cursiva | `*texto*` |
| Lista | `- elemento` |
| Lista numerada | `1. elemento` |
| Enlace | `[texto](https://url)` |
| Imagen | `![texto alternativo](imagen.png)` |
| Código en línea | `` `código` `` |
| Bloque de código | ```` ```bash ```` … ```` ``` ```` |
| Cita | `> texto` |
| Tabla | filas y columnas delimitadas por barras verticales |
| Tarea | `- [ ] pendiente` / `- [x] hecho` |

Las tablas se escriben con barras verticales; este es un ejemplo literal (dentro de un bloque de
código):

```markdown
| Columna 1 | Columna 2 |
| --------- | --------- |
| dato      | dato      |
```

El **`README.md`** es la portada del repositorio: es lo primero que ve quien entra. Un buen README
lleva:

- Qué es el proyecto (una o dos frases).
- Cómo instalarlo y usarlo.
- Ejemplos.
- Cómo contribuir.
- Licencia (si procede).

```markdown
# herramienta-x

Pequeña utilidad en Bash para ordenar logs por IP.

## Instalación
    chmod +x herramienta.sh

## Uso
    ./herramienta.sh access.log

## Licencia
MIT
```

### Cómo contribuir a esta web

Esta web es un proyecto **abierto**. El repositorio es
[github.com/UJACKING/ujacking.github.io](https://github.com/UJACKING/ujacking.github.io) y todo el
contenido vive en la carpeta `docs/`.

Flujo para contribuir:

1. Haz **fork** del repositorio a tu cuenta.
2. **Clona** tu fork: `git clone git@github.com:tu-usuario/ujacking.github.io.git`.
3. Añade el original como `upstream`:
   `git remote add upstream https://github.com/UJACKING/ujacking.github.io.git`.
4. Crea una **rama**: `git switch -c docs/fix-typo-bash`.
5. Edita los ficheros (páginas en Markdown dentro de `docs/`).
6. `git add`, `git commit` con un mensaje claro y `git push` a tu fork.
7. Abre un **Pull Request** hacia `main` del repositorio original explicando tu cambio.

!!! warning "Respeta la plantilla de nivel"
    Las páginas de Nivel 1 siguen una **plantilla obligatoria** (título, objetivos, requisitos,
    explicación, ejemplos, errores comunes, ejercicios con solución, resumen, checklist, recursos y
    siguiente paso). Si añades una página nueva, respétala. Los enlaces internos roto **rompen la
    build**: comprueba que cada enlace apunta a un fichero existente.

## La sección crítica: qué NUNCA subir

!!! danger "Un secreto subido a un repo público está comprometido para siempre"
    No es una exageración. Hay bots que escanean GitHub 24/7 en busca de claves y tokens recién
    subidos. En muchos casos, **en minutos** ya se está usando tu clave.

### Lista negra: lo que jamás debe acabar en Git

| Nunca subas… | Ejemplos |
| --- | --- |
| **Claves privadas SSH** | `id_rsa`, `id_ed25519` (¡los `.pub` sí se pueden!) |
| **Tokens de acceso** | tokens de GitHub, de APIs, de bots |
| **Contraseñas** | en scripts, configs, `.env` |
| **Ficheros de entorno** | `.env`, `.env.local`, `config.secret.json` |
| **Credenciales de nube** | `~/.aws/credentials`, claves de Azure/GCP |
| **Certificados y keystores** | `*.pem`, `*.key`, `*.p12`, `*.jks` |
| **Bases de datos con datos reales** | dumps `.sql` con datos personales |
| **Ficheros de configuración locales** | `settings.local.php`, `wp-config.php` real |

### Prevención (antes de que ocurra)

1. **`.gitignore` desde el primer momento:**

   ```text
   .env
   *.key
   *.pem
   id_rsa
   id_ed25519
   credentials.json
   *.sql
   ```

2. **Revisa antes de cada commit:** `git status` y `git diff --staged`.
3. **Nunca pegues secretos en el código:** usa **variables de entorno**.
4. **Escaneo de secretos:** GitHub y otras herramientas avisan si detectan una clave conocida; actívalo
   si puedes.

### Qué hacer si YA has subido un secreto

!!! warning "Regla número uno: asume que está comprometido"
    Aunque lo borres en un commit nuevo, **sigue en el historial** y en las copias que se hayan hecho.
    Borrarlo "por encima" **no** lo elimina. Hay que actuar como si ya lo tuviera alguien.

**Paso 1 — Revocar / rotar el secreto (lo PRIMERO, antes de nada más).**

- Si es un **token de GitHub**: ve a *Settings → Developer settings → Personal access tokens* y
  **revócalo**.
- Si es una **clave SSH**: elimínala de *Settings → SSH and GPG keys* y genera otra.
- Si es una **contraseña de servicio**: cámbiala en ese servicio.
- Si es una **clave de API/nube**: rótala en el panel del proveedor.

**Paso 2 — Quitarlo del estado actual.**

```bash
git rm --cached .env
echo ".env" >> .gitignore
git commit -m "Elimina .env del repositorio y lo añade a .gitignore"
git push
```

Esto lo saca de la **última** versión, pero **el secreto sigue en el historial**.

**Paso 3 — Reescribir el historial (con aviso).**

Para borrarlo de commits anteriores hay que **reescribir la historia** del repositorio. Se hace con
herramientas como `git filter-repo` (recomendada) o el *BFG Repo-Cleaner*.

!!! danger "Reescribir el historial es destructivo"
    Cambia los identificadores de los commits. Si alguien más trabaja en el repo:

    - **Avisa a TODO el equipo** antes.
    - Tendrán que **volver a clonar** o hacer un `reset` cuidadoso.
    - Después hay que hacer *force push*: `git push --force-with-lease`.
    - Si es un repo público con forks, el contenido podría seguir accesible en los forks.

    Si dudas, **pide ayuda** antes de reescribir historia en un repo compartido.

**Paso 4 — Si el secreto era muy sensible**, contacta con el proveedor (GitHub soporte, el servicio de
la clave…) para que invaliden accesos y, si procede, revisen el uso.

**Lo que NO funciona:**

| Idea equivocada | Por qué no sirve |
| --- | --- |
| "Lo borro con otro commit y ya está" | Sigue en el historial. |
| "El repo es privado, no pasa nada" | Los privados también se filtran y se comparten por error. |
| "Pongo el repositorio en privado" | El secreto ya puede estar copiado o en caché. |
| "Cambio solo la contraseña en el código" | El valor antiguo sigue en el historial. |

## Ejemplos prácticos

### Ejemplo 1 · Conectar un repo local con GitHub

```bash
cd ~/mi-proyecto
git remote add origin git@github.com:tu-usuario/mi-proyecto.git
git remote -v
git push -u origin main
```

```text
origin  git@github.com:tu-usuario/mi-proyecto.git (fetch)
origin  git@github.com:tu-usuario/mi-proyecto.git (push)
```

El `-u` la primera vez vincula `main` local con `origin/main`, y luego basta `git push`/`git pull`.

### Ejemplo 2 · Clonar y crear una rama para un PR

```bash
git clone git@github.com:tu-usuario/ujacking.github.io.git
cd ujacking.github.io
git remote add upstream https://github.com/UJACKING/ujacking.github.io.git
git switch -c docs/fix-typo-bash
```

### Ejemplo 3 · Sincronizar con el original

```bash
git fetch upstream
git switch main
git merge upstream/main
git push origin main
```

Traes los cambios del proyecto original (`upstream`) a tu `main` local y los subes a tu fork
(`origin`).

### Ejemplo 4 · El ciclo completo de un cambio

```bash
git switch -c fix/archivo-roto
# editas ficheros...
git add docs/nivel-1-principiante/04-bash/02-comandos-esenciales.md
git commit -m "Corrige ejemplo de find en comandos esenciales"
git push -u origin fix/archivo-roto
```

Tras el `push`, GitHub te muestra un enlace para **abrir el Pull Request**.

### Ejemplo 5 · Ver los remotos y el estado frente a ellos

```bash
git remote -v
git status
git log --oneline origin/main..main   # commits locales que no están en el remoto
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| `Permission denied (publickey)` | SSH mal configurado. | Reconfigura (página 02) y prueba `ssh -T git@github.com`. |
| `Updates were rejected` al hacer push | El remoto tiene commits que no tienes. | `git pull` (o `--rebase`) y vuelve a hacer push. |
| Olvidé hacer `pull` y hay conflictos | Trabajaste sobre una base antigua. | Resuelve conflictos (página 03). |
| Subí un `.env` | Error grave. | **Revoca** el secreto ya; luego límpialo (ver sección crítica). |
| El PR no aparece | Hiciste push a `main` de tu fork en vez de a una rama. | Crea una rama, sube ahí y abre el PR. |
| `fatal: not a git repository` | No estás en una carpeta con `.git`. | `cd` al repo correcto. |
| El README se ve raro | Markdown mal cerrado. | Revisa saltos de línea y bloques de código. |

## Ejercicios

1. Crea un repositorio en GitHub y sube tu `~/mi-proyecto` con `git remote add` y `git push`.
2. Haz *fork* de cualquier repositorio público que te interese (por ejemplo, uno de scripting) y
   clónalo.
3. Añade el remoto `upstream` a tu fork y comprueba con `git remote -v` que tienes `origin` y
   `upstream`.
4. Crea una rama, cambia el `README.md` añadiendo una sección, y súbela a tu fork.
5. Abre un Pull Request de esa rama hacia `main` de tu propio fork (aunque no lo fusiones).
6. *(Difícil)* Simula un secreto: crea un fichero `secreto.txt` con texto, añádelo y commitea. Luego
   quítalo del seguimiento con `git rm --cached` y añádelo a `.gitignore`. Explica en tus palabras
   **por qué** el contenido sigue en el historial.

??? success "Solución"

    **1.**
    ```bash
    cd ~/mi-proyecto
    git remote add origin git@github.com:tu-usuario/mi-proyecto.git
    git push -u origin main
    ```
    (El repositorio debe existir antes en GitHub; no lo crees con README si ya tienes commits
    locales.)

    **2.** En GitHub, botón **Fork** → luego `git clone git@github.com:tu-usuario/repo.git`.

    **3.**
    ```bash
    cd repo
    git remote add upstream https://github.com/propietario/repo.git
    git remote -v
    ```

    **4.**
    ```bash
    git switch -c docs/nueva-seccion
    echo "## Nueva sección" >> README.md
    git add README.md && git commit -m "Añade sección al README"
    git push -u origin docs/nueva-seccion
    ```

    **5.** En GitHub, tras el push, pulsa **Compare & pull request** (o *Pull requests → New*), elige
    base `main` y compara tu rama. Rellena título y descripción.

    **6.**
    ```bash
    echo "contrasena123" > secreto.txt
    git add secreto.txt && git commit -m "añade secreto"
    git rm --cached secreto.txt
    echo "secreto.txt" >> .gitignore
    git commit -m "quita secreto y lo ignora"
    ```
    El fichero **ya no aparece** en los commits nuevos, pero el commit antiguo todavía contiene su
    contenido: cualquiera que mire el historial (`git log -p`) lo ve. Por eso hay que **revocar** el
    secreto y, si de verdad importa, reescribir la historia.

## Resumen

- **GitHub** aloja repositorios Git y añade PR, Issues, Actions y Pages.
- Remotos: `clone`, `remote add`, `push` (subir), `pull`/`fetch` (bajar). `origin` es el habitual.
- **Fork** = copia en tu cuenta; **clone** = copia en tu máquina.
- Un **Pull Request** propone cambios y se revisa antes del merge.
- **Markdown** da formato a `README.md`, Issues y PRs.
- Contribuir a esta web: fork → clona → rama → cambios → push → PR.
- **Nunca** subas claves, tokens, contraseñas ni `.env`. Si lo haces, **revoca primero**, luego limpia
  (y reescribe historia con cuidado).

## Checklist

- [ ] Sé conectar un repo local con GitHub y hacer `push`/`pull`.
- [ ] Distingo fork de clone y sé cuándo usar cada uno.
- [ ] He completado (o entiendo) el flujo fork → rama → PR.
- [ ] Sé escribir Markdown y un `README.md` decente.
- [ ] Sé cómo contribuir a esta web con un PR.
- [ ] Tengo claro qué **nunca** subir.
- [ ] Sé reaccionar si subo un secreto: revocar, limpiar y, con aviso, reescribir historial.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [GitHub Docs](https://docs.github.com) | Documentación oficial (PR, fork, SSH) | EN | Gratis |
| [GitHub Skills](https://skills.github.com) | Cursos interactivos dentro de GitHub | EN | Gratis |
| [Guía de Markdown de GitHub](https://docs.github.com) | Sintaxis completa | EN | Gratis |
| [git-filter-repo](https://github.com/newren/git-filter-repo) | Herramienta para limpiar historial | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta una guía de **Pull Requests en español** con enlace verificado, y una lista de comprobación
    propia de la web para revisar PRs de contenido. Debe añadirlas un redactor.

## Siguiente paso

Ya colaboras en GitHub. Ahora, a publicar y a lucirte:
**[05 · GitHub Pages y perfil](05-github-pages-y-perfil.md)**.
