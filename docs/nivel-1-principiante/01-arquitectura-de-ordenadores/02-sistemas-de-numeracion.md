# 02 · Sistemas de numeración

Los ordenadores no piensan en números "normales": trabajan con **dos estados** (apagado/encendido,
0/1). De ahí nacen el **binario** y, por comodidad, el **octal** y el **hexadecimal**. En esta página
aprendes por qué existen y, sobre todo, a **convertir entre ellos paso a paso**.

Es la página más "matemática" del módulo, pero no asustes: con un poco de papel y lápiz se domina. Y
la vas a necesitar en todas partes (direcciones MAC, permisos, memoria, colores, análisis de red).

## Objetivos de aprendizaje

Al terminar esta página deberías ser capaz de:

- Explicar qué son los sistemas **binario, octal, decimal y hexadecimal** y por qué existen.
- Convertir **binario ↔ decimal** paso a paso.
- Convertir **decimal ↔ hexadecimal** paso a paso.
- Convertir **binario ↔ hexadecimal** agrupando en **nibbles**.
- Usar la tabla de equivalencias **0-15** de memoria (o casi).
- Realizar conversiones rápido con la terminal.

**Tiempo estimado: 90-120 min.**

## Requisitos previos

- **[00 · Ética y legalidad](../00-etica-y-legalidad.md)**.
- **[01 · Componentes del ordenador](01-componentes-del-ordenador.md)**: para entender qué es la
  memoria y los registros (usaremos sus conceptos como ejemplo).

## Explicación

### ¿Qué es un sistema de numeración?

Un **sistema de numeración posicional** representa un número usando una **base** (cuántos símbolos
distintos usa) y **posiciones** que valen potencias de esa base. El que usamos a diario es el
**decimal** (base 10). Los ordenadores usan:

| Sistema | Base | Símbolos | Uso típico |
| --- | --- | --- | --- |
| **Binario** | 2 | 0, 1 | Cómo trabaja el hardware. |
| **Octal** | 8 | 0-7 | Permisos en Linux (a veces), notación compacta. |
| **Decimal** | 10 | 0-9 | El nuestro, para leer. |
| **Hexadecimal** | 16 | 0-9 y A-F | Direcciones, MAC, colores, memoria. |

El **prefijo o subíndice** marca la base cuando hay dudas: escribimos `1010₂` o `0b1010` (binario),
`0x1F` (hexadecimal), `0o17` (octal). En el texto usaremos el subíndice cuando convenga.

### ¿Por qué existen el binario y el hexadecimal?

- **Binario**: es el idioma natural del electrónico. Un transistor está apagado (0) o encendido (1).
  Todo lo demás (imágenes, texto, vídeo) se traduce a 0s y 1s.
- **Hexadecimal**: escribir binario a mano es incómodo (`11111111` es fácil de confundir). Como
  **16 = 2⁴**, cada dígito hexadecimal equivale exactamente a **4 bits** (un **nibble**). Así, 8 bits
  (1 byte) se escriben con **2 dígitos** hexadecimales: `11111111` = `0xFF`. Compacto y sin errores.
- **Octal**: cada dígito octal son **3 bits**. Aparece en permisos de Linux (`chmod 644`) y en
  notaciones antiguas.

### Los pesos posicionales

Cada dígito se multiplica por la base elevada a su posición (de derecha a izquierda, empezando en 0):

- En **decimal**: `3 4 5` = 3·10² + 4·10¹ + 5·10⁰ = 300 + 40 + 5 = 345.
- En **binario**: `1 0 1 1` = 1·2³ + 0·2² + 1·2¹ + 1·2⁰ = 8 + 0 + 2 + 1 = 11.
- En **hexadecimal**: `2 F` = 2·16¹ + 15·16⁰ = 32 + 15 = 47 (recuerda que F = 15).

!!! tip "Truco: memoriza las potencias"
    Potencias de 2 muy usadas (de derecha a izquierda en un byte):
    `128 64 32 16 8 4 2 1`. Con eso conviertes binario a decimal **sumando** las que tienen un 1.

### Conversión binario → decimal (paso a paso)

