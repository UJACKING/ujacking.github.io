# Entrevistas

La entrevista deja de medir lo que sabes y pasa a medir **cómo lo comunicas**. Esta página te prepara
las fases típicas, las preguntas más frecuentes por área (con respuestas modelo), las de
comportamiento y las pruebas técnicas.

!!! info "Aviso importante"
    **No existen dos procesos iguales.** Cada empresa diseña el suyo: el orden y el número de fases
    cambian. Aquí describimos **patrones habituales** del sector, no el proceso de ninguna empresa
    concreta. Ante la duda, pregunta a la persona que te cita qué esperar.

## Fases típicas (patrón general)

Aunque varía, es común encontrar:

1. **Filtro inicial.** RRHH o reclutador técnico. Comprueba encaje, disponibilidad y motivación.
2. **Entrevista técnica.** Fundamentos: redes, sistemas, seguridad. Puede ser con o sin código.
3. **Prueba práctica.** Reto, laboratorio, máquina o ejercicio guiado.
4. **Entrevista con el equipo.** Cultural y técnica, con quien sería tu compañero/a.
5. **Oferta y condiciones.**

!!! tip "Cada fase tiene el mismo objetivo"
    Demostrar tres cosas: que **sabes**, que **sabes explicarlo** y que **sería agradable trabajar
    contigo**.

## Preguntas técnicas por área

No se espera que lo sepas todo. Ante una pregunta que no domines: **razona en voz alta**. Cómo
piensas vale tanto como la respuesta.

### Fundamentos y redes

??? success "¿Qué pasa cuando escribes una URL en el navegador?"

    Se descompone en pasos lógicos:

    1. **Resolución DNS:** el nombre se traduce a una dirección IP.
    2. **Conexión TCP:** se establece una conexión al puerto correspondiente (80 o 443).
    3. **TLS** (si es HTTPS): se negocia el cifrado y se valida el certificado.
    4. **Petición HTTP:** el navegador pide el recurso.
    5. **Respuesta y renderizado:** llega el contenido y el navegador lo pinta.

    Idea clave: mencionar la **resolución de nombres** y el **apretón de manos TCP** demuestra que
    entiendes las capas.

??? success "Explica la diferencia entre TCP y UDP."

    **TCP** es orientado a conexión y fiable: confirma la entrega y reordena los datos (HTTP, SSH).
    **UDP** no garantiza entrega ni orden, es más ligero y rápido (DNS, vídeo, VoIP). Elige TCP cuando
    la integridad importa; UDP cuando la latencia es crítica.

??? success "¿Qué es una VPN y para qué sirve?"

    Un túnel cifrado entre dos puntos a través de una red no confiable. Sirve para **proteger el
    tráfico** (confidencialidad), **autenticar** al usuario y dar acceso remoto a una red interna.
    No hace que navegues "anónimo": solo mueve el punto donde termina el cifrado.

### Linux

??? success "¿Cómo ves qué procesos están escuchando en red?"

    Con `ss` (o su equivalente antiguo `netstat`): `ss -tulpn`. La `-t` muestra TCP, `-u` UDP, `-l`
    solo los que escuchan, `-p` el proceso y `-n` puertos numéricos. Saber interpretarlo es clave en
    cualquier análisis.

??? success "Un usuario puede ejecutar un comando como root. ¿Cómo lo investigas?"

    Reviso `sudo -l` para ver qué puede ejecutar y con qué permisos. Busco configuraciones
    peligrosas (binarios que permiten lanzar shell, tareas programadas, permisos SUID). Es un patrón
    clásico de escalada de privilegios en Linux; en un laboratorio propio se practica con máquinas
    vulnerables.

??? success "¿Para qué sirven los permisos en Linux y cómo se leen?"

    Controlan quién puede leer, escribir y ejecutar (`r`, `w`, `x`) sobre un fichero, para el dueño,
    el grupo y el resto. Se aplican con `chmod` y cambian de dueño con `chown`. El principio de
    **mínimo privilegio** recomienda dar solo los permisos necesarios.

