# PortSwigger Web Security Academy

**El mejor recurso gratuito del mundo para aprender seguridad web.** La Web Security Academy la
mantiene PortSwigger, la empresa detrás de Burp Suite, y ofrece teoría y **laboratorios** de
vulnerabilidades web reales. Es gratis y sin excusas: si tu interés es la seguridad web, esto va antes
que pagar cualquier curso.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Explicar qué es la Web Security Academy y por qué es una referencia.
- Entender por qué los laboratorios son seguros y legales.
- Seguir los laboratorios **por temas**, empezando por los más fáciles.
- Reconocer las grandes familias de vulnerabilidades web y relacionarlas con el OWASP Top 10.

**Tiempo estimado:** 30-45 min de lectura; cada laboratorio, entre 10 y 60 min.

## Requisitos previos

- [Índice del módulo](index.md): comparativa de plataformas.
- [02 · Protocolos de aplicación](../02-redes/07-protocolos-de-aplicacion.md): HTTP, DNS y compañía.
- [02 · Seguridad en tránsito](../02-redes/08-seguridad-en-transito.md): HTTP vs HTTPS.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md).

## Explicación

### ¿Qué es la Web Security Academy?

Es una plataforma de formación **gratuita** sobre seguridad en aplicaciones web. Cada tema trae:

1. Una **parte teórica** clara (qué es la vulnerabilidad, por qué existe).
2. Uno o varios **laboratorios** (labs) donde explotas esa vulnerabilidad de verdad.
3. Una **solución** que puedes consultar cuando te atascas.

Los laboratorios están en servidores **de PortSwigger**, creados a propósito para ser vulnerables. Eso
los hace **legales y seguros**: es exactamente donde se practica.

### ¿Por qué es de lo mejor y además gratis?

- Lo mantiene **la empresa de Burp Suite**, la herramienta de referencia en seguridad web.
- La teoría es precisa y está actualizada (vulnerabilidades del mundo real).
- Los laboratorios son **modernos** y cubren desde lo básico hasta ataques avanzados.
- Es **100 % gratis**: no hay plan de pago que desbloquee los labs.

No hay truco ni versión "lite". Es su forma de que la comunidad aprenda y adopte Burp.

### Organización por temas

La Academy agrupa el contenido en **temas** (topics), y dentro de cada tema hay laboratorios de
dificultad creciente (normalmente etiquetados como *Apprentice*, *Practitioner* y *Expert*).

Temas clásicos que estudiarás:

| Familia | Ejemplo de vulnerabilidad |
| --- | --- |
| **Inyección** | SQL injection, comandos OS |
| **Scripting del lado cliente** | XSS, CSRF, CORS |
| **Lógica de negocio** | Fallos en flujos de la aplicación |
| **Autenticación y sesiones** | Fuerza bruta, robo de cookies |
| **Control de acceso** | IDOR, escalada de privilegios web |
| **Ataques del lado servidor** | SSRF, deserialización |
| **API y JWT** | Manipulación de tokens |
| **Componentes y config** | Vulnerabilidades de dependencias |

