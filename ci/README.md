# `ci/` — workflows listos para activar

Esta carpeta contiene los **workflows de GitHub Actions** de la web, en `ci/workflows/`.

## ¿Por qué están aquí y no en `.github/workflows/`?

GitHub exige que el token (Personal Access Token) con el que se sube el repositorio tenga el
**scope `workflow`** para poder crear o modificar ficheros dentro de `.github/workflows/`. El token
usado en la construcción inicial **no tenía ese scope**, así que GitHub rechazó subir estos ficheros
a su ubicación definitiva.

Para no perderlos, se dejaron versionados en `ci/workflows/`. **No se ejecutan desde aquí**: GitHub
solo ejecuta workflows que estén en `.github/workflows/`.

## Cómo activarlos (elige una opción)

### Opción A — Con un token que tenga el scope `workflow` (recomendado)

```bash
mkdir -p .github/workflows
git mv ci/workflows/deploy.yml        .github/workflows/deploy.yml
git mv ci/workflows/pr-check.yml      .github/workflows/pr-check.yml
git mv ci/workflows/links.yml         .github/workflows/links.yml
git rm -r ci   # ya no hace falta la carpeta
git commit -m "ci: mover workflows a .github/workflows"
git push
```

### Opción B — Desde la web de GitHub

1. Entra en **Add file → Create new file**.
2. En el nombre escribe `.github/workflows/deploy.yml` (la barra crea la carpeta).
3. Copia y pega el contenido de `ci/workflows/deploy.yml`.
4. Repite con `pr-check.yml` y `links.yml`.

## Y después: activar GitHub Pages con Actions

Cuando los workflows estén en su sitio:

1. Repo → **Settings → Pages**.
2. En **Source**, elige **GitHub Actions**.
3. Haz un push a `main` (o lanza el workflow *Deploy* a mano) y comprueba que termina en verde.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Mientras los workflows no estén activos, la web se publica con el método alternativo
    (rama `gh-pages`). Cuando se pase a GitHub Actions, hay que **cambiar la fuente de Pages a
    "GitHub Actions"** y se puede dejar de usar la rama `gh-pages`.
