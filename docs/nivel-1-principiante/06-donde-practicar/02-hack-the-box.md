# Hack The Box

**El siguiente escalón después de lo guiado.** Hack The Box (HTB) es una de las plataformas de
pentesting más reconocidas. Sus máquinas y laboratorios están pensados para gente que ya se maneja con
la terminal, y su parte educativa (Academy) y su puerta de entrada (Starting Point) la hacen apta para
principiantes decididos.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Explicar qué ofrece HTB y en qué se diferencia de TryHackMe.
- Entender qué es **Starting Point** y por qué es tu punto de entrada.
- Distinguir a grandes rasgos qué hay **gratis** y qué requiere suscripción, sin depender de precios
  concretos.
- Saber **cuándo** es buen momento para empezar en HTB y cuándo aún no.

**Tiempo estimado:** 40-60 min de lectura; tu primera máquina de Starting Point, 1-3 h.

## Requisitos previos

- [Índice del módulo](index.md): comparativa de plataformas.
- [OverTheWire](03-overthewire.md): si aún no te manejas por SSH, empieza por ahí.
- [02 · Herramientas de diagnóstico](../02-redes/10-herramientas-de-diagnostico.md): lo que aplicarás
  al enumerar máquinas.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md): imprescindible antes de escanear nada.

## Explicación

### ¿Qué es Hack The Box?

HTB es una plataforma de práctica de hacking ético con varias "puertas de entrada":

| Parte de HTB | Qué es | Para quién |
| --- | --- | --- |
| **Starting Point** | Máquinas muy guiadas, con pistas paso a paso | Principiantes |
| **Machines (labs)** | Máquinas objetivo que debes comprometer tú solo | Nivel medio/avanzado |
| **Academy** | Módulos teórico-prácticos tipo curso | Quien quiere base sólida |
| **Challenges** | Retos cortos (web, cripto, reversing…) | Practicar una habilidad concreta |
| **Pro Labs / CTF** | Entornos grandes y competiciones | Nivel avanzado |

### Starting Point: tu primera parada

**Starting Point** es el conjunto de máquinas pensadas para quien llega nuevo. Se organizan por
niveles (empezando por el "Tier 0", muy básico) y traen **guía** para que no te quedes bloqueado. La
idea es que aprendas la metodología completa: reconocimiento, escaneo, acceso y escalada.

Si es tu primera vez en HTB, **no toques las máquinas sueltas**: empieza por Starting Point.

### Academy: cursos con laboratorio

HTB Academy son módulos de formación (conceptos + ejercicios) que van desde "fundamentos" hasta
especializaciones (web, Active Directory, explotación, etc.). Es más "clase" que "reto libre".

Sobre el coste, en términos generales:

- HTB Academy ofrece **algunos módulos gratuitos** y el resto requiere una **suscripción de pago**.
- Los **labs de máquinas** tienen un **acceso gratuito limitado** (con restricciones) y un plan de
  pago con más comodidades.

