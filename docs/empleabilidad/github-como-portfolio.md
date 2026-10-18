# GitHub como portfolio

Tu perfil de GitHub puede ser tu mejor carta de presentación en ciberseguridad: es **prueba pública
de que haces cosas**. En esta guía aprendes a organizar tus repos, escribir READMEs que se entiendan,
y —igual de importante— a **no publicar lo que no debes**.

!!! info "Antes de empezar"
    Si aún no sabes usar Git ni GitHub, empieza por el módulo
    [Git y GitHub](../nivel-1-principiante/05-git-y-github/index.md). Aquí damos por hecho que sabes
    crear un repositorio, hacer `commit` y subirlo, y abrir un *pull request*
    ([forks y pull requests](../nivel-1-principiante/05-git-y-github/04-github-forks-y-pull-requests.md)).

## Por qué GitHub cuenta (y mucho)

Un reclutador técnico no tiene tiempo de creerte por lo que dices: mira lo que **puede comprobar**.
Un GitHub bien cuidado transmite en segundos:

- Que **sabes trabajar** con control de versiones (herramienta obligatoria en cualquier equipo).
- Que tus proyectos **existen y funcionan** (código, documentación, capturas).
- Que **explicas** lo que haces (esto vale casi más que el propio código).
- Que tienes **constancia** (commits repartidos en meses, no todos de un fin de semana).

## Qué hace un buen perfil

1. **Foto, nombre real y bio.** Una frase clara: qué haces y qué buscas. Ejemplo:
   *"Estudiante de ciberseguridad · Pentesting web y Blue Team · buscando prácticas"*.
2. **Repos fijados (pinned).** GitHub te deja fijar hasta 6 repos en la parte superior del perfil.
   Fija solo los mejores. Mejor 3 buenos que 6 mediocres.
3. **Un repo de perfil personal.** Puedes crear un repositorio que se llame **igual que tu usuario**
   (`tuusuario/tuusuario`): su `README.md` se muestra como portada de tu perfil. Úsalo para una bio
   más larga con enlaces a tus writeups y a tu LinkedIn.
4. **Actividad razonable.** El gráfico de contribuciones se ve. No hace falta rellenarlo a diario,
   pero sí mostrar trabajo continuo.

## Estructura de un buen repositorio

Un repositorio ordenado tiene, como mínimo:

```text
mi-proyecto/
├── README.md            # lo primero que se lee
├── LICENSE              # licencia del código
├── .gitignore           # qué NO subir (¡clave!)
├── docs/                # documentación e imágenes
│   └── capturas/
├── src/                 # código fuente
└── requirements.txt     # dependencias (ejemplo Python)
```

Reglas prácticas:

- **README.md obligatorio.** Un repo sin README parece abandonado.
- **`.gitignore` desde el primer commit.** Evita subir basura (entornos virtuales, ficheros locales).
- **Nombres claros y en minúsculas con guiones:** `escaneo-puertos-python`, no `Proyecto1_ final v2`.
- **Commit messages útiles:** `añade validación de argumentos`, no `arreglos`.

## Qué hace un buen README

Un README responde rápido a: *¿qué es esto, para qué sirve, cómo lo pruebo y qué has aprendido?*.
Orden recomendado:

```markdown
# Nombre del proyecto

Una frase que explique qué es y para qué sirve.

## Descripción
Qué problema resuelve y por qué lo hiciste.

## Características
- Qué hace (en viñetas).

## Capturas
Imágenes o GIF del proyecto funcionando.

## Instalación
Pasos exactos y copiables.

## Uso
Ejemplo real de ejecución y su salida.

## Aprendizajes
Qué has aprendido construyéndolo (esto lo leen mucho los reclutadores).

## Limitaciones y trabajo futuro
Sé honesto: qué falta o qué mejorarías.

## Licencia
Tipo de licencia y enlace al fichero LICENSE.
```

!!! tip "El README es tu texto, el código es tu prueba"
    No tengas miedo de explicar con detalle. Un README largo y claro suele impresionar más que
    cuatrocientas líneas de código sin contexto.

### Ejemplo de sección de "Uso" bien hecha

````markdown
## Uso

Ejecuta el escáner sobre una IP de **tu propio laboratorio**:

```bash
python3 escaner.py --host 192.168.56.10 --puertos 22,80,443
```

Salida de ejemplo:

```text
192.168.56.10:22   abierto   (SSH)
192.168.56.10:80   abierto   (HTTP)
192.168.56.10:443  cerrado
```
````

## Capturas y evidencias

Las capturas hacen que tu trabajo sea creíble. Recomendaciones:

- Usa imágenes **propias** (nunca con hotlink a webs externas).
- Guárdalas en una carpeta `docs/capturas/` dentro del repo y enlázalas con rutas relativas.
- Difumina o tapa **cualquier dato sensible** antes de subirlas (IPs reales, nombres de clientes,
  tokens, correos).