### Seguridad web

??? success "¿Qué es un ataque XSS y cómo se mitiga?"

    *Cross-Site Scripting*: el atacante consigue que el navegador de la víctima ejecute código
    JavaScript malicioso, normalmente porque la aplicación refleja datos del usuario sin escaparlos.
    Se mitiga **escapando la salida según el contexto**, **validando la entrada**, aplicando una
    **Content Security Policy (CSP)** y usando `HttpOnly` en las cookies. Véase
    [OWASP](https://owasp.org).

??? success "¿Diferencia entre SQLi y XSS?"

    **SQL injection** ataca la base de datos: manipula una consulta SQL para leer o modificar datos.
    **XSS** ataca al usuario en el navegador: inyecta JavaScript en la página. Se mitigan de forma
    distinta: consultas parametrizadas (SQLi) y escapado/CSP (XSS).

??? success "¿Qué revisas primero al analizar una aplicación web?"

    El **flujo de autenticación**, después las **entradas de usuario** que se reflejan o se guardan, y
    la gestión de **sesiones y cookies**. Uso herramientas como
    [Burp Suite](https://portswigger.net) y laboratorios como la
    [Web Security Academy](https://portswigger.net/web-security).

### Blue Team / SOC

??? success "¿Cómo distingues un falso positivo de un incidente real?"

    Correlaciono varias fuentes: un pico de tráfico puede ser una tarea programada (falso positivo) o
    *exfiltración* si coincide con accesos raros, horarios extraños y destino externo. Se apoya en el
    **contexto** del activo y en la **línea base** del comportamiento normal.

??? success "¿Qué es un SIEM?"

    Un sistema que **recoge, normaliza y correlaciona** eventos de muchas fuentes (firewall, logs de
    sistema, endpoints) para generar alertas. Sirve de panel central para el analista, que usa
    *reglas* y *correlaciones* para detectar patrones.

??? success "¿Qué mirarías primero en un informe de alerta?"

    Los **cinco datos**: *qué* activo, *qué* usuario, *qué* evento, *cuándo* y *desde dónde*. Con eso
    decido si escalo el incidente, si necesito más evidencia o si lo cierro como falso positivo.

!!! note "Recuerda la ética"
    Cuando menciones técnicas ofensivas, deja claro que **solo se practican en laboratorio propio o
    plataformas autorizadas**. Un entrevistador valora mucho esa línea.

## Preguntas de comportamiento (método STAR)

Las preguntas de comportamiento empiezan por "Cuéntame una vez en la que…". Responde con **STAR**:

| Letra | Significado | Qué incluir |
| --- | --- | --- |
| **S** | Situation (Situación) | Contexto breve: cuándo y dónde. |
| **T** | Task (Tarea) | Qué tenías que lograr. |
| **A** | Action (Acción) | Qué hiciste **tú** (no "el equipo"). |
| **R** | Result (Resultado) | Qué se consiguió, con datos si puedes. |

Ejemplo de respuesta modelo:

> **Pregunta:** *"Cuéntame un problema difícil que resolvieras."*
>
> **S:** "En mi laboratorio monté una máquina vulnerable y el servicio no arrancaba."
> **T:** "Necesitaba entender por qué para poder practicar la escalada."
> **A:** "Revisé los logs con `journalctl`, comparé la configuración con la documentación oficial y
> detecté un permiso mal puesto en un directorio de trabajo."
> **R:** "Corregí el permiso, el servicio arrancó y documenté el caso en un writeup; ahora reviso
> logs primero en lugar de probar al azar."

Preguntas típicas de comportamiento:

- "Cuéntame una vez en que trabajaste en equipo y hubo un desacuerdo."
- "¿Cómo gestionas varias tareas a la vez con poco tiempo?"
- "Háblame de un error que cometiste y qué aprendiste."
- "¿Por qué te interesa la ciberseguridad y hacia dónde quieres ir?"

!!! tip "Prepara 4-5 historias reutilizables"
    Con 4 o 5 casos bien pensados (un éxito, un error, un conflicto, un trabajo bajo presión, algo
    que aprendiste solo) puedes responder a casi cualquier pregunta de comportamiento.

## Pruebas técnicas

Formatos habituales, para que no te sorprendan:

- **Reto tipo CTF o máquina.** Resolver un entorno controlado y explicar los pasos.
- **Ejercicio en directo.** Te piden analizar algo mientras piensas en voz alta.
- **Tarea para casa.** Un caso a resolver con tiempo; cuidado con el límite de horas que te den.
- **Preguntas de diseño.** "¿Cómo protegerías esta red/servicio?"

Consejos:

- **Piensa en voz alta.** El entrevistador quiere ver tu razonamiento.
- **No te bloquees.** Si algo no sale, di qué probarías después.
- **Pregunta lo que no entiendas.** Pedir aclaraciones es señal de madurez.
- **Documenta como en un writeup.** Un mini-informe ordenado impresiona.

## Preparar un laboratorio de demostración

Si te piden demostrar tus habilidades, un laboratorio propio listo es una gran baza:

- [ ] **Entorno aislado:** red interna de virtualización sin salida a producción.
- [ ] **Máquinas:** una atacante (Kali/Parrot) y una o varias vulnerables.
- [ ] **Guion:** qué vas a mostrar en 5-10 minutos, con principio y fin.
- [ ] **Un caso que domines:** mejor algo pequeño y bien explicado que mucho y a medias.
- [ ] **Capturas o terminal:** ten preparado qué enseñar si falla la conexión.
- [ ] **Ética y legalidad:** recuerda en voz alta que es tu laboratorio y está autorizado para ello.

Puedes apoyarte en [virtualbox.org](https://www.virtualbox.org) o [vmware.com](https://www.vmware.com)
y en [vulnhub.com](https://www.vulnhub.com) para máquinas de práctica.

## Preguntas que debes hacer tú

La entrevista es de doble sentido. Pregunta con naturalidad:

- ¿Cómo es un día típico en el equipo?
- ¿Qué herramientas usáis a diario?
- ¿Cómo es el proceso de incorporación y formación?
- ¿Qué se espera de esta persona a los 3 y 6 meses?
- ¿Cómo se mide el éxito en el puesto?
- ¿Cuáles son los mayores retos técnicos del equipo ahora mismo?

## Errores comunes en entrevistas

| Error | Mejora |
| --- | --- |
| Inventar que sabes algo | Reconoce lo que no sabes y explica cómo lo aprenderías |
| Respuestas de una palabra | Amplía con el porqué |
| Hablar mal de un jefe o compañero | Céntrate en lo que aprendiste |
| No preguntar nada | Prepara 2-3 preguntas |
| Llegar sin haber mirado la oferta | Relaciona tu perfil con lo que piden |
| Prometer disponibilidad que no tienes | Sé honesto con tus condiciones |

## Checklist antes de la entrevista

- [ ] He releído la oferta y adaptado mi discurso.
- [ ] Tengo preparadas 4-5 historias STAR.
- [ ] Repasé fundamentos de redes, Linux y web.
- [ ] Mi laboratorio de demostración funciona (si lo voy a usar).
- [ ] Tengo 2-3 preguntas preparadas.
- [ ] Probé conexión y cámara si es online.

## Para ir más allá

| Recurso | Tipo | Idioma | Coste |
| --- | --- | --- | --- |
| [owasp.org](https://owasp.org) | Referencia de seguridad web | EN | Gratis |
| [portswigger.net/web-security](https://portswigger.net/web-security) | Laboratorios prácticos | EN | Gratis |
| [Dónde practicar](../nivel-1-principiante/06-donde-practicar/index.md) | Contenido interno | ES | Gratis |
| [Paths por área](../paths/index.md) | Preparación por especialidad | ES | Gratis |

## Siguiente paso

Encuentra dónde enviar todo esto: **[Portales de empleo](portales-de-empleo.md)**.
