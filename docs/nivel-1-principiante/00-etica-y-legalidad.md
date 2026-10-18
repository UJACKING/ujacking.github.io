# 00 · Ética y legalidad

Antes de aprender ninguna técnica hay que entender **dónde se puede practicar y dónde no**. El
hacking ético consiste en buscar fallos de seguridad **con permiso**, para que quien los sufre pueda
arreglarlos. Esta página te da el marco ético, el legal (a nivel general) y la plantilla de
autorización que necesitarás toda tu carrera.

Esta no es una página "de relleno" que puedas saltarte: es la que te evita problemas legales y la que
te enseña a comportarte como un profesional.

## Objetivos de aprendizaje

Al terminar esta página deberías ser capaz de:

- Explicar qué es el hacking ético y en qué se diferencia del delito informático.
- Distinguir los **tipos de hackers** (sombrero blanco, negro y gris) y qué son los hacktivistas.
- Entender por qué la **autorización por escrito** es imprescindible y no un trámite.
- Definir el **alcance (scope)** de una prueba y por qué hay que respetarlo.
- Describir la **divulgación responsable** y qué es un **bug bounty** a grandes rasgos.
- Conocer, a nivel orientativo, qué conductas castiga el **Código Penal español**.
- Aplicar las **reglas de oro** de un laboratorio seguro.

**Tiempo estimado: 45-60 min.**

## Requisitos previos

- Ninguno. Esta es la **primera página** del Nivel 1.
- Si aún no sabes cómo está organizada la web, mira el [índice del Nivel 1](index.md).

## Explicación

### ¿Qué es el hacking ético?

El **hacking ético** (o *pentesting*, del inglés *penetration testing*: pruebas de penetración) es la
práctica de **analizar sistemas con permiso** para encontrar sus fallos **antes** que un atacante
malicioso. La diferencia con un delito no es la técnica, sino el **permiso** y la **intención**:

| | Hacker ético | Ciberdelincuente |
| --- | --- | --- |
| Permiso | Sí, **por escrito** y con alcance definido | No |
| Objetivo | Que se arreglen los fallos | Beneficio propio, daño, chantaje |
| Resultado | Informe y (si procede) ayuda a corregir | Uso de los fallos en beneficio propio |
| Consecuencia legal | Ninguna (es legal) | Delito |

En ciberseguridad se habla de:

- **Red team** (equipo rojo): simula a un atacante para poner a prueba las defensas.
- **Blue team** (equipo azul): defiende, detecta y responde a los ataques.
- **Purple team**: trabaja para que rojo y azul colaboren y aprendan juntos.

Todo lo que aprendas en esta web es **doble uso**: las mismas herramientas sirven para auditar tu
laboratorio o para atacar a un vecino. La ética decide cuál de las dos.

### Tipos de hackers

Los "sombreros" (del inglés *hat*) son una forma clásica y útil de clasificar intenciones:

| Tipo | Permiso | Intención | Ejemplo |
| --- | --- | --- | --- |
| **Sombrero blanco** (*white hat*) | Sí | Legítima: mejorar la seguridad | Consultor de pentesting contratado |
| **Sombrero negro** (*black hat*) | No | Maliciosa: robar, dañar, lucrarse | Ciberdelincuente que vende datos |
| **Sombrero gris** (*grey hat*) | No (o dudoso) | Mixta | Alguien que encuentra un fallo sin permiso y luego lo reporta |

Matices que conviene conocer desde el principio:

- **Hacktivistas**: atacan sistemas con una motivación **política o social** (por ejemplo, como
  protesta). Aunque su causa te parezca justa, **atacar sistemas sin permiso es un delito**. La
  motivación no cambia la legalidad.
- **APTs** (*Advanced Persistent Threat*, amenaza persistente avanzada): grupos muy organizados,
  normalmente ligados a Estados o al crimen organizado, que atacan de forma sigilosa y sostenida en
  el tiempo. Son el "otro lado" profesional: bien financiados y muy pacientes. Existen dentro de los
  sombreros negros, pero a gran escala.

!!! info "Sombreros vs. roles laborales"
    Los "sombreros" describen la **intención**, no el puesto de trabajo. Un mismo profesional puede
    ser red team en un proyecto y blue team en otro. Lo que nunca cambia es que **siempre se actúa con
    autorización**.

### Autorización por escrito y por qué es imprescindible

Sin permiso, cualquier prueba técnica es, legalmente, un posible delito, por muy buenas que sean tus
intenciones. El permiso debe ser:

- **Por escrito**: un correo vale como punto de partida, pero lo profesional es un **contrato de
  autorización** firmado (mira la plantilla al final de esta página).
- **Explícito**: debe decir claramente que te autorizan a hacer las pruebas.
- **Con alcance definido**: qué sistemas, qué ventana de tiempo, qué técnicas están permitidas.
- **Firmado por quien puede autorizarlo**: el dueño del sistema o alguien con poder para hacerlo.
  Que un amigo te diga "tú prueba en la web de mi empresa" **no** es autorización si él no es el
  responsable.

Nunca aceptes un "te doy permiso" verbal y recuerda: si un sistema no es tuyo, **no lo toques** sin
ese papel.

### Alcance (scope) de una prueba

El **alcance** o *scope* es la frontera exacta de lo que puedes tocar. Incluye, como mínimo:

- **Qué**: direcciones IP, dominios, subdominios, aplicaciones, rangos de red.
- **Cuándo**: fechas y horas permitidas (a veces fuera del horario de producción).
- **Cómo**: qué técnicas se permiten y cuáles están **prohibidas** (por ejemplo, no ataques de
  denegación de servicio, no ingeniería social, no modificar datos).
- **Exclusiones**: sistemas que están expresamente fuera, aunque parezcan parte del conjunto.

Reglas prácticas del scope:

1. **Lo que no está listado, está prohibido.** Si dudas de si algo entra en alcance, pregunta.
2. Los sistemas que pertenecen a **terceros** (un proveedor de cloud, un hosting compartido) quedan
   fuera aunque estén "pegados" a los del cliente.
3. Deja constancia por escrito de cualquier duda o ampliación de alcance.

!!! warning "Salirse del alcance es un problema real"
    Tocar un sistema que no estaba en el scope, aunque sea "para comprobar algo", puede romper el
    contrato y constituir un delito. El scope no es una sugerencia: es el límite legal.

### Divulgación responsable (responsible disclosure)

Cuando encuentras un fallo, lo correcto es **avisar en privado** a quien puede arreglarlo y darle un
tiempo razonable antes de hacerlo público. Un procedimiento habitual:

1. **Documenta** el fallo: qué es, cómo se reproduce, qué impacto tiene.
2. **Contacta en privado**: busca el canal de seguridad del responsable (por ejemplo, un correo
   `security@` o una política de divulgación). Si no lo encuentras, márcalo como `TODO-UJACKING` en
   tu proceso y busca una vía alternativa.
3. **Da tiempo**: acuerda un plazo razonable para que lo corrijan antes de publicar nada.
4. **Coordina**: no publiques detalles que pongan en riesgo a usuarios hasta que esté arreglado.
5. **Nunca** exijas dinero a cambio de no publicar el fallo: eso es **extorsión** y es delito.

### Bug bounty a alto nivel

Un **bug bounty** ("recompensa por fallos") es un programa en el que una organización **invita
públicamente** a investigar sus sistemas y **ofrece una recompensa** por reportar vulnerabilidades
válidas. Es, en la práctica, un permiso predefinido.

Cómo funciona por encima:

1. La organización publica un **programa** con sus **reglas** y su **alcance**: qué sistemas puedes
   probar y cuáles no.
2. Tú investigas **dentro de ese alcance** y respetando las reglas.
3. Envías un **informe** con el fallo y su reproducción.
4. El equipo del programa lo **evalúa** (*triage*) y decide si es válido y con qué severidad.
5. Si es válido y está cubierto, puede haber **recompensa** y **reconocimiento**.

Puntos importantes, sin inventar detalles:

- **Las reglas del programa son la ley.** Si algo está excluido, no se toca.
- Muchos programas **no pagan** por todos los fallos, solo por los que cumplen sus criterios.
- Hay programas que **solo dan reconocimiento**, sin pago. Y hay plataformas **gratuitas** para
  practicar (laboratorios legales) antes de tocar un programa real.
- No todos los fallos "raros" cuentan: cada programa define qué es válido.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Añadir aquí, cuando se verifiquen, los enlaces a las **plataformas de bug bounty** y a los
    programas de referencia, así como ejemplos de **políticas de divulgación**. No inventar nombres
    de programas, importes ni pagos concretos.

Existe un apartado de la web dedicado al bug bounty dentro de los **paths**; lo verás cuando avances
en tu ruta.

### Marco legal español (orientativo)

!!! danger "Esto NO es asesoramiento legal"
    Esta sección es **divulgativa y orientativa**. No sustituye al consejo de un abogado o de una
    persona con formación jurídica. Si tienes un caso real, consulta a un profesional.