Muchos de estos temas aparecen en el **OWASP Top 10**, el listado de referencia de riesgos web.
Enlázalo y úsalo como mapa: [https://owasp.org](https://owasp.org).

!!! tip "Regla de oro: por temas y de fácil a difícil"
    No vayas saltando. Coge **un tema**, haz todos sus laboratorios en orden, y solo entonces pasa al
    siguiente. La dificultad está pensada para que cada lab te prepare para el siguiente.

!!! danger "Aviso ético"
    Trabaja **solo** en los laboratorios de la Academy y en entornos que te autoricen. Aprender un
    ataque (por ejemplo, una inyección SQL) es legal; **usarlo contra una web que no es tuya, no**.
    Es delito y no hay "estaba practicando" que valga.

## Ejemplos prácticos

**1. Empezar un laboratorio.** El flujo típico:

1. Crea una cuenta gratuita en [https://portswigger.net/web-security](https://portswigger.net/web-security).
2. Abre un tema y su primer laboratorio ("Apprentice").
3. Lee la teoría del tema.
4. Pulsa "Access the lab": se abre una web vulnerable en el navegador.
5. Aplícale el ataque hasta resolverlo. El lab se marca como resuelto.

**2. Comprobar que entiendes HTTP (la base de todo).** Antes de atacar nada, mira las peticiones. Con
`curl` ves el intercambio crudo:

```bash
curl -s -o /dev/null -w "%{http_code}\n" https://portswigger.net/web-security
```

```text
200
```

- `-s` — modo silencioso (sin barra de progreso).
- `-o /dev/null` — descarta el cuerpo de la respuesta.
- `-w "%{http_code}\n"` — imprime solo el código de estado HTTP.
- `200` significa "OK": la petición fue bien.

**3. Ver las cabeceras de una respuesta.** Útil para muchos laboratorios:

```bash
curl -sI https://portswigger.net/web-security | head -n 5
```

```text
HTTP/2 200
content-type: text/html; charset=utf-8
... (salida de ejemplo)
```

`-I` pide solo las **cabeceras** (`HEAD`). Aprenderse a leerlas te ahorrará horas.

**4. Orden de estudio sugerido** (asumiendo que empiezas de cero):

| Orden | Tema | Por qué |
| --- | --- | --- |
| 1 | Access control (control de acceso) | Muy intuitivo y muy común. |
| 2 | Authentication | Fácil de entender y de explotar. |
| 3 | SQL injection | El clásico; imprescindible. |
| 4 | XSS | Muy didáctico y visual. |
| 5 | CSRF | Encaja tras XSS y sesiones. |

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "No entiendo el lab" | No has leído la teoría del tema | Lee la parte teórica **antes** del lab |
| "Voy directo a Expert" | Impaciencia | Empieza por Apprentice, siempre |
| "Pego payloads sin entender" | Copiar y pegar | Entiende qué hace cada parte del payload |
| "No veo las peticiones" | No usas proxy | Aprende a interceptar con Burp Suite |
| "Se me olvida lo hecho" | No documentas | Anota cada lab resuelto y cómo |

## Ejercicios

1. **Crea la cuenta y encuentra el mapa.** Regístrate y localiza la lista de temas (all topics). Anota
   los cinco primeros temas que aparezcan y sus niveles.

    ??? success "Solución"
        Los temas y su orden cambian con las actualizaciones, así que la respuesta válida es **la lista
        real que veas hoy**. Lo importante es que identifiques la estructura tema → laboratorios →
        nivel (Apprentice / Practitioner / Expert).

2. **Resuelve tu primer laboratorio "Apprentice".** Elige el tema de control de acceso y completa el
   laboratorio más básico.

    ??? success "Solución"
        Se comprueba en la propia Academy: el laboratorio debe aparecer como **Solved**. Apunta en tu
        repositorio qué vulnerabilidad era y qué cambiaste en la petición para explotarla.

3. **Inspecciona una petición HTTP con `curl`.** Haz una petición a la home de la Academy y guarda
   las cabeceras en un fichero.

    ??? success "Solución"
        ```bash
        curl -sI https://portswigger.net/web-security -o cabeceras.txt
        cat cabeceras.txt | head
        ```

        Debe contener la línea de estado (`HTTP/2 200`) y varias cabeceras (salida de ejemplo).

4. **Relaciona vulns con el OWASP Top 10.** Elige tres temas de la Academy e indica a qué categoría
   del OWASP Top 10 se parecen más.

    ??? success "Solución"
        No hay una correspondencia 1 a 1 perfecta, pero ejemplos razonables:
        - SQL injection → categoría de **inyección**.
        - Control de acceso roto → **Broken Access Control**.
        - Fallos de autenticación → **Identification and Authentication Failures**.

        Lo evaluable es que **sepas ubicar** cada vulnerabilidad en el mapa del OWASP Top 10.

5. **Planifica un tema completo.** Elige un tema y planifica cuántos laboratorios harás por sesión
   hasta terminarlo.

    ??? success "Solución"
        Ejemplo:

        ```markdown
        Tema: SQL injection
        Labs: 3 por sesión, 3 sesiones
        Sesión 1: los 3 primeros (Apprentice)
        Sesión 2: 3 Practitioner
        Sesión 3: resto + repaso y writeup
        ```

6. **Explica una vulnerabilidad con tus palabras.** Escoge XSS y explícala en 4-5 líneas como si se la
   contaras a alguien que no sabe nada.

    ??? success "Solución"
        Ejemplo válido: "XSS (Cross-Site Scripting) ocurre cuando una web muestra en la página datos
        que vienen del usuario sin limpiarlos. Si un atacante consigue meter **código JavaScript** en
        esos datos, el navegador de la víctima lo ejecutará como si fuera parte de la web. Con eso puede
        robar la sesión, redirigir a otra página o mostrar contenido falso."

## Resumen

- La Web Security Academy es **gratis** y es la referencia para seguridad web.
- Combina **teoría + laboratorios** reales en servidores de PortSwigger (legales).
- Se organiza **por temas** y por dificultad (Apprentice → Expert).
- Estudia **un tema completo** antes de pasar al siguiente.
- Los labs se conectan con el **OWASP Top 10**: úsalo como mapa.

## Checklist

- [ ] Tengo cuenta en la Web Security Academy.
- [ ] Sé navegar por temas y distinguir los niveles de dificultad.
- [ ] He resuelto al menos un laboratorio de nivel Apprentice.
- [ ] Entiendo cómo ver una petición/respuesta HTTP (al menos con `curl`).
- [ ] Sé relacionar varias vulnerabilidades con el OWASP Top 10.
- [ ] Guardo mis writeups de los labs en mi repositorio.

## Para ir más allá

- **PortSwigger Web Security Academy** — Plataforma oficial. Nivel: principiante-avanzado. Idioma:
  (EN). **Gratis**. [https://portswigger.net/web-security](https://portswigger.net/web-security)
- **OWASP** — Organización y OWASP Top 10. Nivel: todos. Idioma: (EN). **Gratis**.
  [https://owasp.org](https://owasp.org)
- **Seguridad web y OWASP Top 10** (Nivel 2 de UJACKING) — Profundiza en estas vulnerabilidades.
  [Seguridad web y OWASP Top 10](../../nivel-2-medio/07-seguridad-web-y-owasp-top-10.md)
- **Burp Suite** (Nivel 2 de UJACKING) — La herramienta que necesitarás para los labs avanzados.
  [Burp Suite](../../nivel-2-medio/08-burp-suite.md)

## Siguiente paso

Ya has tocado retos guiados y web. Ahora, la experiencia de competir: **[CTFs](05-ctfs.md)**.
