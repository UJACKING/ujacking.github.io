# Módulo 01 · Arquitectura de ordenadores

**Qué hay dentro de una máquina y cómo funciona.** Antes de escanear puertos o atacar una web conviene
entender qué es una CPU, qué es la memoria, cómo se representan los datos (bits, bytes, hexadecimal) y
cómo arranca un ordenador. Es la base sobre la que se apoyan las redes, los sistemas operativos y la
seguridad.

No vas a montar un ordenador pieza a pieza: vas a entender **los conceptos** que después aparecerán
una y otra vez en tu día a día como profesional.

## Objetivos de aprendizaje

Al terminar este módulo deberías ser capaz de:

- Identificar los **componentes** principales de un ordenador y qué hace cada uno.
- Entender la **jerarquía de memoria** y por qué una CPU parece "trabajar sola".
- Convertir números entre **binario, octal, decimal y hexadecimal**.
- Manejar con soltura **bits, bytes, nibbles y múltiplos** (KB, MB, GB, TB) y saber qué es un **nibble**.
- Entender la **representación de datos**: endianness, ASCII/Unicode y el ciclo de la CPU.
- Conocer el **arranque** del sistema (BIOS/UEFI, GRUB, kernel, init) y qué es la **virtualización**.

**Tiempo total estimado del módulo: 5-6 horas** (repartidas en las 4 páginas, según el tiempo indicado
en cada una).

## Requisitos previos

- Ninguno técnico. Es el **primer módulo** del Nivel 1.
- Antes de practicar nada, lee **[00 · Ética y legalidad](../00-etica-y-legalidad.md)**: marca dónde
  puedes practicar y dónde no.
- Ganas de probar cosas en tu propio ordenador. Todo lo de este módulo es **seguro** y no toca nada
  ajeno.

## Explicación

### ¿En qué consiste este módulo?

Un ordenador es, simplificando, una máquina que **mueve datos** y **ejecuta instrucciones**. Este
módulo responde a cuatro preguntas grandes:

1. **¿Qué piezas tiene y para qué sirve cada una?** → Módulo 01.1
2. **¿Cómo representamos números por dentro?** → Módulo 01.2
3. **¿Cómo se representan datos y se ejecutan programas?** → Módulo 01.3
4. **¿Cómo arranca y cómo puedo tener varios sistemas a la vez?** → Módulo 01.4

Todo lo que viene después (redes, Linux, pentesting) usa estos conceptos. Por eso se estudian primero.

### ¿Qué páginas lo componen?

| Página | De qué va | Tiempo estimado |
| --- | --- | --- |
| [01 · Componentes del ordenador](01-componentes-del-ordenador.md) | CPU, RAM, almacenamiento, placa base, GPU, fuente y buses. | 60-90 min |
| [02 · Sistemas de numeración](02-sistemas-de-numeracion.md) | Binario, octal, decimal, hexadecimal y conversiones. | 90-120 min |
| [03 · Bits, bytes y representación](03-bits-bytes-y-representacion.md) | Bit, byte, endianness, ASCII/Unicode, ciclo de CPU, pila y heap. | 75-90 min |
| [04 · Arranque y virtualización](04-arranque-y-virtualizacion.md) | BIOS/UEFI, GRUB, kernel, init y máquinas virtuales. | 75-90 min |

### Orden recomendado

Estudia las páginas **en el orden de la tabla**:

1. Primero los **componentes** (te da el vocabulario).
2. Después los **sistemas de numeración** (necesitarás el hexadecimal constantemente).
3. Luego **bits, bytes y representación** (cómo se guardan y se ejecutan los datos).
4. Por último **arranque y virtualización** (el puente hacia Sistemas Operativos).

No te saltes el 02 aunque "se te den mal los números": el hexadecimal aparecerá en direcciones MAC,
colores, permisos, memoria y análisis de tráfico. Mejor domésticalo con calma ahora.

!!! tip "Cómo aprovechar el módulo"
    Ten el ordenador delante y **haz los ejercicios** de cada página. Los del sistema de numeración se
    resuelven con papel y lápiz; los de arranque y virtualización se entienden mucho mejor si abres una
    terminal y ejecutas los comandos.

## Ejemplos prácticos

Estos comandos de calentamiento funcionan en **Linux** y te dan una idea de lo que verás en el
módulo. No modifican nada.

```bash
# ¿Qué arquitectura tiene mi máquina? (x86_64 = 64 bits)
uname -m

# ¿Cuánta memoria (RAM) tengo? (-h = unidades legibles)
free -h

# ¿Cuánto espacio en disco? (-h = unidades legibles)
df -h

# Información del procesador
lscpu
```

