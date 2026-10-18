# 03 · Ramas, merge y conflictos

**Las ramas son la forma en que Git te deja probar cosas sin romper lo que funciona.** Cada rama es
una línea de desarrollo independiente: puedes desarrollar una función nueva, arreglar un fallo o
escribir una página, todo aislado, y luego fusionarlo (`merge`) con la rama principal cuando esté
listo. Esta página explica las ramas y, sobre todo, cómo resolver **conflictos** paso a paso con un
ejemplo real.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Explicar qué es una rama y qué es `HEAD`.
- Crear, listar y cambiar de rama con `git branch` y `git switch`.
- Fusionar ramas con `git merge` (fast-forward y *three-way*).
- Entender **por qué** se producen conflictos.
- Resolver un conflicto **paso a paso** y confirmar el merge.
- Deshacer un merge a medias (`git merge --abort`) y borrar ramas.

**Tiempo estimado: 60-90 min.**

## Requisitos previos

- [Git básico](02-git-basico.md): commits, `status`, `log`, `.gitignore`.

## Explicación

### ¿Qué es una rama?

Una rama (*branch*) es un **puntero móvil** a un commit. La rama principal (normalmente `main`) apunta
al último commit de esa línea. Cuando haces un commit nuevo, el puntero avanza.

```text
main → [C1]──[C2]──[C3]
                    ▲
                   HEAD (estás aquí)
```

**`HEAD`** es un puntero especial a **dónde estás ahora** (qué rama y qué commit). Cuando cambias de
rama, `HEAD` se mueve.

Crear una rama es **instantáneo**: Git solo crea un puntero nuevo, no copia ficheros. Por eso en Git
"ramificar es barato" y se recomienda crear ramas para casi todo.

```text
main → [C1]──[C2]──[C3]
                    │
feature →           └──[C4]──[C5]
                    ▲
                   HEAD (estás en 'feature')
```

### ¿Para qué sirven?

- **Aislar trabajo**: desarrollar algo sin tocar `main` (que debe estar siempre funcionando).
- **Colaborar**: cada persona trabaja en su rama y luego se fusiona.
- **Experimentar**: si sale mal, borras la rama y `main` sigue intacta.
- **Organizar por tema**: una rama por funcionalidad, por arreglo, por página.

Convenciones habituales de nombres: `feature/login`, `fix/error-404`, `docs/readme`.

### `switch` o `checkout`: ¿cuál uso?

| Comando | Qué hace hoy | Nota |
| --- | --- | --- |
| `git switch nombre` | Cambia de rama. | **Moderno** y claro. Úsalo para ramas. |
| `git switch -c nueva` | Crea y cambia. | `-c` = *create*. |
| `git checkout nombre` | Cambia de rama **o** restaura ficheros. | Antiguo y ambiguo: hace demasiadas cosas. |
| `git checkout -b nueva` | Crea y cambia (equivalente antiguo). | Verás mucho en tutoriales. |

En esta web usamos `git switch` para ramas y `git restore` para ficheros, que es lo recomendado desde
Git 2.23. `git checkout` sigue funcionando y lo encontrarás por todas partes.

### `merge`: fusionar ramas

`git merge` trae los cambios de otra rama a la rama en la que **estás** (¡importante: te mueves a la
rama destino y luego fusionas!). Hay dos casos:

**Fast-forward** ("avance rápido"): no hubo trabajo en `main` desde que creaste la rama, así que Git
solo adelanta el puntero. No se crea un commit nuevo.

```text
Antes:   main → [C1]──[C2]      feature → [C3]──[C4]
Después: main → [C1]──[C2]──[C3]──[C4]
```

**Three-way merge** (merge real): ambas ramas avanzaron, así que Git combina los cambios y crea un
**commit de merge** con dos "padres".

```text
Antes:    main → [C1]──[C2]──[C5]
          feature → [C1]──[C2]──[C3]──[C4]
Después:  main → [C1]──[C2]──[C5]──[M]
                     └────[C3]──[C4]──┘
```

### ¿Y los conflictos?

Un **conflicto** ocurre cuando Git **no puede decidir solo** qué cambio conservar: normalmente porque
**las dos ramas modificaron las mismas líneas** del mismo fichero de formas distintas.

Git entonces:

1. Detiene el merge a medias.
2. Marca las zonas conflictivas en el fichero con **marcadores de conflicto**.
3. Te pide que **tú decidas**.

No es un error ni un drama: es Git diciéndote "aquí hay que pensar".

Los marcadores tienen esta forma:

```text
<<<<<<< HEAD
lo que dice TU rama actual
=======
lo que dice la otra rama
>>>>>>> otra-rama
```