Método: **sumar las potencias de 2** de las posiciones que tienen un `1`.

Ejemplo: convertir `1101₂` a decimal.

1. Coloca los pesos debajo de cada bit:

   ```text
   1     1     0     1
   2³    2²    2¹    2⁰
   8     4     2     1
   ```

2. Suma solo las posiciones con `1`:

   ```text
   bit 1 → 8   (2³)
   bit 1 → 4   (2²)
   bit 0 → 0   (2¹)  ← no se suma
   bit 1 → 1   (2⁰)
   Total = 8 + 4 + 0 + 1 = 13
   ```

Resultado: `1101₂ = 13₁₀`.

### Conversión decimal → binario (paso a paso)

Método recomendado: **divisiones sucesivas entre 2**, apuntando el resto, y luego leer los restos **de
abajo arriba**.

Ejemplo: convertir `13` a binario.

1. Divide entre 2 y anota el resto, hasta llegar a 0:

   ```text
   13 ÷ 2 = 6  resto 1
    6 ÷ 2 = 3  resto 0
    3 ÷ 2 = 1  resto 1
    1 ÷ 2 = 0  resto 1
   ```

2. Lee los restos **de abajo arriba**: `1 1 0 1`.

Resultado: `13₁₀ = 1101₂`.

Método alternativo: **restar la potencia de 2 más grande** que quepa. Para 13: cabe 8 (13−8=5);
cabe 4 (5−4=1); no cabe 2; cabe 1 (1−1=0). Posiciones usadas: 8, 4, 1 → `1101`. Mismo resultado.

### Conversión decimal → hexadecimal (paso a paso)

Igual que con el binario, pero **dividiendo entre 16**.

Ejemplo: convertir `200` a hexadecimal.

1. Divide entre 16:

   ```text
   200 ÷ 16 = 12  resto 8
    12 ÷ 16 = 0   resto 12
   ```

2. Convierte los restos a hexadecimal: 12 = `C`, 8 = `8`.

3. Lee de abajo arriba: `C` y luego `8` → `C8`.

Resultado: `200₁₀ = C8₁₆`.

### Conversión hexadecimal → decimal (paso a paso)

Multiplica cada dígito por la potencia de 16 de su posición.

Ejemplo: convertir `2F₁₆` a decimal.

1. Escribe los pesos:

   ```text
   2      F
   16¹    16⁰
   16     1
   ```

2. Convierte las letras: `F = 15`.

3. Multiplica y suma: (2 · 16) + (15 · 1) = 32 + 15 = 47.

Resultado: `2F₁₆ = 47₁₀`.

### Conversión binario ↔ hexadecimal (el truco de los nibbles)

Como **4 bits = 1 dígito hexadecimal**, agrupamos el binario **de 4 en 4 desde la derecha** (rellenando
con ceros a la izquierda si hace falta).

Ejemplo: convertir `11010110₂` a hexadecimal.

1. Agrupa en nibbles desde la derecha: `1101` y `0110`.
2. Traduce cada nibble: `1101 = D`, `0110 = 6`.
3. Junta: `D6`.

Resultado: `11010110₂ = D6₁₆`.

Y al revés: convertir `A3₁₆` a binario expandiendo cada dígito a 4 bits.

- `A = 1010`
- `3 = 0011`
- Resultado: `1010 0011` → `10100011₂`.

!!! tip "Regla de oro del nibble"
    **1 dígito hexadecimal = 4 bits = 1 nibble**. **2 dígitos hexadecimales = 8 bits = 1 byte**.
    Si dominas esto, las conversiones binario↔hexadecimal son instantáneas y no necesitas dividir.

### Tabla de equivalencias (0-15)

| Decimal | Binario | Octal | Hex |
| --- | --- | --- | --- |
| 0 | 0000 | 0 | 0 |
| 1 | 0001 | 1 | 1 |
| 2 | 0010 | 2 | 2 |
| 3 | 0011 | 3 | 3 |
| 4 | 0100 | 4 | 4 |
| 5 | 0101 | 5 | 5 |
| 6 | 0110 | 6 | 6 |
| 7 | 0111 | 7 | 7 |
| 8 | 1000 | 10 | 8 |
| 9 | 1001 | 11 | 9 |
| 10 | 1010 | 12 | A |
| 11 | 1011 | 13 | B |
| 12 | 1100 | 14 | C |
| 13 | 1101 | 15 | D |
| 14 | 1110 | 16 | E |
| 15 | 1111 | 17 | F |

