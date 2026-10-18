# 05 · GitHub Pages y perfil

**GitHub no solo guarda código: también publica webs gratis y te sirve de escaparate profesional.**
En esta página aprendes qué es GitHub Pages, cómo se publica una web estática y, en concreto, **cómo
se publica la web que estás leyendo**. Terminamos con cómo construir un perfil de GitHub que cause
buena impresión a quien te vaya a contratar.

## Objetivos de aprendizaje

Al terminar esta página sabrás:

- Explicar qué es **GitHub Pages** y para qué sirve.
- Conocer las formas de publicar un sitio (rama + carpeta, o GitHub Actions).
- Entender **cómo se despliega esta web** (MkDocs + Actions + Pages).
- Levantar una copia local de la web con `mkdocs serve`.
- Crear un **README de perfil** y **fijar repositorios**.
- Montar un perfil de GitHub con aspecto profesional.

**Tiempo estimado: 60-90 min.**

## Requisitos previos

- [GitHub, forks y Pull Requests](04-github-forks-y-pull-requests.md).
- Nociones de Markdown (página anterior).

## Explicación

### ¿Qué es GitHub Pages?

**GitHub Pages** es un servicio de **alojamiento de webs estáticas** gratuito, directamente desde un
repositorio. Publica ficheros HTML, CSS, JavaScript y markdown ya convertido: lo que no puede hacer
es ejecutar código en el servidor (no hay PHP, ni bases de datos, ni backend).

Una **web estática** es una web hecha de ficheros que se sirven tal cual. Justo lo que es esta web:
MkDocs convierte los `.md` en HTML y GitHub Pages los sirve.

URL típica (según el tipo de repo):

| Tipo de repositorio | URL del sitio |
| --- | --- |
| `usuario.github.io` | `https://usuario.github.io` |
| Cualquier otro repo | `https://usuario.github.io/nombre-repo` |
| Dominio propio | `https://tu-dominio.com` (configurando CNAME) |

**Ventajas:** gratis, HTTPS incluido, actualización automática con cada `push`.
**Límites:** solo contenido estático; para webs dinámicas hace falta otro hosting.

### Cómo se publica un sitio con GitHub Pages

Hay dos caminos habituales:

**A) Publicar desde una rama y una carpeta.**
En *Settings → Pages → Build and deployment → Source* eliges la rama (`main`) y la carpeta (`/` o
`/docs`). GitHub sirve el contenido de ahí tal cual.

**B) Publicar con GitHub Actions (recomendado para webs generadas).**
Un *workflow* construye el sitio (por ejemplo, ejecuta MkDocs) y publica el resultado. Es lo que
usamos aquí, porque la web se **genera** a partir de Markdown: no se sirve el `.md` directamente.

```text
   push a main
       │
       ▼
 ┌─────────────┐     ┌──────────────┐     ┌───────────────┐
 │ GitHub      │ ──► │ mkdocs build │ ──► │ Actions       │
 │ Actions     │     │ --strict     │     │ deploy-pages  │
 └─────────────┘     └──────────────┘     └───────┬───────┘
                                                  ▼
                                         https://ujacking.github.io/
```

!!! note "¿Qué es un workflow de Actions?"
    Un fichero YAML en `.github/workflows/` que describe qué hacer cuando ocurre algo (un `push`, un
    Pull Request, una hora concreta…). GitHub ejecuta esos pasos en la nube, gratis para repos
    públicos.

### Cómo se publica ESTA web

Esta web es **MkDocs + Material for MkDocs**. Todo el contenido son ficheros Markdown en la carpeta
`docs/`, y `mkdocs.yml` define la estructura (el menú `nav`), el tema y los plugins.

| Pieza | Dónde vive | Para qué |
| --- | --- | --- |
| Contenido | `docs/` (ficheros `.md`) | Las páginas que lees. |
| Configuración | `mkdocs.yml` | Menú, tema, extensiones. |
| Dependencias | `requirements.txt` | Versiones de MkDocs y Material. |
| Despliegue | `.github/workflows/deploy.yml` | Construye y publica en Pages. |
| Comprobación de PR | `.github/workflows/pr-check.yml` | Verifica la build estricta. |
| Comprobación de enlaces | `.github/workflows/links.yml` | Revisa enlaces periódicamente. |

El **despliegue** ocurre así: al hacer *merge* en `main`, el workflow `deploy.yml` se dispara,
instala las dependencias, ejecuta **`mkdocs build --strict`** (modo estricto: cualquier error, aviso o
enlace interno roto **hace fallar la build**), sube el resultado como artefacto y lo publica en Pages.

