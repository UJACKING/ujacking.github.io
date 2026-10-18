# CV de ciberseguridad

Un buen CV no es una lista de todo lo que has hecho: es un **documento de venta** que en 10 segundos
deja claro qué sabes y por qué encajas. Aquí tienes la estructura, cómo pasar los filtros automáticos
(ATS) y una plantilla lista para adaptar.

## Objetivo del CV

Solo tiene que conseguir una cosa: **que te llamen**. Para eso:

- Que se entienda **en una lectura rápida**.
- Que contenga las **palabras clave** de la oferta.
- Que no tenga nada que distraiga o genere dudas.

## Estructura recomendada

Orden pensado para que lo más importante aparezca arriba:

1. **Datos de contacto.** Nombre, ciudad/región, email profesional, teléfono, GitHub, LinkedIn.
2. **Perfil (2-3 líneas).** Quién eres, hacia qué área apuntas y qué aportas.
3. **Experiencia.** Trabajos previos, aunque no sean de ciberseguridad: destaca lo **transferible**.
4. **Proyectos.** Laboratorio propio, herramientas, CTFs, writeups. Clave si tienes poca experiencia.
5. **Formación.** Títulos y cursos relevantes.
6. **Certificaciones.** Las que tengas, y las "en curso" si están cerca de terminar (dilo claro).
7. **Skills (Habilidades).** Agrupadas por categorías, no en una nube suelta.

!!! tip "Una página basta si estás empezando"
    Con poca experiencia, una sola página. Reserva dos páginas solo cuando tengas muchos años de
    experiencia relevante.

## Cómo pasar los filtros ATS

Muchas empresas usan un **ATS** (*Applicant Tracking System*): un software que **lee y ordena CVs**
antes de que los vea un humano. Para no quedar descartado:

- **Formato simple.** Una sola columna, sin tablas complejas, sin cajas, sin gráficos de barras para
  "nivel de Python". El ATS no los interpreta.
- **Sin encabezados raros.** Usa `Experiencia`, `Formación`, `Certificaciones`, no imágenes con texto.
- **Palabras clave de la oferta.** Si piden "SIEM", "Wireshark", "Active Directory", escribe esos
  términos **exactos** donde corresponda y **con verdad**.
- **Fechas coherentes.** Formato constante (por ejemplo `03/2024 – 09/2024`) y sin huecos sin explicar.
- **Exporta a PDF** salvo que pidan otro formato. Antes, comprueba que **el texto se puede copiar**
  (si al seleccionarlo no se selecciona nada, es una imagen y el ATS no lo lee).
- **Nombre de archivo claro:** `CV-Nombre-Apellido-Ciberseguridad.pdf`.

!!! warning "No engañes al ATS mintiendo"
    Poner habilidades que no tienes es la vía rápida a que te pillen en la entrevista técnica. El ATS
    filtra, pero **una persona te entrevista después**.

## Qué poner con poca experiencia

Aquí está el truco: con poca o ninguna experiencia laboral en ciberseguridad, **los proyectos son tu
experiencia**. Rellena la sección de proyectos con:

- **Laboratorio propio.** Montar redes virtuales con [VirtualBox](https://www.virtualbox.org) o
  [VMware](https://www.vmware.com), máquinas vulnerables de [vulnhub.com](https://www.vulnhub.com).
- **Plataformas de práctica.** Máquinas resueltas en [hackthebox.com](https://www.hackthebox.com) o
  [tryhackme.com](https://tryhackme.com): pon estadísticas reales del perfil, no exageres.
- **CTFs.** Participaciones en [ctftime.org](https://ctftime.org) o [picoctf.org](https://picoctf.org).
- **Writeups.** Pero con enlaces a casos donde puedas publicarlos
  (ver [Cómo hacer writeups](writeups.md)).
- **Herramientas propias.** Scripts en Python o Bash publicados en tu
  [GitHub como portfolio](github-como-portfolio.md).
- **Trabajo previo no técnico.** El trato con clientes, la gestión de incidencias o el trabajo en
  equipo **también son habilidades transferibles** en SOC o soporte.

## Cómo escribir bullets que vendan

Regla práctica: cada *bullet* con **verbo de acción + qué hiciste + herramienta + resultado**.

=== "Ejemplos en español"

    - Automatiqué el análisis de logs de seguridad con **Python y expresiones regulares**,
      reduciendo el tiempo de revisión manual en una tarea repetitiva del laboratorio.
    - Documenté 15 máquinas de laboratorio en **writeups** publicados, practicando metodología de
      pentesting y escalada de privilegios en Linux.
    - Desplegué un **laboratorio virtual aislado** con máquinas vulnerables para practicar escaneo,
      explotación y hardening sin afectar a sistemas reales.
    - Analicé tráfico de red con **Wireshark** para identificar protocolos inseguros y proponer
      alternativas cifradas.
    - Configuré un **firewall** con reglas de mínimo privilegio en un entorno de prácticas, aplicando
      el principio de denegar por defecto.

=== "Ejemplos en inglés"

    - Automated security log analysis with **Python and regular expressions**, reducing manual
      review time on a repetitive lab task.
    - Documented 15 lab machines in public **writeups**, practising pentesting methodology and Linux
      privilege escalation.
    - Built an **isolated virtual lab** with vulnerable machines to practise scanning, exploitation
      and hardening without affecting real systems.
    - Analysed network traffic with **Wireshark** to identify insecure protocols and propose
      encrypted alternatives.
    - Configured a **firewall** with least-privilege rules in a practice environment, applying a
      deny-by-default policy.

!!! tip "En inglés, cuidado con el tono"
    Un CV en inglés refuerza si apuntas a multinacionales o remoto internacional. Mantén el **mismo**
    nivel de honestidad: lo que no has hecho, no lo escribas en ningún idioma.

## Plantilla en Markdown

Copia y adapta. **Nunca inventes** fechas, empresas ni certificaciones.

```markdown
# Nombre Apellido

Ciudad, España · correo@ejemplo.com · +34 600 000 000
GitHub: https://github.com/tuusuario · LinkedIn: https://linkedin.com/in/tuusuario

## Perfil

Estudiante/orientado a [área: pentesting web, Blue Team/SOC, ...]. Base en redes, Linux y
seguridad web, con laboratorio propio y proyectos publicados. Busco [puesto: prácticas / junior].

## Experiencia

**Puesto — Empresa** (MM/AAAA – MM/AAAA)
- Verbo de acción + qué hiciste + herramienta + resultado.
- Verbo de acción + qué hiciste + herramienta + resultado.

**Puesto no técnico — Empresa** (MM/AAAA – MM/AAAA)
- Destaca lo transferible (trato con cliente, trabajo en equipo, gestión de incidencias).

## Proyectos

**Laboratorio de pentesting personal** (AAAA)
- Monté un entorno virtual aislado con máquinas vulnerables para practicar escaneo y explotación.
- Documenté la metodología y los resultados en un repositorio público.

**Writeups de máquinas** (AAAA – actualidad)
- Resolví y documenté N máquinas, con sección de mitigación en cada una.

## Formación

**Título / Curso — Centro** (AAAA – AAAA)
- Contenido relevante para el puesto.

## Certificaciones

- [Certificación] — [año]  (o "en preparación, examen previsto MM/AAAA")
- [Certificación] — [año]

## Skills

- **Redes:** TCP/IP, DNS, HTTP, Wireshark, subnetting.
- **Sistemas:** Linux (usuarios, permisos, logs), Windows básico.
- **Seguridad ofensiva:** Nmap, Burp Suite, metodología de pentesting (laboratorio).
- **Defensiva:** análisis de logs, fundamentos de SIEM (si es cierto).
- **Otros:** Git/GitHub, Bash, Python básico.
```

## Errores que descartan CVs

| Error | Consecuencia |
| --- | --- |
| Word art, varias columnas, gráficos de barras | El ATS no lo lee |
| "Nivel de Python: 90%" | No significa nada; mejor un proyecto |
| Habilidades que no tienes | Te pillan en la entrevista |
| Faltas de ortografía | Sensación de dejadez |
| Datos de contacto erróneos o un PDF sin texto | No te pueden contactar / no se lee |
| Un CV distinto para cada oferta sin adaptarlo | Poca adecuación a la oferta |

## Checklist antes de enviar

- [ ] Una sola columna, texto seleccionable, exportado a PDF.
- [ ] Perfil de 2-3 líneas adaptado a la oferta.
- [ ] Palabras clave de la oferta presentes y **verificables**.
- [ ] Proyectos con enlaces que funcionan (GitHub, writeups).
- [ ] Fechas coherentes y sin huecos sin explicar.
- [ ] Revisado por otra persona (ortografía y claridad).
- [ ] Nombre de archivo profesional.

## Para ir más allá

| Recurso | Tipo | Idioma | Coste |
| --- | --- | --- | --- |
| [github.com](https://github.com) | Portfolio de proyectos | ES/EN | Gratis |
| [Módulo Git y GitHub](../nivel-1-principiante/05-git-y-github/index.md) | Contenido interno | ES | Gratis |
| [Paths por área](../paths/index.md) | Salidas laborales por especialidad | ES | Gratis |

## Siguiente paso

Que te **encuentren** a ti: **[Perfil de LinkedIn](perfil-de-linkedin.md)**.
