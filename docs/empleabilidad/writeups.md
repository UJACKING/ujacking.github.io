# Cómo hacer writeups

Un **writeup** es la documentación de cómo resolviste una máquina, un reto o un CTF. Bien hecho, es
una de las mejores pruebas de que **entiendes** lo que haces, no solo de que copiaste una solución.
Aquí tienes la estructura, una plantilla lista para usar y las buenas prácticas.

## Por qué escribir writeups

- **Demuestras comprensión.** Explicar es más difícil que ejecutar; si puedes explicarlo, sabes.
- **Te obliga a entender.** Escribir te destapa los huecos que aún no dominas.
- **Construye tu portfolio.** Se enlaza desde tu [GitHub como portfolio](github-como-portfolio.md).
- **Te prepara para entrevistas.** Repasar tus propios writeups es preparación técnica de primera.
- **Devuelves a la comunidad.** Ayudas a quien viene detrás (sin destripar, ver más abajo).

## Estructura recomendada

Un buen writeup sigue un orden narrativo: de "no sé nada" a "resuelto", explicando el **porqué** de
cada paso. Estructura sugerida:

1. **Ficha de la máquina.** Plataforma, nombre, dificultad, sistema operativo, fecha de resolución.
2. **Reconocimiento.** Qué herramientas usaste y qué información sacaste.
3. **Enumeración.** Puertos, servicios, web, usuarios, etc.
4. **Explotación / acceso inicial.** Cómo entraste y por qué funcionó.
5. **Escalada de privilegios.** Cómo pasaste de usuario normal a administrador/root.
6. **Flags / objetivo cumplido.** Sin destripar de más si la máquina sigue activa.
7. **Lecciones aprendidas.** Qué fallo de seguridad había y cómo se mitigaría.
8. **Mitigación.** Cómo se habría defendido ese sistema. **Esta sección diferencia a un buen writeup.**

!!! tip "Explica el porqué, no solo el comando"
    `nmap -sV` no dice nada. *"Uso `-sV` para identificar las versiones de los servicios y así buscar
    vulnerabilidades conocidas de esa versión en concreto"* sí. Un reclutador técnico lee esa frase.

## Plantilla completa en Markdown

Copia esta plantilla y rellénala. Los apartados entre corchetes son para personalizar.

````markdown
# [Plataforma] — [Nombre de la máquina]

## Ficha

| Campo | Valor |
| --- | --- |
| Plataforma | [HackTheBox / TryHackMe] |
| Dificultad | [Fácil / Media / Difícil] |
| Sistema | [Linux / Windows] |
| Fecha | [AAAA-MM-DD] |
| Categoría | [Linux / Web / Active Directory / ...] |

## Resumen

Dos o tres líneas con la idea general: qué servicio era vulnerable y por dónde se ganó acceso y
escalada. **Sin destripar flags ni textos de solución.**

## Reconocimiento

Qué herramientas usé y qué aprendí de la fase de reconocimiento.

```bash
# Comando de ejemplo (sustituir por el tuyo)
nmap -sV -sC -p- 10.10.10.10 -oN escaneo.txt
```

Comentario de los resultados **(salida de ejemplo)**:

```text
22/tcp  open  ssh     OpenSSH 8.2
80/tcp  open  http    Apache httpd 2.4.41
```

Qué significa cada hallazgo y por qué me fijo en él.

## Enumeración

Detalle de la enumeración de cada servicio relevante. Rutas, directorios, usuarios, versiones.

## Acceso inicial

Explico la vulnerabilidad, **por qué existe** y cómo la aproveché. Pego los comandos mínimos.

## Escalada de privilegios

Cómo pasé de usuario normal a root/administrador y **por qué** funcionó (permisos mal configurados,
sudo mal usado, servicio vulnerable, etc.).

## Flags / objetivo

`[REDACTADO]` si la máquina sigue activa, o el valor si la plataforma ya permite publicarlo.

## Lecciones aprendidas

- Qué falló en el sistema (en términos de configuración/seguridad).
- Qué técnicas nuevas he aprendido.
- Qué haría más rápido la próxima vez.

## Mitigación

Cómo un administrador habría evitado este ataque:

- [Recomendación 1: p. ej., no ejecutar servicios con usuario root.]
- [Recomendación 2: p. ej., aplicar principio de mínimo privilegio.]
- [Recomendación 3: p. ej., mantener software actualizado.]

