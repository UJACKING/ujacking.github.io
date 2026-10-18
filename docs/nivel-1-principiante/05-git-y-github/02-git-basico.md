# 02 · Git básico

**Aquí empieza lo práctico.** Instalamos Git, lo configuramos, preparamos el acceso a GitHub (con
claves SSH o token) y usamos el ciclo de trabajo fundamental: `init`, `status`, `add`, `commit`,
`log`, `diff`, `.gitignore`. Al terminar tendrás un repositorio local propio y sabrás guardarlo, ver
qué cambió y volver atrás.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Instalar Git en Linux, Windows y macOS.
- Configurar tu identidad con `git config`.
- Generar y usar **claves SSH** (paso a paso) y, como alternativa, un **token** de acceso.
- Crear un repositorio con `git init` y entender el **staging area**.
- Registrar cambios con `git add` y `git commit`.
- Consultar el estado (`status`), el historial (`log`) y las diferencias (`diff`).
- Excluir ficheros con `.gitignore`.

**Tiempo estimado: 90-120 min.**

## Requisitos previos

- [Control de versiones](01-control-de-versiones.md) (conceptos y vocabulario).
- Terminal y comandos básicos del [módulo de Bash](../04-bash/index.md).
- Una cuenta gratuita en [GitHub](https://github.com).

## Explicación

### Instalar Git

=== "Debian / Ubuntu / Kali"

    ```bash
    sudo apt update
    sudo apt install git
    git --version
    ```

=== "Fedora / RHEL"

    ```bash
    sudo dnf install git
    git --version
    ```

=== "Arch / Manjaro"

    ```bash
    sudo pacman -S git
    git --version
    ```

=== "Windows"

    1. Descarga el instalador desde [git-scm.com](https://git-scm.com/downloads) y ejecútalo, o usa
       `winget install --id Git.Git`.
    2. Al instalar, verás **Git Bash**: una terminal con Git ya disponible.
    3. Comprueba con `git --version` en Git Bash, PowerShell o CMD.

=== "macOS"

    ```bash
    brew install git
    git --version
    ```

    (Si no tienes Homebrew, instalar las *Command Line Tools* de Xcode también trae Git.)

!!! info "Versión vigente"
    No memorices números de versión: comprueba con `git --version` cuál tienes instalada. Para la
    última disponible, consulta [git-scm.com](https://git-scm.com).

### Configurar tu identidad

Git firma cada commit con tu nombre y tu email. Se configuran una vez (global) o por repositorio
(local):

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global init.defaultBranch main
git config --global core.editor "nano"
```

```bash
git config --list
```

```text
user.name=Tu Nombre                              (salida de ejemplo)
user.email=tu@email.com
init.defaultBranch=main
core.editor=nano
```

- `user.name` y `user.email` → quién firma los commits.
- `init.defaultBranch main` → los repos nuevos usan `main` como rama principal.
- `core.editor nano` → editor por defecto para los mensajes de commit.

### Acceso a GitHub: SSH o token

Para subir tu trabajo a GitHub necesitas autenticarte. Hay dos caminos habituales:

| Método | Cómo funciona | Recomendado para |
| --- | --- | --- |
| **SSH** | Usas un par de claves (pública/privada). No tecleas contraseñas tras configurarlo. | Uso diario cómodo. |
| **Token (HTTPS)** | Una contraseña especial de un solo uso para Git, guardada como credencial. | Quien prefiere no tocar claves. |

!!! danger "GitHub ya no acepta tu contraseña normal por HTTPS"
    Cuando Git te pida la contraseña por HTTPS, hay que darle un **token de acceso personal**, no la
    contraseña de tu cuenta. Crea uno en GitHub: *Settings → Developer settings → Personal access
    tokens*. Guarda el token en un gestor de contraseñas; **no lo pongas en el código**.

#### Generar claves SSH paso a paso

!!! warning "Antes de nada: protección de claves"
    La clave **privada** (`id_ed25519`, sin `.pub`) es como la llave de tu casa: **nunca** la
    compartas ni la subas a ningún sitio. La **pública** (`.pub`) es la que se da a GitHub, y esa sí
    se puede compartir.

**Paso 1 — Comprueba si ya tienes claves:**

```bash
ls -la ~/.ssh
```

Si ves `id_ed25519` e `id_ed25519.pub`, ya tienes un par y puedes saltar al paso 3.

**Paso 2 — Genera un par de claves (ed25519):**

```bash
ssh-keygen -t ed25519 -C "tu@email.com"
```

- `-t ed25519` → tipo de clave moderno y seguro. Si tu sistema es muy antiguo y no lo soporta, se usa
  `-t rsa -b 4096`.
- `-C` → un comentario, normalmente tu email, para identificarla.

El programa pregunta dónde guardar (`~/.ssh/id_ed25519` por defecto: pulsa `++enter++`) y una
**frase de paso** (*passphrase*) opcional pero **recomendada**: si alguien roba tu clave privada, sin
esa frase no puede usarla.

**Paso 3 — Añade la clave al agente SSH** (para no escribir la frase cada vez):

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

**Paso 4 — Copia la clave pública:**

```bash
cat ~/.ssh/id_ed25519.pub
```

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAA... tu@email.com   (salida de ejemplo)
```

Copia **toda** esa línea (empieza por `ssh-ed25519` y termina con tu email).

**Paso 5 — Añádela a GitHub:**

1. Entra en GitHub → tu foto de perfil → **Settings**.
2. Menú lateral → **SSH and GPG keys**.
3. Botón **New SSH key**.
4. Título descriptivo (p. ej. "Portátil personal") y pega la clave pública.
5. **Add SSH key**.

**Paso 6 — Comprueba que funciona:**

```bash
ssh -T git@github.com
```

```text
Hi usuario! You've successfully authenticated, but GitHub does not provide shell access.
```

Ese mensaje (con tu nombre de usuario) significa que **todo va bien**. La primera vez puede pedirte
confirmar la huella (`yes`).

### El ciclo de trabajo de Git

Git tiene tres zonas. Entenderlas es la mitad de todo:

```text
   Directorio de trabajo        Staging area            Repositorio (.git)
   (donde editas)               (lo preparado)          (commits guardados)
         │                            │                         │
         │       git add              │      git commit         │
         └───────────────────────────►└────────────────────────►│
         ◄────────────────────────────────────────────────────  │
                        git checkout / git restore
```

| Zona | Qué contiene | Cómo pasas de ella |
| --- | --- | --- |
| **Directorio de trabajo** | Tus ficheros tal cual los editas. | `git add` los lleva al staging. |
| **Staging area** (índice) | Lo que **incluirás** en el próximo commit. | `git commit` lo guarda. |
| **Repositorio** | Los commits guardados. | `git checkout`/`git restore` recupera. |

La gracia del staging es que **tú eliges qué entra en cada commit**, aunque hayas tocado veinte
ficheros.

### `git status`: tu brújula

Lo vas a usar constantemente. Te dice en qué rama estás, qué está preparado (staged) y qué no.

### `.gitignore`: lo que Git debe ignorar

Hay ficheros que **no** quieres versionar: salidas de programas, dependencias, logs, y sobre todo
**secretos**. Se listan en un fichero `.gitignore` en la raíz del repo.

```text
# .gitignore
*.log
*.tmp
node_modules/
venv/
.env
*.key
*.pem
__pycache__/
```

- `*.log` → ignora todos los `.log`.
- `node_modules/` → ignora una carpeta entera (la barra final indica directorio).
- `.env`, `*.key`, `*.pem` → **secretos**: deben quedarse fuera siempre.

## Ejemplos prácticos

### Ejemplo 1 · Crear un repositorio desde cero

```bash
mkdir -p ~/mi-proyecto && cd ~/mi-proyecto
git init
git status
```

```text
Initialized empty Git repository in /home/usuario/mi-proyecto/.git/
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

`git init` crea la carpeta oculta `.git/`. Ya es un repositorio, pero **vacío**.

### Ejemplo 2 · Primer commit

```bash
echo "# Mi proyecto" > README.md
git status
git add README.md
git status
git commit -m "Añade README inicial"
```

```text
On branch main
No commits yet
Untracked files:
        README.md

nothing added to commit but untracked files present (use "git add" to track)

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md

[main (root-commit) 1a2b3c4] Añade README inicial
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

Fíjate en la secuencia: primero **untracked** (Git no lo sigue), tras `git add` está **staged**, y
tras `git commit` queda **guardado**.

### Ejemplo 3 · Varios ficheros y añadirlos todos

```bash
echo "contenido" > notas.txt
echo "linea" > otro.txt
git add .
git status
git commit -m "Añade notas y otro"
```

`git add .` añade **todo** lo que haya cambiado en el directorio actual (y subcarpetas). Cómodo,
pero revisa antes con `git status` para no añadir algo que no quieres.

### Ejemplo 4 · Ver el historial

```bash
git log
git log --oneline
git log --oneline --graph --all
```

```text
commit 5f6e7d8...   (salida de ejemplo)
Author: Tu Nombre <tu@email.com>
Date:   ...

    Añade notas y otro

5f6e7d8 Añade notas y otro
1a2b3c4 Añade README inicial
```

`--oneline` compacta cada commit a una línea. `--graph --all` dibuja el árbol de ramas (útil más
adelante).

### Ejemplo 5 · Ver qué ha cambiado con `diff`

```bash
echo "otra linea" >> README.md
git diff
```

```text
diff --git a/README.md b/README.md
index e69de29..1234567 100644
--- a/README.md
+++ b/README.md
@@ -1 +1,2 @@
 # Mi proyecto
+otra linea
```

- `git diff` → cambios **aún no preparados** (entre el directorio de trabajo y el staging).
- `git diff --staged` → cambios **ya preparados** (entre el staging y el último commit).

### Ejemplo 6 · Deshacer: restaurar un fichero

```bash
git restore README.md
git status
```

`git restore` descarta los cambios **no preparados** de un fichero y lo devuelve al último commit.
Cuidado: lo que no estaba preparado se pierde. Para sacar algo del staging (deshacer `git add`):

```bash
git restore --staged README.md
```

### Ejemplo 7 · Un `.gitignore` funcional

```bash
cat > .gitignore <<'EOF'
*.log
.env
*.key
EOF
echo "texto de log" > prueba.log
git status
```

```text
On branch main
Untracked files:
        .gitignore
        README.md

(prueba.log NO aparece: está ignorado)
```

`prueba.log` no sale en `git status` porque `.gitignore` lo excluye.

### Ejemplo 8 · Ignorar algo que ya está versionado

!!! warning "`.gitignore` no afecta a ficheros ya añadidos"
    Si un fichero **ya está** en Git, añadirlo a `.gitignore` no lo deja de seguir. Hay que
    quitarlo del seguimiento:
    ```bash
    git rm --cached secreto.txt
    ```
    El `--cached` borra de Git pero **no** del disco.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| `Please tell me who you are` | Falta `user.name`/`user.email`. | Configúralos con `git config --global`. |
| Nada que commitear | No hiciste `git add` o ya commiteaste. | Revisa `git status`. |
| Se commiteó un fichero que quería ignorar | Estaba ya versionado. | `git rm --cached fichero` y añádelo a `.gitignore`. |
| `Permission denied (publickey)` | Clave SSH mal añadida o no cargada. | Rehaz `ssh-add` y `ssh -T git@github.com`. |
| Se subió un secreto | Error grave. | Ver [04 · GitHub, forks y Pull Requests](04-github-forks-y-pull-requests.md) y **revocar** el secreto ya. |
| Mensajes de commit vacíos | `git commit` sin `-m` abre el editor. | Escribe el mensaje y guarda, o usa `-m "..."`. |
| Perdí cambios con `git restore` | Descartaste cambios no preparados. | No hay vuelta si nunca se prepararon. Por eso `git add` pronto. |

## Ejercicios

1. Instala Git (o comprueba que está instalado) y muestra su versión.
2. Configura tu `user.name` y `user.email` globales.
3. Genera un par de claves SSH y añade la pública a tu cuenta de GitHub. Comprueba con
   `ssh -T git@github.com`.
4. Crea un repositorio llamado `mi-proyecto`, añade un `README.md` y haz tu primer commit.
5. Crea un `.gitignore` que ignore `*.log` y `.env`, y comprueba que un fichero `x.log` no aparece en
   `git status`.
6. *(Difícil)* Modifica el `README.md`, comprueba la diferencia con `git diff`, prepárala con
   `git add`, vuelve a mirar con `git diff --staged` y haz el commit. Después deshaz el commit **sin
   borrar los cambios** (pista: `git reset --soft HEAD~1`).

??? success "Solución"

    **1.**
    ```bash
    git --version
    ```

    **2.**
    ```bash
    git config --global user.name "Tu Nombre"
    git config --global user.email "tu@email.com"
    git config --list
    ```

    **3.**
    ```bash
    ssh-keygen -t ed25519 -C "tu@email.com"
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_ed25519
    cat ~/.ssh/id_ed25519.pub
    ```
    Copia la clave pública a GitHub (*Settings → SSH and GPG keys → New SSH key*) y comprueba:
    ```bash
    ssh -T git@github.com
    ```

    **4.**
    ```bash
    mkdir ~/mi-proyecto && cd ~/mi-proyecto
    git init
    echo "# Mi proyecto" > README.md
    git add README.md
    git commit -m "Añade README inicial"
    ```

    **5.**
    ```bash
    printf '*.log\n.env\n' > .gitignore
    echo "prueba" > x.log
    git status
    ```
    `x.log` no debe aparecer.

    **6.**
    ```bash
    echo "linea nueva" >> README.md
    git diff
    git add README.md
    git diff --staged
    git commit -m "Actualiza README"
    git reset --soft HEAD~1
    ```
    `--soft` deshace el commit y deja los cambios **preparados** (en el staging), sin perder nada.

## Resumen

- Instala Git (`apt`, `dnf`, `pacman`, Homebrew, instalador de Windows) y verifica con
  `git --version`.
- Configura identidad: `user.name`, `user.email`, `init.defaultBranch`, `core.editor`.
- Acceso a GitHub: **SSH** (claves ed25519) o **token** por HTTPS.
- Las claves SSH: `ssh-keygen -t ed25519 -C "email"` → `ssh-add` → pegar `.pub` en GitHub →
  `ssh -T git@github.com`.
- Ciclo: `init` → editar → `status` → `add` → `commit` → `log`/`diff`.
- Tres zonas: directorio de trabajo, **staging**, repositorio.
- `.gitignore` excluye ficheros; si ya estaban versionados, `git rm --cached`.
- `git restore` deshace cambios; `git restore --staged` deshace un `add`.

## Checklist

- [ ] Tengo Git instalado y sé su versión.
- [ ] Configuré mi nombre y email.
- [ ] Generé una clave SSH, la añadí a GitHub y `ssh -T git@github.com` funciona.
- [ ] Sé crear un repo, añadir ficheros y hacer commits con buenos mensajes.
- [ ] Entiendo el staging area y la diferencia entre `add` y `commit`.
- [ ] Sé leer `git status`, `git log` y `git diff`.
- [ ] Tengo un `.gitignore` y sé ignorar ficheros ya versionados.
- [ ] Sé deshacer cambios sin perder trabajo.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Pro Git (libro)](https://git-scm.com/book/es/v2) | Libro oficial de Git | **ES** | Gratis |
| [Documentación de Git](https://git-scm.com/doc) | Referencia de comandos | EN | Gratis |
| [GitHub Docs · autenticación](https://docs.github.com) | SSH y tokens explicados | EN | Gratis |
| [Oh My Git!](https://ohmygit.org) | Juego para aprender Git | EN | Gratis |

## Siguiente paso

Con los commits dominados, toca organizar el trabajo con ramas:
**[03 · Ramas, merge y conflictos](03-ramas-merge-y-conflictos.md)**.