!!! danger "Enlaces internos roto = build rota"
    Como la build es `--strict`, si enlazas a una página que **no existe**, el despliegue falla. Por
    eso hay que ser muy cuidadoso con los enlaces relativos entre páginas. Es la regla de oro de
    contribuir a esta web.

### Ejecutar la web en local

Antes de proponer un cambio, pruébalo en tu máquina:

```bash
git clone https://github.com/UJACKING/ujacking.github.io.git
cd ujacking.github.io
python3 -m venv .venv
source .venv/bin/activate        # En Windows: .venv\Scripts\activate
pip install -r requirements.txt
mkdocs serve
```

Abre <http://127.0.0.1:8000/>. El navegador **se recarga solo** al guardar un cambio. Antes de subir
nada, comprueba la build estricta:

```bash
mkdocs build --strict
```

Si ese comando termina sin errores, tu cambio pasará el control automático del Pull Request.

### Tu perfil de GitHub como portfolio

Tu perfil (`https://github.com/tu-usuario`) es tu **tarjeta de presentación** técnica. En
ciberseguridad se mira mucho: repositorios, READMEs y constancia.

**1. El README de perfil.**
Si creas un repositorio **con el mismo nombre que tu usuario** (por ejemplo `ana/ana`) y dentro pones
un `README.md`, ese README **se muestra en la parte superior de tu perfil**. Es tu escaparate.

**2. Fija repositorios (pinned).**
En tu perfil puedes **fijar hasta seis repositorios** para que se vean destacados. Elige los mejores,
no los más numerosos.

**3. Repositorios que suman.**
Cada repo debería tener:

- Nombre claro (en minúsculas, con guiones).
- Un **`README.md`** que explique qué es, cómo se usa y una captura o ejemplo.
- Una **licencia** (por ejemplo MIT) si el código es libre.
- **Topics** (etiquetas) para que se encuentre.
- Commits con mensajes decentes.

**4. Constancia.**
El gráfico de contribuciones (los cuadraditos verdes) muestra actividad. No hace falta rellenarlo
artificialmente: publicar tus writeups y scripts de práctica con regularidad es suficiente.

**5. Aprovecha Pages.**
Puedes publicar con GitHub Pages una web personal o un blog de writeups y enlazarla en tu perfil.

## Ejemplos prácticos

### Ejemplo 1 · Un `README` de perfil sencillo

Crea el repositorio `tu-usuario` y dentro este `README.md`:

```markdown
# Hola, soy Ana 👋

Estudiante de ingeniería y apasionada de la **ciberseguridad ofensiva**.

- 🔭 Ahora aprendiendo: pentesting de infraestructura.
- 🌱 Practicando en TryHackMe y Hack The Box.
- 📝 Escribo writeups en mi [blog](https://tu-usuario.github.io/).

## Herramientas
![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black)
![Bash](https://img.shields.io/badge/Bash-4EAA25?logo=gnubash&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)

## Contacto
- LinkedIn: [tu-perfil](https://www.linkedin.com)
```

!!! warning "Shields e imágenes externas"
    Los *badges* de shields.io cargan imágenes externas. En **esta web** no usamos hotlinks de
    imágenes (ver la guía de contenido); pero en tu perfil personal sí puedes usarlos. Si fallan, el
    README seguirá funcionando sin el icono.

### Ejemplo 2 · Un repositorio de scripts bien presentado

```text
mis-scripts/
├── README.md
├── LICENSE
├── bin/
│   ├── backup.sh
│   └── ping-sweep.sh
└── docs/
    └── ejemplos.md
```

Un `README.md` que explique el propósito y muestre un ejemplo de uso hará que el repo parezca serio
aunque sean diez líneas de Bash.

### Ejemplo 3 · Publicar una web personal con Pages

1. Crea un repositorio llamado `tu-usuario.github.io`.
2. Añade un `index.html` (o genera el sitio con MkDocs/Jekyll).
3. En *Settings → Pages*, elige la rama `main` y la carpeta raíz.
4. En unos minutos, `https://tu-usuario.github.io` estará online.

### Ejemplo 4 · Comprobar tu build antes de subir

```bash
mkdocs build --strict
```

```text
INFO    -  Building documentation...
INFO    -  Documentation built in 1.23 seconds   (salida de ejemplo)
```