!!! warning "PENDIENTE (TODO-UJACKING)"
    No inventamos precios ni límites. Antes de publicar, verifica en
    [https://www.hackthebox.com](https://www.hackthebox.com) cuántas máquinas incluye el plan gratuito
    hoy, el número de "resets" permitidos y qué módulos de Academy siguen siendo gratuitos.

### ¿Cuándo empezar en HTB?

Empieza en HTB **cuando cumples esto**:

- [ ] Te mueves por la terminal de Linux sin mirar la chuleta a cada paso.
- [ ] Entiendes qué es una IP, un puerto y un servicio (módulo 02).
- [ ] Has completado habitaciones guiadas en [TryHackMe](01-tryhackme.md) o similar.
- [ ] Sabes usar `nmap` al menos a nivel básico.

Si has marcado las cuatro, adelante con **Starting Point**. Si no, vuelve a
[OverTheWire](03-overthewire.md) y a [TryHackMe](01-tryhackme.md) un par de semanas más. No hay prisa.

!!! danger "Aviso ético"
    En HTB tienes **autorización explícita** para atacar sus máquinas. Fuera de ahí, no. Nunca uses
    lo aprendido contra sistemas que no sean tuyos o de una plataforma que lo permita por escrito.

## Ejemplos prácticos

**1. Preparar la conexión.** HTB usa una VPN propia igual que TryHackMe. Descarga tu `.ovpn` desde el
panel y conéctalo:

```bash
sudo openvpn --config ~/Descargas/htb_tun.ovpn
```

```text
... Initialization Sequence Completed
```

**2. Comprobar que ves la máquina objetivo.** Cuando lances una máquina en Starting Point, te dará una
IP. Comprueba conectividad:

```bash
ping -c 2 10.129.12.34
```

```text
64 bytes from 10.129.12.34: icmp_seq=1 ttl=63 time=24.1 ms
... (salida de ejemplo)
```

Si `ping` no responde pero la máquina está "Running" en el panel, puede tener el ping bloqueado: prueba
directamente con `nmap`.

**3. Primer escaneo (metodología real de HTB).**

```bash
nmap -sC -sV -oA startingpoint_primera 10.129.12.34
```

Explicación línea a línea del comando:

- `nmap` — la herramienta de escaneo de puertos.
- `-sC` — ejecuta los **scripts por defecto** (detección básica de servicios y configuraciones).
- `-sV` — detecta la **versión** de cada servicio.
- `-oA startingpoint_primera` — guarda la salida en tres formatos con ese nombre base.
- `10.129.12.34` — la IP de la máquina (la tuya será distinta).

A partir de ahí: busca el servicio interesante (una web, un FTP, un SSH…), investígalo y sigue las
pistas de Starting Point.

**4. Apuntar los resultados.** Anota en tu repositorio cada paso, porque en HTB el valor está en el
proceso:

```bash
mkdir -p ~/apuntes-ciberseguridad/htb && cd $_
printf '# HTB Starting Point - Máquina 1\n' > maquina1.md
```

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| Ir directo a máquinas sueltas | Crees que Starting Point es "muy fácil" | Haz Starting Point primero, enseña metodología |
| "La máquina no responde" | VPN caída o ping bloqueado | Revisa VPN; usa `nmap -Pn` |
| Copiar el writeup entero | Te bloqueas en cuanto cambia una línea | Mira pistas una a una, no la solución |
| Perder la flag | HTB da la flag al "comprometer" del todo | Sigue hasta el final; la flag suele estar en `root` |
| Confundir Academy con labs | Son cosas distintas | Academy = cursos; labs = máquinas |

## Ejercicios

1. **Crea la cuenta y localiza Starting Point.** Entra en HTB, crea cuenta y encuentra la sección
   Starting Point. Anota cuántos niveles (Tiers) ves.

    ??? success "Solución"
        Deberías ver los Tiers empezando por el 0. Anota **los nombres reales de los niveles** que
        aparezcan hoy (cambian con el tiempo). El objetivo es que sepas dónde está tu punto de
        entrada, no memorizar un número concreto.

2. **Conecta la VPN y comprueba tu IP.**

    ??? success "Solución"
        ```bash
        sudo openvpn --config ~/Descargas/htb_tun.ovpn
        ip a | grep tun0 -A2
        ```

        Debe aparecer una IP en la interfaz `tun0` (salida de ejemplo). Sin eso, ninguna máquina de
        HTB te responderá.

3. **Resuelve la primera máquina de Starting Point.** Complétala y guarda la flag de usuario y la de
   root en tus apuntes.

    ??? success "Solución"
        No damos la solución (sería hacerte trampa). La comprobación es: la máquina aparece como
        **Owned** en tu perfil y tienes ambas flags guardadas. Si te atascas, usa las pistas
        integradas **de una en una**.

4. **Escribe el "árbol de decisiones" de tu máquina.** Enumera en orden las decisiones que tomaste
   (qué puerto miraste primero, por qué, qué probaste…).

    ??? success "Solución"
        Ejemplo de respuesta válida:

        ```markdown
        1. Port scan -> 22 (SSH), 80 (HTTP)
        2. La web parece lo más débil -> la abro en el navegador
        3. Encuentro un directorio raro -> lo investigo
        4. Consigo credenciales -> pruebo SSH
        5. Escalada: busco ficheros SUID
        ```

        Los pasos concretos dependen de la máquina; lo evaluable es que tu razonamiento sea **coherente
        y en orden**.

5. **Diferencia Academy de labs.** Escribe una frase explicando para qué sirve cada uno y pon un
   ejemplo de cuándo usarías cada uno.

    ??? success "Solución"
        - **Academy:** aprender un tema con teoría guiada (p. ej. "fundamentos de redes").
        - **Labs:** poner a prueba lo aprendido resolviendo una máquina (p. ej. comprometer un
          servidor web vulnerable).

6. **Decide si es tu momento.** Rellena el checklist de "¿Cuándo empezar en HTB?" de esta página y
   decide, con honestidad, si empiezas ahora o sigues un par de semanas en TryHackMe.

    ??? success "Solución"
        Respuesta válida: si has marcado las **cuatro** casillas, empieza; si no, no pasa nada por
        esperar. Reconocer que aún no es tu momento **también** es una respuesta correcta y te ahorra
        frustración.

## Resumen

- HTB es el "siguiente nivel" tras lo guiado, con Starting Point como puerta de entrada.
- **Starting Point** enseña metodología con pistas; **Academy** son cursos; los **labs** son retos.
- Hay acceso **gratuito limitado** y planes de pago; verifica las condiciones actuales.
- Empieza cuando domines terminal, IP/puertos y `nmap` básico.
- HTB te autoriza a atacar **sus** máquinas. Y solo esas.

## Checklist

- [ ] Tengo cuenta en HTB.
- [ ] Sé qué es Starting Point y he localizado el Tier inicial.
- [ ] He conectado la VPN correctamente.
- [ ] He empezado (o completado) mi primera máquina de Starting Point.
- [ ] Tengo un writeup propio guardado en mi repositorio.
- [ ] Entiendo la diferencia entre Academy, labs y challenges.

## Para ir más allá

- **Hack The Box** — Plataforma oficial. Nivel: medio-avanzado. Idioma: (EN). **Freemium**.
  [https://www.hackthebox.com](https://www.hackthebox.com)
- **Nmap en profundidad** (Nivel 2 de UJACKING) — Cuando el `nmap` básico se te quede corto.
  [Nmap en profundidad](../../nivel-2-medio/05-nmap-en-profundidad.md)
- **Metodología de pentesting** (Nivel 2 de UJACKING) — El proceso ordenado detrás de cada máquina.
  [Metodología de pentesting](../../nivel-2-medio/06-metodologia-de-pentesting.md)

## Siguiente paso

Antes de saltar a retos más duros, conviene reforzar los **fundamentos de Linux por SSH**:
**[OverTheWire](03-overthewire.md)**.
