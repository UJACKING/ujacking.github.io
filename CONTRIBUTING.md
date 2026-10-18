# Cómo contribuir a la web de UJACKING

¡Gracias por querer aportar! Esta web crece con las contribuciones de la comunidad. Aquí tienes
todo lo necesario para hacerlo bien.

Antes de nada, lee el [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).

## Requisitos para contribuir

- Git instalado y una cuenta de GitHub.
- Python 3.10+ para poder construir la web en local.

## Flujo de trabajo (fork → rama → PR)

1. **Haz un fork** del repositorio `UJACKING/ujacking.github.io` (botón *Fork*).
2. **Clona tu fork** y añade el remoto original:

   ```bash
   git clone https://github.com/TU_USUARIO/ujacking.github.io.git
   cd ujacking.github.io
   git remote add upstream https://github.com/UJACKING/ujacking.github.io.git
   ```

3. **Crea una rama** con un nombre descriptivo:

   ```bash
   git switch -c docs/subnetting-ejercicios
   ```

4. **Edita** los ficheros Markdown dentro de `docs/`. Puedes previsualizar con `mkdocs serve`.
5. **Commit** siguiendo la convención (abajo).
6. **Push** a tu fork y abre un **Pull Request** hacia `UJACKING:main`.

## Convención de commits

Formato `tipo: descripción` (en español, imperativo, sin punto final):

| Tipo       | Para qué sirve                                        |
| ---------- | ----------------------------------------------------- |
| `feat`     | Añadir contenido o funcionalidad nueva                |
| `docs`     | Correcciones, mejoras o reestructuración de texto     |
| `fix`      | Corregir un error (comando, enlace, dato)             |
| `chore`    | Tareas de mantenimiento (dependencias, configuración) |
| `ci`       | Cambios en workflows de GitHub Actions                |
| `style`    | Formato, CSS, sin cambiar el significado del contenido|

Ejemplos:

```text
docs: ampliar la tabla de protocolos de aplicación
fix: corregir la máscara del ejemplo 3 de subnetting
feat: nueva página de Paths sobre Cloud security
```

## Guía de estilo

- **Idioma:** español de España. Tono cercano pero profesional, sin relleno.
- **Términos técnicos en inglés:** mantenlos (por ejemplo *switch*, *firewall*, *payload*), pero
  explícalos la primera vez que aparezcan.
- **Frases cortas.** Prefiere listas y tablas a párrafos largos.
- **Cero invenciones.** Si no estás seguro de un dato (versión, precio, fecha, artículo de ley),
  no lo afirmes: usa un PENDIENTE (ver abajo).
- **Enlaces:** no inventes URLs profundas. Si no puedes verificar un enlace, enlaza al dominio raíz
  y deja constancia. Marca los recursos como **Gratis**, **Freemium** o **De pago**, e indica el
  idioma con `(EN)` cuando sea en inglés.
- **Sin copiar:** nada de texto pegado de otras webs o cursos. Explica con tus palabras y cita la
  fuente como enlace.
- **Comandos:** pruébalos antes. Si no has podido ejecutarlos, escribe la salida como
  "(salida de ejemplo)" y dilo claramente.

## Plantilla obligatoria de las páginas de Nivel 1

Toda página de contenido del Nivel 1 debe incluir, **en este orden**:

1. **Título y resumen** (2-3 líneas).
2. **Objetivos de aprendizaje** (lista) y **tiempo estimado**.
3. **Requisitos previos** (con enlaces a las páginas anteriores).
4. **Explicación** progresiva (con analogías, tablas y diagramas Mermaid o ASCII).
5. **Ejemplos prácticos** con comandos copiables y su salida explicada.
6. **Errores comunes y cómo solucionarlos.**
7. **Ejercicios** (mínimo 5, de dificultad creciente) con soluciones en bloques
   `??? success "Solución"`.
8. **Resumen** en viñetas y **checklist** con casillas `- [ ]`.
9. **Para ir más allá:** recursos gratuitos etiquetados (tipo, idioma, gratis/freemium).
10. **Siguiente paso** con enlace.

Al final de cada página ofensiva, añade un recordatorio breve de uso ético.

## Cómo proponer un recurso

Usa la plantilla de issue **Proponer un recurso**. Indica:

- Nombre y URL (dominio raíz preferiblemente).
- Tipo: vídeo, curso, laboratorio, lectura, herramienta.
- Idioma.
- Precio: Gratis / Freemium / De pago.
- Para qué nivel y tema sirve.

## Cómo marcar un PENDIENTE

Todo dato que falte o esté sin verificar se marca así, para poder localizarlo con `grep`:

```markdown
!!! warning "PENDIENTE (TODO-UJACKING)"
    Descripción clara de qué falta y quién debe rellenarlo.
```

En líneas sueltas usa el marcador `TODO-UJACKING:` seguido de la descripción.

Antes de abrir un PR, comprueba que el marcador está bien escrito: `grep -rn "TODO-UJACKING" docs/`.

## Checklist antes de abrir la PR

- [ ] He ejecutado `mkdocs build --strict` en local y **no hay warnings**.
- [ ] Los enlaces internos funcionan y los externos están verificados o marcados.
- [ ] No hay contenido copiado de otras fuentes.
- [ ] No hay secretos: ni tokens, ni contraseñas, ni claves (`git grep -nEi "ghp_|github_pat_|password"`).
- [ ] Los PENDIENTES están marcados con el formato correcto.
- [ ] He respetado la plantilla de la página (si es Nivel 1).
- [ ] El commit sigue la convención `tipo: descripción`.

## Ejecutar la build en local

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs build --strict     # debe terminar sin warnings ni errores
```

!!! note
    `--strict` convierte cualquier *warning* de MkDocs en error. Es lo mismo que ejecuta el CI, así
    que si pasa en local, pasa en GitHub.