En España, el **Código Penal** castiga, entre otras, estas conductas (los números de artículo que se
citan son **orientativos y están pendientes de verificar**):

| Conducta | Descripción divulgativa |
| --- | --- |
| **Acceso ilícito a sistemas informáticos** | Entrar (o intentarlo) en un sistema sin autorización. Artículo `197 bis` `TODO-UJACKING`: número pendiente de verificar por una persona con formación jurídica. |
| **Descubrimiento y revelación de secretos** | Apoderarse o difundir datos o comunicaciones ajenos. Artículo `197` (y siguientes) `TODO-UJACKING`: números pendientes de verificar. |
| **Daños informáticos** | Borrar, alterar o inutilizar datos, programas o sistemas ajenos. Artículo `264` `TODO-UJACKING`: número pendiente de verificar. |
| **Estafa informática** | Conseguir un beneficio patrimonial mediante engaño (por ejemplo, *phishing*). Artículos `248` y `249` `TODO-UJACKING`: números pendientes de verificar. |

!!! warning "PENDIENTE (TODO-UJACKING)"
    Los números de artículo del Código Penal citados arriba (`197`, `197 bis`, `264`, `248`, `249`)
    son **orientativos y no están verificados**. Deben ser revisados, corregidos y ampliados por una
    **persona con formación jurídica** antes de publicar esta página. Valorar también añadir
    referencias al `197 ter` y a la normativa europea pertinente `TODO-UJACKING`.

Ideas clave que **sí** puedes dar por seguras, sin necesidad de citar artículos:

- Practicar contra sistemas de los que **no eres responsable** y sin autorización puede ser delito.
- La **intención** (curiosidad, "solo probaba", "quería ayudar") no convierte en legal un acceso no
  autorizado.
- La **autorización por escrito** es tu principal protección legal, aunque tampoco es un salvoconducto
  absoluto: si te sales del alcance, la autorización deja de cubrirte.

### Reglas de oro del laboratorio

1. **Laboratorio aislado.** Monta tus máquinas atacante y objetivo en una red propia, sin acceso a
   Internet si es posible, o con salida controlada.
2. **Solo lo tuyo.** Practica contra máquinas que has creado tú o contra plataformas legales.
3. **Snapshots.** En máquinas virtuales, haz una **instantánea** antes de experimentar: si rompes
   algo, vuelves atrás en segundos.
4. **Nada de datos reales.** No uses datos personales reales en tus pruebas; inventa datos de ejemplo.
5. **Copia de seguridad.** Guarda una copia de tu máquina base para no tener que reinstalarla.
6. **Permiso para todo lo que no sea tu laboratorio.** Ante la duda, no lo toques.

### Qué NO hacer nunca

!!! danger "Líneas rojas"
    - **Atacar** un sistema del que no eres responsable y sin autorización.
    - **Escanear** redes públicas, de tu universidad, de tu trabajo o de un vecino.
    - **Distribuir o crear malware** funcional con fines dañinos.
    - **Publicar** datos de vulnerabilidades sin dar tiempo a arreglarlas (divulgación no
      responsable).
    - **Exigir dinero** a cambio de no revelar un fallo (extorsión).
    - **Usar datos reales de personas** en tus prácticas.
    - **Escudarte en "es solo curiosidad"**: la curiosidad no te protege legalmente.

### Plantilla de autorización (ejemplo)

!!! warning "PLANTILLA — a adaptar, no es asesoramiento legal"
    Este texto es una **plantilla orientativa** para que veas las claves que debe cubrir una
    autorización. **No es un documento legal válido tal cual**: debe adaptarla y revisarla una
    persona con formación jurídica, y firmarla quien tiene competencia para autorizar las pruebas.

```text
AUTORIZACIÓN PARA PRUEBAS DE SEGURIDAD (PENTESTING)

Cliente (autorizante): ____________________________________
NIF / CIF:               ____________________________________
Persona de contacto:     ____________________________________
Correo / teléfono:       ____________________________________

Autorizo a (profesional/empresa): __________________________
NIF / CIF:               ____________________________________

a realizar pruebas de seguridad sobre los siguientes sistemas:

  1) SISTEMAS EN ALCANCE (IP, dominios, subdominios, aplicaciones):
     - ______________________________________________________
  2) SISTEMAS FUERA DE ALCANCE (excluidos expresamente):
     - ______________________________________________________
  3) VENTANA TEMPORAL (fechas y horas):
     - Del ____/____/______ al ____/____/______, de __:__ a __:__ (hora local).
  4) TÉCNICAS PERMITIDAS:
     - ______________________________________________________
  5) TÉCNICAS PROHIBIDAS (p. ej. denegación de servicio, ingeniería social):
     - ______________________________________________________
  6) CONTACTOS DE EMERGENCIA DURANTE LAS PRUEBAS:
     - ______________________________________________________
  7) LÍMITES Y CONDICIONES ESPECIALES:
     - ______________________________________________________

El profesional se compromete a:
  - No acceder a datos reales más allá de lo necesario para demostrar el fallo.
  - Reportar los hallazgos de forma privada y confidencial.
  - No divulgar información sin autorización previa por escrito.

Firma del cliente:                    Firma del profesional:
___________________________           ___________________________
Nombre y cargo:                       Nombre:
Fecha: ____/____/______               Fecha: ____/____/______
```