| Marca | Significa |
| --- | --- |
| `<<<<<<< HEAD` | Empieza tu versión (la rama en la que estás). |
| `=======` | Separador entre las dos versiones. |
| `>>>>>>> otra-rama` | Termina la versión de la otra rama. |

Resolver un conflicto es **editar el fichero** dejándolo como quieres (borrando los marcadores),
`git add` y `git commit`.

## Ejemplos prácticos

Vamos a provocar y resolver un conflicto **de verdad**, paso a paso. Trabaja en una carpeta de
prueba.

### Paso 0 · Preparar el repositorio

```bash
mkdir -p ~/lab-git && cd ~/lab-git
git init
printf 'linea comun\nlinea original\nlinea final\n' > app.txt
git add app.txt
git commit -m "Versión inicial de app.txt"
```

El fichero tiene tres líneas y estamos en `main`.

### Paso 1 · Crear una rama y cambiarla

```bash
git branch
git switch -c feature
git branch
```

```text
* main                        (salida de ejemplo)

  main
* feature
```

El `*` indica dónde estás. `git switch -c feature` crea la rama **y** te mueve a ella.

### Paso 2 · Cambiar el fichero en la rama `feature`

```bash
sed -i 's/linea original/linea cambiada en FEATURE/' app.txt
git add app.txt
git commit -m "Cambia la línea 2 en feature"
cat app.txt
```

```text
linea comun
linea cambiada en FEATURE
linea final
```

### Paso 3 · Volver a `main` y cambiar **la misma línea**

```bash
git switch main
sed -i 's/linea original/linea cambiada en MAIN/' app.txt
git add app.txt
git commit -m "Cambia la línea 2 en main"
cat app.txt
```

```text
linea comun
linea cambiada en MAIN
linea final
```

Ahora las dos ramas han modificado **la misma línea** de formas distintas. Ese es el escenario del
conflicto.

### Paso 4 · Intentar el merge (y chocar)

Recuerda: te mueves a la rama **destino** (`main`) y traes la otra (`feature`).

```bash
git merge feature
```

```text
Auto-merging app.txt
CONFLICT (content): Merge conflict in app.txt
Automatic merge failed; fix conflicts and then commit the result.
```

El merge queda **a medias**. Comprobamos el estado:

```bash
git status
```

```text
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   app.txt
```

### Paso 5 · Ver el conflicto en el fichero

```bash
cat app.txt
```

```text
linea comun
<<<<<<< HEAD
linea cambiada en MAIN
=======
linea cambiada en FEATURE
>>>>>>> feature
linea final
```

Ya ves los marcadores: arriba tu versión (`HEAD` = `main`), abajo la de `feature`.

### Paso 6 · Resolverlo

Editamos el fichero para dejarlo como queramos. Por ejemplo, combinamos las dos ideas:

```bash
printf 'linea comun\nlinea cambiada en MAIN y FEATURE\nlinea final\n' > app.txt
cat app.txt
```

```text
linea comun
linea cambiada en MAIN y FEATURE
linea final
```

Lo clave: han desaparecido **todos** los marcadores (`<<<<<<<`, `=======`, `>>>>>>>`).

!!! warning "No dejes marcadores"
    Si commiteas con los marcadores dentro, el conflicto queda mal resuelto y el fichero está roto.
    Revisa siempre que no quede ninguno: `grep -rn "<<<<<<<" .`

### Paso 7 · Marcar como resuelto y confirmar

```bash
git add app.txt
git status
git commit -m "Fusiona feature en main: combina cambios de la línea 2"
git log --oneline --graph
```

```text
*   9f1c2a3 (HEAD -> main) Fusiona feature en main: combina cambios de la línea 2
|\
| * 4d5e6f7 (feature) Cambia la línea 2 en feature
* | 8a9b0c1 Cambia la línea 2 en main
|/
* 123abcd Versión inicial de app.txt
```

El `git add` le dice a Git "esto ya está resuelto". El `git commit` cierra el merge. En el log se ve
el commit de merge con sus dos padres.

### Paso 8 · Si te arrepientes: abortar

En cualquier momento **antes** de confirmar, puedes cancelar el merge:

```bash
git merge --abort
```

Esto devuelve el repositorio al estado anterior al merge. Muy útil si el conflicto es enorme o te has
liado.

### Paso 9 · Borrar una rama ya fusionada

```bash
git branch -d feature
git branch
```

```text
* main
```

`-d` solo borra si la rama ya está fusionada (protección). Con `-D` fuerzas el borrado (cuidado:
puedes perder trabajo no fusionado).

### Ejemplo extra · Herramientas para ver ramas