## Ejemplos prácticos

Puedes comprobar tus conversiones con la **terminal** (bash). Estos comandos son **de solo lectura**.

```bash
# Binario -> decimal (n#numero, donde n es la base)
echo $((2#1101))          # 13

# Hexadecimal -> decimal
echo $((16#2F))           # 47
echo $((0x2F))            # 47   (0x también sirve)

# Decimal -> hexadecimal (minúsculas)
printf '%x\n' 200         # c8

# Hexadecimal -> decimal con printf
printf '%d\n' 0x2F        # 47

# Decimal -> octal
printf '%o\n' 15          # 17

# Decimal -> binario (bash no tiene %b directo: usa un bucle)
n=13; b=""; while [ "$n" -gt 0 ]; do b="$((n % 2))$b"; n=$((n / 2)); done; echo "$b"   # 1101
```

- `$((2#1101))` — interpreta `1101` en **base 2** y devuelve su valor decimal (`13`).
- `$((16#2F))` y `$((0x2F))` — ambas formas leen el número en **base 16** (`47`).
- `printf '%x\n' 200` — imprime `200` en **hexadecimal** (`c8`, en minúsculas).
- `printf '%d\n' 0x2F` — imprime un hexadecimal en **decimal** (`47`).
- `printf '%o\n' 15` — imprime en **octal** (`17`).
- El mini-bucle `while` construye el binario **de un decimal** (útil si no tienes otra herramienta).

Otro atajo si tienes **Python**:

```bash
python3 -c "print(bin(13), oct(13), hex(13))"   # 0b1101 0o15 0xd
```

## Errores comunes

| Error | Por qué está mal | Solución |
| --- | --- | --- |
| Leer los restos de arriba abajo. | El orden se invierte. | Lee **de abajo arriba** (el último resto es el dígito más significativo). |
| Olvidar que en hex A-F valen 10-15. | `A` no es "diez" escrito raro: **A = 10**, `F = 15`. | Memoriza la tabla 0-15. |
| Agrupar nibbles desde la izquierda. | El bit menos significativo está a la derecha. | Agrupa **de 4 en 4 desde la derecha**; rellena con ceros a la izquierda. |
| Confundir `1000₂` con "mil". | Es 8 en decimal. | Piensa siempre en **potencias de 2**, no en decimal. |
| Mezclar bases sin darse cuenta. | `10` es 2, 8, 10 o 16 según la base. | Usa prefijos (`0b`, `0x`, `0o`) o subíndices. |
| Comerse un cero a la izquierda. | `0110` no es lo mismo que `110`. | Los ceros a la izquierda **sí cuentan** en las agrupaciones. |

## Ejercicios

Resuelve a mano y comprueba con la terminal.

1. **Binario → decimal.** Convierte `1011₂` a decimal.

   ??? success "Solución"
       Pesos: `8 4 2 1`. Bits `1 0 1 1` → sumamos 8 + 0 + 2 + 1 = **11**.
       Compruébalo: `echo $((2#1011))` → `11`.

2. **Decimal → binario.** Convierte `13` a binario.

   ??? success "Solución"
       Divisiones: 13÷2=6 r1; 6÷2=3 r0; 3÷2=1 r1; 1÷2=0 r1. Restos de abajo arriba: `1 1 0 1` →
       **`1101₂`**. Comprueba: `echo $((2#1101))` → `13`.

3. **Decimal → hexadecimal.** Convierte `200` a hexadecimal.

   ??? success "Solución"
       200÷16 = 12 r8; 12÷16 = 0 r12. Restos 12 (C) y 8 → **`C8₁₆`**.
       Comprueba: `printf '%x\n' 200` → `c8`.