Si aparece un `WARNING` o un `ERROR`, **corrígelo** antes de hacer el Pull Request. Los avisos de
enlaces internos roto son los más frecuentes.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| La build falla en el PR | `mkdocs build --strict` encontró un error o aviso. | Lee el mensaje, casi siempre es un enlace interno roto. |
| La web no se actualiza | No se hizo *merge* en `main`, o el workflow falló. | Revisa la pestaña **Actions** del repositorio. |
| `mkdocs: command not found` | No activaste el entorno virtual. | `source .venv/bin/activate` antes de `mkdocs`. |
| El README de perfil no aparece | El repo no tiene **exactamente** el nombre de tu usuario. | Renómbralo. |
| El sitio da 404 | Pages no está activado o la carpeta/rama es incorrecta. | Revisa *Settings → Pages*. |
| Páginas 404 dentro del sitio | Nombres de fichero/enlace mal escritos. | Reproduce en local con `mkdocs serve`. |
| Perfil con repos vacíos | Repos sin README ni commits útiles. | Rellénalos o elimínalos; fija los buenos. |

## Ejercicios

1. Crea un repositorio `tu-usuario` con un `README.md` de perfil y comprueba que aparece en tu
   perfil.
2. Fija (pin) tus tres mejores repositorios.
3. Mejora el `README.md` de uno de tus repositorios añadiendo instalación, uso y licencia.
4. Clona esta web, ejecútala con `mkdocs serve` y localiza un enlace interno para ver cómo está
   escrito.
5. Ejecuta `mkdocs build --strict` y comprueba que termina sin errores.
6. *(Difícil)* Publica una web estática propia con GitHub Pages (aunque sea un `index.html`
   mínimo) y enlázala en tu README de perfil.

??? success "Solución"

    **1.** GitHub → *New repository* → nombre igual a tu usuario → público → añade `README.md`. Al
    guardar, tu perfil mostrará ese README arriba.

    **2.** En tu perfil, botón **Customize your pins** → selecciona hasta seis repos → *Save pins*.

    **3.**
    ```markdown
    # nombre-repo

    Qué hace el proyecto en una frase.

    ## Instalación
        git clone https://github.com/tu-usuario/nombre-repo.git

    ## Uso
        ./script.sh --ayuda

    ## Licencia
    MIT
    ```

    **4.**
    ```bash
    git clone https://github.com/UJACKING/ujacking.github.io.git
    cd ujacking.github.io
    mkdocs serve
    ```
    Un enlace interno se escribe como ruta relativa al `.md`, por ejemplo
    `[Chuleta](04-bash/05-chuleta-bash.md)` desde la portada.

    **5.**
    ```bash
    mkdocs build --strict
    ```
    Debe terminar con `Documentation built in ... seconds` y sin `WARNING`/`ERROR`.

    **6.** Crea `tu-usuario.github.io`, pon un `index.html` mínimo, actívalo en *Settings → Pages* y
    enlázalo desde tu README de perfil:
    ```markdown
    🌐 [Mi web](https://tu-usuario.github.io/)
    ```

## Resumen

- **GitHub Pages** publica webs **estáticas** gratis desde un repositorio.
- Se puede publicar desde una rama/carpeta o con **GitHub Actions** (lo segundo, para sitios
  generados).
- Esta web es **MkDocs + Material**; se despliega con `deploy.yml` al hacer merge en `main`, usando
  `mkdocs build --strict`.
- Prueba en local con `mkdocs serve` y verifica con `mkdocs build --strict` antes de un PR.
- Tu **perfil** es tu portfolio: README de perfil, repos fijados, buenos READMEs, licencias y
  constancia.
- Los **enlaces internos roto rompen la build**: cuídalos.

## Checklist

- [ ] Sé qué es GitHub Pages y para qué sirve.
- [ ] Entiendo las dos formas de publicar un sitio.
- [ ] Sé cómo se despliega esta web (Actions + MkDocs).
- [ ] He ejecutado `mkdocs serve` y `mkdocs build --strict` en local.
- [ ] Tengo un README de perfil.
- [ ] He fijado mis mejores repositorios.
- [ ] Mis repositorios tienen README, licencia y topics.
- [ ] Sé que un enlace interno roto rompe la build.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [GitHub Pages (docs)](https://docs.github.com) | Documentación oficial de Pages | EN | Gratis |
| [MkDocs](https://www.mkdocs.org) | Generador de sitios estáticos | EN | Gratis |
| [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) | Tema que usa esta web | EN | Gratis |
| [GitHub Skills](https://skills.github.com) | Cursos interactivos, incluido Pages | EN | Gratis |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Falta una guía en **español** sobre cómo crear un portfolio de ciberseguridad en GitHub con
    enlace verificado, y una plantilla de README de perfil propia de UJACKING. Debe añadirlas un
    redactor.

## Siguiente paso

Has terminado el módulo de Git y GitHub. El siguiente es práctico y muy entretenido:
**[06 · Dónde practicar](../06-donde-practicar/index.md)**.