```bash
git branch -a          # todas, incluidas las remotas
git log --oneline --graph --all
git diff main..feature # diferencias entre dos ramas
git switch -           # vuelve a la rama anterior
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "No me deja cambiar de rama" | Tienes cambios sin guardar que se pisarían. | Haz `commit` o `git stash` y vuelve a intentarlo. |
| Merge hecho en la rama equivocada | Fusionaste desde la rama destino. | Recuerda: **te mueves al destino** y luego `git merge origen`. |
| Se commiteó con marcadores de conflicto | No editaste el fichero. | Corrige el fichero, `git add` y `git commit --amend`. |
| `git merge` dejó todo "a medias" | Conflicto sin resolver. | Resuelve, `add` y `commit`; o `git merge --abort`. |
| `branch -d` no borra | La rama no está fusionada. | Revísalo; si estás seguro, `-D`. |
| Perdí trabajo de una rama borrada | Usaste `-D`. | Recuperable a veces con `git reflog` (tema avanzado). |
| `detached HEAD` | Hiciste checkout de un commit, no de una rama. | `git switch nombre-rama` para volver a una rama. |

## Ejercicios

1. Crea un repo, haz un commit inicial y crea una rama `saludo`. Añade un fichero, commitéalo y
   vuelve a `main`.
2. Fusiona `saludo` en `main` cuando no ha habido cambios en `main` (será *fast-forward*) y observa
   el log.
3. Provoca un conflicto: modifica **la misma línea** en `main` y en una rama, e intenta el merge.
4. Resuelve el conflicto combinando ambas versiones y confirma el merge.
5. Aborta un merge a medias con `git merge --abort` y comprueba que `main` vuelve a estar limpio.
6. *(Difícil)* Crea tres ramas (`a`, `b`, `c`) desde `main`, haz en cada una un commit que toque
   ficheros distintos, fusiónalas una a una en `main` y explica por qué **no** hay conflictos.

??? success "Solución"

    **1.**
    ```bash
    mkdir ~/lab-git2 && cd ~/lab-git2 && git init
    echo "hola" > base.txt && git add . && git commit -m "inicio"
    git switch -c saludo
    echo "buenas" > saludo.txt && git add . && git commit -m "añade saludo"
    git switch main
    ```

    **2.**
    ```bash
    git merge saludo
    git log --oneline
    ```
    Al no haber cambios en `main`, se produce un *fast-forward*: el puntero avanza; no hay commit de
    merge.

    **3.**
    ```bash
    git switch -c rama-x
    echo "version X" > comun.txt && git add . && git commit -m "comun en rama-x"
    git switch main
    echo "version main" > comun.txt && git add . && git commit -m "comun en main"
    git merge rama-x     # CONFLICTO
    ```

    **4.**
    ```bash
    printf 'version X y version main combinadas\n' > comun.txt
    git add comun.txt
    git commit -m "resuelve conflicto de comun.txt"
    ```

    **5.**
    ```bash
    # repite el 3 sin confirmar y luego:
    git merge --abort
    git status
    ```
    Verás "nothing to commit, working tree clean".

    **6.** No hay conflicto porque cada commit toca **ficheros distintos**: Git combina cambios de
    zonas diferentes sin problema. Los conflictos aparecen cuando se modifican **las mismas líneas**.

## Resumen

- Una **rama** es un puntero a un commit; crear y cambiar de rama es barato y rápido.
- **`HEAD`** indica dónde estás.
- Usa `git switch` (ramas) y `git restore` (ficheros); `git checkout` es la forma antigua.
- `git merge` se ejecuta **desde la rama destino**, trayendo la rama origen.
- **Fast-forward** (sin cambios en destino) vs **three-way** (crea commit de merge).
- Los **conflictos** aparecen al tocar las mismas líneas; se resuelven editando, `git add` y
  `git commit`.
- `git merge --abort` cancela un merge a medias; `git branch -d` borra ramas fusionadas.

## Checklist

- [ ] Sé qué es una rama y qué es `HEAD`.
- [ ] Creo, listo y cambio de rama con `branch` y `switch`.
- [ ] Entiendo fast-forward vs three-way merge.
- [ ] Sé por qué se produce un conflicto.
- [ ] He resuelto un conflicto paso a paso y confirmado el merge.
- [ ] Sé comprobar que no quedan marcadores (`grep "<<"`).
- [ ] Sé abortar un merge y borrar ramas.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Pro Git · Ramificaciones](https://git-scm.com/book/es/v2) | Capítulo de ramas (libro oficial) | **ES** | Gratis |
| [Documentación de Git](https://git-scm.com/doc) | Referencia de `merge`, `switch`, `branch` | EN | Gratis |
| [Learn Git Branching](https://learngitbranching.js.org) | Juego interactivo de ramas y merges | EN | Gratis |

## Siguiente paso

Ya sabes trabajar con ramas en local. Ahora, a colaborar en la nube:
**[04 · GitHub, forks y Pull Requests](04-github-forks-y-pull-requests.md)**.