- `uname -m` — muestra la **arquitectura**: `x86_64` (64 bits Intel/AMD), `aarch64` (64 bits ARM), etc.
- `free -h` — muestra **memoria RAM** total, usada y disponible.
- `df -h` — muestra el **uso de disco** por sistema de archivos.
- `lscpu` — muestra detalles de la **CPU**: núcleos, hilos, frecuencia.

Si algún comando no existe en tu sistema, no pasa nada: en el módulo 01.1 lo explicamos con calma.

## Errores comunes

| Error | Por qué está mal | Solución |
| --- | --- | --- |
| Memorizar sin entender. | Se olvida a la semana. | Relaciona cada concepto con una analogía y practícalo. |
| Saltarse los sistemas de numeración. | El hexadecimal se usa en todas partes. | Haz los ejercicios aunque te cueste. |
| Confundir RAM con almacenamiento. | Son cosas distintas (una es temporal, otra permanente). | Repasa la tabla comparativa del 01.1. |
| Creer que "virtualizar" es "instalar un programa". | Virtualizar implica un **hipervisor** y recursos repartidos. | Lee el 01.4 antes de montar nada. |
| Correr antes de andar. | Este módulo es la base; sin él, lo demás se atasca. | Dedica una semana tranquila a los 4 temas. |

## Ejercicios

1. **Ordena.** Enumera las 4 páginas de este módulo en el orden recomendado de estudio.

   ??? success "Solución"
       1. Componentes del ordenador.
       2. Sistemas de numeración.
       3. Bits, bytes y representación.
       4. Arranque y virtualización.

2. **Planifica.** Tienes 6 horas esta semana para el módulo. Reparte el tiempo entre las 4 páginas.

   ??? success "Solución"
       Un reparto razonable: ~1,5 h en componentes, ~2 h en sistemas de numeración (es el más denso),
       ~1,5 h en bits/bytes y ~1 h en arranque y virtualización, dejando margen para repasar. Lo
       importante es **no dejar el módulo a medias**.

3. **Anticípate.** Sin haber leído el módulo, ¿por qué crees que a un profesional de ciberseguridad le
   importa entender el **arranque** de un ordenador? Da al menos una razón.

   ??? success "Solución"
       Ejemplos válidos: entender el arranque ayuda a comprender el **UEFI/BIOS** y el **Secure Boot**
       (mecanismo de seguridad), los **bootkits**/rootkits que arrancan antes del sistema, y cómo se
       montan los **laboratorios virtuales** en los que practicarás.

4. **Conecta.** ¿Qué relación hay entre el sistema de numeración **hexadecimal** y las direcciones de
   memoria o MAC?

   ??? success "Solución"
       El hexadecimal es una forma **compacta** de escribir binario: cada dígito hexadecimal equivale
       exactamente a **4 bits** (un nibble). Por eso se usa para direcciones de memoria, direcciones
       **MAC** y colores, que en binario serían cadenas larguísimas.

5. **Prepárate.** Escribe qué herramienta usarás para practicar todo lo de este módulo **sin riesgo**.

   ??? success "Solución"
       Una **máquina virtual** (con un hipervisor como VirtualBox o VMware) o un contenedor, siempre
       en un **laboratorio propio**. Nunca practiques contra máquinas ajenas. Esto se detalla en el
       módulo 01.4.

## Resumen

- Este módulo es la **base técnica** de todo lo que vendrá después.
- Se compone de **4 páginas**: componentes, sistemas de numeración, bits/bytes y arranque/virtualización.
- El **orden recomendado** es el de la tabla; no conviene saltarse ninguna.
- **Tiempo total**: unas **5-6 horas**.
- Todo se practica en **tu laboratorio**, nunca contra sistemas ajenos.

## Checklist

- [ ] He leído el índice del Nivel 1 y sé dónde encaja este módulo.
- [ ] Tengo claro el **orden** de las 4 páginas.
- [ ] He reservado tiempo (una semana, aprox.) para hacerlo con calma.
- [ ] He anotado que el **hexadecimal** es clave y no pienso saltármelo.
- [ ] Sé que practicaré **solo** en mi laboratorio.

## Para ir más allá

- [man7.org](https://man7.org) — páginas de manual (`man`) de Linux, útiles para los comandos del
  módulo. **Gratis**, inglés (EN).
- [Ruta perfecta](../../ruta-perfecta.md) — el plan de 12 semanas donde encaja este módulo. **Gratis**,
  español.
- [Glosario de UJACKING](../../glosario.md) — términos como CPU, RAM o byte explicados en claro.
  **Gratis**, español.

## Siguiente paso

Empieza por la primera página: **[01 · Componentes del ordenador](01-componentes-del-ordenador.md)**.

Cuando termines las cuatro, seguirás con el **[Módulo 02 · Redes](../02-redes/index.md)**.