## Referencias

Enlaces a documentación oficial (no a otros writeups que destripen la máquina).
````

## Buenas prácticas

- **No destripar sin contexto.** Antes de explicar la solución, describe el camino mental: qué
  probaste, qué falló y por qué llegaste a esa conclusión. La solución "de golpe" no enseña.
- **Explica el porqué.** Cada comando debería tener una línea de *para qué sirve*.
- **Separa las fases.** Reconocimiento, enumeración, explotación y escalada como apartados distintos.
- **Incluye mitigación.** Es lo que te distingue de quien solo pega comandos.
- **Comandos reproducibles.** Que otra persona pueda seguirlos, aunque sin las flags si están
  reservadas.
- **Redacta en español** (o en inglés si buscas mercado internacional), con corrección y sin copiar
  de otros writeups.
- **Enlaza la fuente oficial.** Si usaste una técnica de OWASP, Burp o PortSwigger, enlaza su
  documentación, no el blog de otro.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Verificar la política vigente de **cada plataforma** sobre publicar writeups de máquinas activas.
    Tanto HackTheBox como TryHackMe **cambian sus reglas con el tiempo**, así que NO se afirma aquí
    qué permite cada una. Antes de publicar un writeup:

    1. Consulta la sección de normas/reglas vigente en la propia plataforma
       ([hackthebox.com](https://www.hackthebox.com), [tryhackme.com](https://tryhackme.com)).
    2. Si permiten publicar, respeta lo que exijan (retraso temporal, ocultar flags, marcar spoilers).
    3. Si dudas, **no lo publiques** y márcatelo como pendiente.

    Quien mantenga esta página debe revisar periódicamente estas políticas y actualizar este aviso.

### Hacks sencillos para no destripar

- Empieza cada apartado con el **razonamiento**, no con la respuesta.
- Usa bloques plegables `??? note "Spoiler"` para ocultar el paso clave.
- Rellena la sección "Ficha" con "Resuelto tras la máquina retirarse" cuando corresponda.
- No copies el texto de la máquina ni las pistas exactas de la plataforma.

## Errores comunes al escribir writeups

| Error | Por qué es un problema | Cómo evitarlo |
| --- | --- | --- |
| Pegar la solución sin explicar | No demuestra comprensión | Cuenta el razonamiento de cada paso |
| Publicar máquina activa | Puede incumplir la política de la plataforma | Consulta las reglas vigentes |
| Meter capturas con datos reales | Filtra información de terceros | Anonimiza antes de subir |
| Copiar otro writeup | Plagio y perjudica a la plataforma | Escribe con tus palabras |
| Incluir código ofensivo contra sistemas reales | Problema legal/ético | Practica solo en laboratorio o plataformas autorizadas |

## Checklist del writeup

- [ ] Ficha completa (plataforma, dificultad, sistema, fecha).
- [ ] Reconocimiento, enumeración, explotación y escalada en apartados separados.
- [ ] Cada comando explicado con su para qué.
- [ ] Lecciones aprendidas y **mitigación** incluidas.
- [ ] Sin datos sensibles ni flags de máquinas activas.
- [ ] Política de la plataforma verificada antes de publicar.
- [ ] Enlazado desde mi repositorio de writeups (ver [GitHub como portfolio](github-como-portfolio.md)).

!!! note "Ética y legalidad"
    Documenta solo máquinas y retos de plataformas que **autorizan** su publicación, tu propio
    laboratorio o sistemas para los que tengas permiso por escrito. Nunca ataques sistemas reales.

## Para ir más allá

| Recurso | Tipo | Idioma | Coste |
| --- | --- | --- | --- |
| [hackthebox.com](https://www.hackthebox.com) | Plataforma de máquinas | EN | Freemium |
| [tryhackme.com](https://tryhackme.com) | Plataforma de salas guiadas | EN | Freemium |
| [PortSwigger Web Security Academy](https://portswigger.net/web-security) | Laboratorios web | EN | Gratis |
| [Dónde practicar](../nivel-1-principiante/06-donde-practicar/index.md) | Contenido interno | ES | Gratis |
| [Máquinas objetivo](../nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md) | Contenido interno | ES | Gratis |

## Siguiente paso

Plasma tu experiencia en papel: **[CV de ciberseguridad](cv-de-ciberseguridad.md)**.