4. **Hexadecimal → decimal.** Convierte `2F₁₆` a decimal.

   ??? success "Solución"
       (2 · 16) + (15 · 1) = 32 + 15 = **47**. Comprueba: `printf '%d\n' 0x2F` → `47`.

5. **Binario → hexadecimal.** Convierte `11010110₂` a hexadecimal usando nibbles.

   ??? success "Solución"
       Agrupa desde la derecha: `1101` `0110`. `1101 = D`, `0110 = 6` → **`D6₁₆`**.
       Comprueba: `printf '%x\n' $((2#11010110))` → `d6`.

6. **Hexadecimal → binario.** Convierte `A3₁₆` a binario.

   ??? success "Solución"
       Expande cada dígito a 4 bits: `A = 1010`, `3 = 0011` → **`10100011₂`**.
       Comprueba: `echo $((2#10100011))` → `163` y `printf '%d\n' 0xA3` → `163`. Coinciden.

7. **Octal → decimal.** Convierte `17₈` a decimal.

   ??? success "Solución"
       (1 · 8) + (7 · 1) = 8 + 7 = **15**. Comprueba: `echo $((8#17))` → `15` (o `printf '%o\n' 15`
       da `17`).

8. **Un byte completo.** Convierte `11111111₂` a decimal y a hexadecimal.

   ??? success "Solución"
       Decimal: suma de todos los pesos de un byte (128+64+32+16+8+4+2+1) = **255**.
       Hexadecimal: `1111` `1111` → `F` `F` → **`FF₁₆`**. Comprueba: `printf '%x\n' 255` → `ff`.

9. **Vuelta completa.** Convierte `255` decimal a binario y a hexadecimal, y verifica que coincide con
   el ejercicio anterior.

   ??? success "Solución"
       Binario: 255 = 128+64+32+16+8+4+2+1 → **`11111111₂`**. Hexadecimal: 255 = `FF₁₆`.
       Coincide con el ejercicio 8. Los tres (`255`, `11111111`, `FF`) son **el mismo número**.

10. **Reto.** ¿Cuánto vale `1A₁₆` en decimal y en binario?

    ??? success "Solución"
        Decimal: (1 · 16) + (10 · 1) = **26**. Binario: `1 = 0001`, `A = 1010` → **`00011010₂`** (o
        `11010₂` sin los ceros a la izquierda). Comprueba: `printf '%d\n' 0x1A` → `26`.

## Resumen

- Los ordenadores usan **binario**; el **hexadecimal** (y el **octal**) son atajos cómodos para
  escribir binario.
- **Binario → decimal**: suma las potencias de 2 de las posiciones con `1`.
- **Decimal → binario/hex**: divide entre 2 (o 16) y lee los restos **de abajo arriba**.
- **Hex → decimal**: multiplica cada dígito por la potencia de 16 correspondiente.
- **Binario ↔ hex**: agrupa/expande en **nibbles** (4 bits = 1 dígito hex; 1 byte = 2 dígitos hex).
- Los dígitos hexadecimales **A-F** valen **10-15**.

## Checklist

- [ ] Sé pasar de **binario a decimal** sin calculadora.
- [ ] Sé pasar de **decimal a binario** con divisiones sucesivas.
- [ ] Sé convertir **decimal ↔ hexadecimal**.
- [ ] Uso el truco de los **nibbles** para binario ↔ hex.
- [ ] Tengo memorizada (o casi) la tabla **0-15**.
- [ ] Puedo comprobar conversiones con `printf` y `$((...))` en la terminal.

## Para ir más allá

- [man7.org](https://man7.org) — manuales de `printf`, `bash` y utilidades de conversión. **Gratis**,
  inglés (EN).
- [MDN Web Docs](https://developer.mozilla.org) — trasfondo sobre representación de números y
  notaciones. **Gratis**, varios idiomas (incluye español).
- [Glosario de UJACKING](../../glosario.md) — binario, byte, nibble y hexadecimal en claro. **Gratis**,
  español.

## Siguiente paso

Domina el hexadecimal: lo vas a ver **constantemente** en direcciones MAC, colores, permisos y memoria.
El siguiente paso es **[03 · Bits, bytes y representación](03-bits-bytes-y-representacion.md)**.