- Para terminales, copiar el texto en un bloque de código suele leerse mejor que una captura.

## Licencias

Si compartes código, di bajo qué condiciones. Sin licencia, por defecto **nadie tiene permiso legal
para reutilizarlo**. Las más habituales en proyectos abiertos:

| Licencia | Resumen | Cuándo usarla |
| --- | --- | --- |
| MIT | Muy permisiva, solo pide mantener el aviso de copyright. | Quieres que reutilicen tu código libremente. |
| Apache 2.0 | Permisiva y añade una cesión explícita de patentes. | Proyectos que quieres que empresas adopten. |
| GPL | Copyleft: quien lo use debe publicar también su versión. | Quieres que las mejoras sigan siendo abiertas. |

GitHub te permite **añadir una licencia con un clic** al crear el repositorio. Si no sabes cuál
elegir, MIT es una elección segura y muy extendida.

!!! warning "No copies código ajeno sin licencia"
    Reutilizar código de otro repo sin respetar su licencia puede ser una infracción de derechos de
    autor. Cita siempre la fuente y respeta sus condiciones.

## Repos fijados: elige como si fuera un escaparate

Los repos fijados aparecen arriba, sin scroll. Elige según el objetivo del puesto:

- **Quieres pentesting:** fija tus writeups, una herramienta propia y un CTF destacado.
- **Quieres Blue Team/SOC:** fija un análisis de logs, un informe de incidente simulado, un script de
  automatización de alertas.
- **Quieres desarrollo seguro:** fija un proyecto donde apliques validación de entradas, gestión de
  secretos y buenas prácticas.

## Lo que NO se debe publicar

Esta sección es la más importante de la página. **Un error aquí puede costarte una oferta o meterte
en un problema legal.**

!!! danger "Nunca subas esto a un repositorio público"

    **1. Credenciales y secretos**

    - Contraseñas, claves SSH, tokens de API, claves de AWS/GCP/Azure.
    - Ficheros `.env`, `id_rsa`, `credentials`, `*.pem`, `*.key`.
    - Usa siempre un `.gitignore` y variables de entorno. Si subes un secreto por error, **no basta
      con borrarlo**: queda en el historial. Rótalo (cámbialo) de inmediato.

    **2. Datos personales y de terceros**

    - Datos de clientes, compañeros, alumnos o cualquier persona real.
    - Capturas con nombres completos, DNIs, correos, teléfonos o direcciones.
    - Informes de pentest reales sin autorización explícita y sin anonimizar.

    **3. Writeups prohibidos por la plataforma**

    - Algunas plataformas restringen publicar soluciones de **máquinas o retos activos**.
    - Consulta siempre la política vigente de la plataforma antes de publicar
      (ver [Cómo hacer writeups](writeups.md)).

    **4. Malware o exploits peligrosos**

    - Código ofensivo funcional apuntando a sistemas reales, sin contexto ni fines educativos.
    - Nada de *malware* real. Si investigas, aísla y documenta, no publiques muestras operativas.

    **5. Información interna que no te pertenece**

    - Código de tu empresa, configuraciones, topologías de red o procedimientos internos.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Añadir aquí la política interna de la asociación respecto a qué se puede publicar de actividades,
    máquinas y retos organizados por UJACKING, y quién autoriza su publicación.

### Cómo protegerte antes de cada `git push`

- [ ] He revisado que no hay contraseñas ni tokens (`grep -ri "password\|token\|secret" .`).
- [ ] El `.gitignore` cubre entornos virtuales, `.env`, `*.key`, `*.pem`.
- [ ] No hay datos de personas reales en capturas ni en texto.
- [ ] No publico writeups de máquinas activas prohibidas por la plataforma.
- [ ] Tengo derecho a publicar lo que subo.

## Checklist final del portfolio

- [ ] Foto, nombre y bio claro en el perfil.
- [ ] Entre 3 y 6 repos fijados que representan lo mejor que sé hacer.
- [ ] Cada repo fijado tiene README completo y capturas.
- [ ] Cada repo con código tiene `LICENSE` y `.gitignore`.
- [ ] Ningún secreto ni dato personal en el historial.
- [ ] El README de perfil (`tuusuario/tuusuario`) enlaza a mis writeups y LinkedIn.

## Para ir más allá

| Recurso | Tipo | Idioma | Coste |
| --- | --- | --- | --- |
| [github.com](https://github.com) | Plataforma | ES/EN | Gratis |
| [git-scm.com](https://git-scm.com) | Documentación oficial de Git | EN | Gratis |
| [Módulo Git y GitHub](../nivel-1-principiante/05-git-y-github/index.md) | Contenido interno | ES | Gratis |
| [GitHub Pages y perfil](../nivel-1-principiante/05-git-y-github/05-github-pages-y-perfil.md) | Contenido interno | ES | Gratis |

## Siguiente paso

Aprende a documentar tus máquinas: **[Cómo hacer writeups](writeups.md)**.