## Ejemplos prácticos

### 1. Comprobar tu identidad y entorno antes de practicar

Antes de tocar nada, sitúate: ¿en qué máquina estás y en qué red?

```bash
whoami
hostname
ip -brief address
```

- `whoami` — con qué **usuario** estás trabajando (salida de ejemplo: `kali`).
- `hostname` — el **nombre** de la máquina (salida de ejemplo: `lab-kali`).
- `ip -brief address` — las **interfaces de red** y sus direcciones (`lo` es tu bucle local,
  `eth0`/`wlan0` son las reales).

Esto te ayuda a confirmar que estás en **tu laboratorio** y no en un sistema ajeno.

### 2. Verificar el alcance de una plataforma legal

Antes de empezar en cualquier plataforma de práctica, lee sus **reglas** y su alcance. Es tu
"autorización" implícita. Enlaza siempre desde el dominio raíz:

- [TryHackMe](https://tryhackme.com) — **Gratis / Freemium**, en inglés (y parte en español).
- [Hack The Box](https://www.hackthebox.com) — **Gratis / Freemium**, en inglés.
- [OverTheWire](https://overthewire.org) — **Gratis**, en inglés (perfecto para empezar).
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — **Gratis**, en inglés.

### 3. Correo de divulgación responsable (plantilla)

Un aviso claro y educado acelera que arreglen el fallo:

```text
Asunto: Notificación de vulnerabilidad — [sistema] — [fecha]

Hola:

Me pongo en contacto para informar de un posible problema de seguridad en
[sistema/dominio]. No he accedido a datos de otros usuarios ni he modificado
nada; solo he realizado una comprobación mínima para confirmarlo.

Resumen: [una línea de qué es el fallo]
Cómo reproducirlo: [pasos breves]
Impacto estimado: [qué podría permitir]
Recomendación: [idea de corrección]

Quedo a vuestra disposición para ampliar la información y os pido un plazo
razonable para corregirlo antes de cualquier publicación. No he divulgado
ni divulgaré estos detalles a terceros sin vuestra autorización.

Un saludo,
[Nombre y contacto]
```

## Errores comunes

| Error | Por qué está mal | Solución |
| --- | --- | --- |
| "Solo entro un segundo, no pasa nada" | Acceder sin permiso ya puede ser delito. | No entres. Consigue autorización por escrito. |
| "Me lo autorizó un amigo de la empresa" | Puede no tener competencia para autorizar. | Pide la firma del responsable real. |
| Escanear la red del instituto "para probar un comando". | Está fuera de cualquier alcance y no autorizado. | Practica en tu laboratorio o en plataformas legales. |
| Ignorar las exclusiones del scope. | Rompe el contrato y te expone legalmente. | Repasa el scope y, ante la duda, pregunta antes. |
| Publicar el fallo al día siguiente. | Divulgación no responsable. | Da un plazo razonable y coordina. |
| Pedir dinero por no publicar. | Es extorsión. | Nunca lo hagas: reporta y ofrece arreglo. |
| Usar datos reales en el laboratorio. | Riesgo legal y de privacidad. | Inventa datos de ejemplo. |

## Ejercicios

1. **Clasifica.** Empareja cada caso con el tipo de hacker (blanco, negro, gris):
   (a) una consultora contratada que audita un banco; (b) alguien que entra en un sistema sin permiso
   y vende los datos; (c) alguien que encuentra un fallo sin permiso y luego lo reporta.

   ??? success "Solución"
       (a) **Sombrero blanco**: hay contrato y permiso.
       (b) **Sombrero negro**: sin permiso y con intención de lucrarse.
       (c) **Sombrero gris**: sin permiso, pero con intención de que se arregle.

2. **Define el scope.** Tu cliente te autoriza a probar `app.cliente.example`. ¿Puedes probar
   `blog.cliente.example`? Razona la respuesta.

   ??? success "Solución"
       **No**, salvo que el contrato lo incluya. El scope era `app.cliente.example`; lo que no está
       listado está prohibido. Debes pedir una **ampliación por escrito** del alcance si quieres
       probar el blog.

3. **Detecta el fallo ético.** Te encuentras una base de datos con datos de miles de clientes.
   ¿Qué NO debes hacer y qué sí?

   ??? success "Solución"
       **No** debes descargar, copiar, difundir ni usar esos datos. Sí debes **documentar la
       existencia** del problema sin volcar los datos, reportarlo **en privado** por el canal de
       seguridad y dar un **plazo razonable** para que lo corrijan.

4. **Divulgación.** Encuentras un fallo en un servicio online y no hay política de divulgación
   visible. Escribe los 3 primeros pasos de tu procedimiento.

   ??? success "Solución"
       1. Documentar el fallo (qué, cómo se reproduce, impacto) y **no** explotarlo más allá de lo
          mínimo.
       2. Buscar un canal de contacto privado: correo `security@`, formulario de contacto o
          responsable de privacidad.
       3. Enviar un aviso claro y **pedir un plazo razonable** antes de cualquier publicación. Si no
          hay forma de contactar, marcar el caso como pendiente y no publicar datos sensibles.

5. **Legalidad.** Alguien te dice: "entra en la web de mi empresa sin que nadie se entere y me dices
   si es segura; luego te pago". ¿Qué compruebas antes de aceptar?

   ??? success "Solución"
       Que exista una **autorización por escrito**, que la firme **quien puede autorizarla**, y que
       incluya **alcance, ventana temporal, técnicas permitidas y prohibidas**. Un encargo informal
       de alguien que no es el responsable **no** te protege legalmente.

6. **Reglas del laboratorio.** Enumeras 3 medidas que eviten que tus prácticas afecten a terceros.

   ??? success "Solución"
       Ejemplos válidos: (1) red de laboratorio **aislada** sin salida a Internet o con salida
       controlada; (2) practicar **solo** contra máquinas propias o plataformas autorizadas;
       (3) usar **snapshots** y copias de seguridad para revertir cualquier cambio.

## Resumen

- El hacking ético es **con permiso**: la técnica es la misma, la diferencia es legal y ética.
- Sombreros: **blanco** (permiso, bien), **negro** (sin permiso, mal), **gris** (sin permiso, mixto).
  Hacktivistas y APTs son matices de motivación y organización.
- La **autorización por escrito** con **alcance claro** es tu principal protección.
- **Divulgación responsable**: avisa en privado, da tiempo, coordina, nunca extorsiones.
- El **bug bounty** es un permiso público con **reglas** que son sagradas; no todos los fallos se pagan.
- El **Código Penal español** castiga el acceso ilícito, los daños, la revelación de secretos y la
  estafa informática (números de artículo **pendientes de verificar**).
- Practica **solo** en tu laboratorio o en plataformas que lo autorizan.

## Checklist

- [ ] Sé explicar la diferencia entre hacking ético y delito informático.
- [ ] Distingo sombrero blanco, negro y gris, y sé qué son hacktivistas y APTs.
- [ ] Entiendo por qué necesito **autorización por escrito** y qué debe incluir.
- [ ] Sé qué es el **alcance (scope)** y por qué "lo no listado está prohibido".
- [ ] Sé qué es la **divulgación responsable** y qué pasos sigue.
- [ ] Puedo describir un **bug bounty** por encima sin inventarme detalles.
- [ ] Conozco las conductas que castiga el Código Penal a nivel orientativo.
- [ ] Tengo claras las **reglas de oro** del laboratorio y las líneas rojas.

## Para ir más allá

- [Ruta perfecta](../ruta-perfecta.md) — el plan de estudio de 12 semanas. **Gratis**, español.
- [Glosario de UJACKING](../glosario.md) — términos clave explicados en claro. **Gratis**, español.
- [OWASP](https://owasp.org) — referencia internacional sobre seguridad de aplicaciones. **Gratis**,
  inglés (EN).
- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — laboratorios web legales
  y gratuitos. **Gratis**, inglés (EN).
- [TryHackMe](https://tryhackme.com) — rutas guiadas para principiantes. **Freemium**, inglés (parte
  en español).

## Siguiente paso

Ya tienes el marco ético y legal. Ahora sí, empezamos por la base técnica:
**[Arquitectura de ordenadores](01-arquitectura-de-ordenadores/index.md)**. Antes de atacar nada,
conviene entender qué hay dentro de una máquina.
