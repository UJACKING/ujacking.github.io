# OverTheWire

**El mejor gimnasio de Linux de la red, y es gratis.** OverTheWire ofrece una colección de "wargames":
retos por niveles a los que te conectas por **SSH**. El más famoso es **Bandit**, la forma clásica de
aprender a moverse por la línea de comandos jugando. Si eres nuevo en Linux, empieza aquí.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Explicar qué son los wargames de OverTheWire y cómo se juega a Bandit.
- Conectarte por SSH al servidor de Bandit y resolver los primeros niveles.
- Transferir lo aprendido (usuarios, permisos, búsqueda de ficheros) a tu propio sistema.
- Saber por qué Bandit es el punto de partida ideal antes de HTB o TryHackMe.

**Tiempo estimado:** 30-45 min para leer; Bandit completo, varias tardes (y merece la pena).

## Requisitos previos

- [Índice del módulo](index.md): comparativa de plataformas.
- [04 · Terminal, shell y consola](../04-bash/01-terminal-shell-y-consola.md): qué es un shell.
- [02 · Comandos esenciales](../04-bash/02-comandos-esenciales.md): al menos `ls`, `cd`, `cat`.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md).

## Explicación

### ¿Qué es OverTheWire?

OverTheWire es un proyecto **gratuito** que lleva años publicando *wargames*: series de niveles donde
cada uno te enseña un concepto nuevo mediante un pequeño enigma que se resuelve en la terminal. No hay
interfaz gráfica bonita ni pistas automáticas: **es Linux de verdad**.

Cada wargame se centra en un tema. Los más conocidos:

| Wargame | Tema | Nivel |
| --- | --- | --- |
| **Bandit** | Fundamentos de Linux y la shell | Principiante total |
| **Leviathan** | Linux básico un poco más allá | Principiante |
| **Natas** | Seguridad web | Principiante → medio |
| **Krypton** | Criptografía clásica | Principiante → medio |
| **Narnia / Behemoth** | Explotación de binarios | Medio → avanzado |
| **Utumno / Maze / Vortex** | Retos de seguridad variados | Avanzado |

!!! warning "PENDIENTE (TODO-UJACKING)"
    La lista de wargames disponibles y su estado pueden cambiar. Verifica cuáles siguen activos y su
    temática actual en [https://overthewire.org](https://overthewire.org) antes de publicar.

### Bandit: empieza aquí si eres nuevo en Linux

**Bandit** está diseñado exactamente para alguien que nunca ha usado una terminal. Cada nivel te da un
usuario y una contraseña; entras por SSH, resuelves el reto (encontrar un fichero, leerlo, usar un
comando nuevo…) y **la contraseña del siguiente nivel** es tu recompensa.

No hay trampa: son decenas de niveles, cada uno con una lección práctica:

- Navegar y leer ficheros.
- Buscar ficheros por nombre, permisos, tamaño o propietario.
- Entender `chmod`, `chown`, enlaces, `SUID`.
- Tuberías, redirecciones y `grep`.
- Conexiones de red básicas (`nc`, `ssh`).

Es, con diferencia, la mejor inversión de tiempo si vienes de cero.

### Cómo se juega (por SSH)

El juego es siempre el mismo patrón:

1. Entras por SSH al siguiente usuario (empieza en `bandit0`).
2. Lees el enunciado del nivel en la web de OverTheWire.
3. Usas la terminal para resolverlo.
4. Encuentras la contraseña del nivel siguiente.
5. Repites.

El servidor es `bandit.labs.overthewire.org` y el **puerto no es el 22 por defecto**, sino el **2220**.
Por eso hay que indicarlo con `-p`.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Confirma en [https://overthewire.org](https://overthewire.org) el host y el puerto vigentes antes
    de publicar, y **no publiques contraseñas concretas**: cambian y el reto pierde sentido. Deja
    siempre el enlace a la web oficial.

!!! danger "Aviso ético"
    OverTheWire te autoriza a atacar **sus** servidores de juego. Copiar lo aprendido a cualquier otro
    sistema es delito. Esta es tu zona de entrenamiento; el mundo real tiene dueños.

## Ejemplos prácticos

**1. Conectarte al primer nivel (bandit0).** La contraseña inicial se indica en la web (para `bandit0`
suele ser el propio nombre; confírmalo allí):

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Explicación línea a línea:

- `ssh` — programa para abrir una sesión remota cifrada.
- `bandit0@bandit.labs.overthewire.org` — usuario `bandit0` en el host del juego.
- `-p 2220` — el puerto **2220** en lugar del 22 por defecto.

Al entrar por primera vez te pedirá aceptar la clave del servidor (`yes`) y la contraseña.

**2. Resolver el nivel 0.** El objetivo típico es leer un fichero llamado `readme` en el directorio
personal:

```bash
ls
cat readme
```

```text
<la contrasena del nivel bandit1>   (la salida cambia; NO es un valor fijo)
```

Anota esa contraseña: es la del siguiente nivel.

**3. Pasar al siguiente nivel.** Sales y entras con el usuario nuevo:

```bash
exit
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

**4. Ejemplo de nivel intermedio: buscar un fichero por permisos.** Uno de los niveles clásicos pide
encontrar un fichero con unas características concretas. Estas herramientas te servirán:

```bash
find / -type f -size 1033c 2>/dev/null      # ficheros de 1033 bytes
find / -user bandit7 -group bandit6 2>/dev/null   # por propietario y grupo
```

Explicación:

- `find / -type f` — busca solo ficheros a partir de la raíz.
- `-size 1033c` — tamaño de exactamente 1033 bytes (`c` = bytes).
- `2>/dev/null` — oculta los errores de "permiso denegado" para ver limpio el resultado.

**5. Crear un directorio temporal para experimentar** (algunos niveles lo piden):

```bash
mktemp -d
```

```text
/tmp/tmp.Ab3xY9z   (salida de ejemplo)
```

`mktemp -d` crea un directorio temporal con nombre único. Es la forma segura de trabajar sin pisar
ficheros ajenos.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| "Connection refused" | Usaste el puerto 22 | Recuerda `-p 2220` |
| "Permission denied" al leer un fichero | No lo lees como el usuario correcto | Revisa qué usuario puede leerlo |
| Pierdo las contraseñas | No las guardas | Apunta cada una en tu Markdown antes de salir |
| "Me sale un fichero que no se leer" | Es un fichero con guiones o caracteres raros | Usa `cat ./-nombre` o `cat -- -nombre` |
| Avanzo copiando de foros | No aprendes | Pide pista, no solución; el reto es para ti |

## Ejercicios

1. **Conéctate a bandit0.** Entra por SSH al primer nivel y ejecuta `whoami` y `pwd`.

    ??? success "Solución"
        ```bash
        ssh bandit0@bandit.labs.overthewire.org -p 2220
        whoami
        pwd
        ```

        `whoami` debe devolver `bandit0` y `pwd` un directorio bajo `/home/bandit0` (salida de
        ejemplo). Si `ssh` falla con "connection refused", te falta el `-p 2220`.

2. **Resuelve los niveles 0 y 1** y guarda las contraseñas obtenidas en un fichero local.

    ??? success "Solución"
        Procedimiento: entra, lee lo que pida el nivel, copia la contraseña, `exit`, y apúntala:

        ```bash
        printf 'bandit1: <contrasena>\nbandit2: <contrasena>\n' >> ~/apuntes-ciberseguridad/bandit.txt
        ```

        **No publicamos las contraseñas reales**: cambian y spoilean el reto.

3. **Localiza un fichero por tamaño.** En tu propio sistema (no en Bandit), busca todos los ficheros
   de exactamente 0 bytes dentro de `/etc`.

    ??? success "Solución"
        ```bash
        sudo find /etc -type f -size 0c 2>/dev/null
        ```

        Puede no haber ninguno o varios (salida variable). Lo importante es dominar la sintaxis
        `-size Nc`.

4. **Usa una tubería.** En Bandit (o en tu máquina) cuenta cuántos usuarios hay en `/etc/passwd`.

    ??? success "Solución"
        ```bash
        wc -l < /etc/passwd
        ```

        O con tubería:

        ```bash
        cat /etc/passwd | wc -l
        ```

        Ambas dan el mismo número (el total de usuarios del sistema).

5. **Documenta el nivel más difícil que hayas hecho.** Describe el problema, el comando clave y la
   lección.

    ??? success "Solución"
        Ejemplo de formato válido:

        ```markdown
        ## Bandit nivel 6
        Problema: encontrar un fichero en todo el sistema con dueño y grupo concretos.
        Comando clave: find / -user bandit7 -group bandit6 -type f 2>/dev/null
        Lección: "2>/dev/null" limpia el ruido de errores de permisos.
        ```

6. **Salta de nivel a nivel sin perder el hilo.** Crea un pequeño script que imprima tu lista de
   contraseñas numeradas (ideal para repasar luego).

    ??? success "Solución"
        ```bash
        nl -ba ~/apuntes-ciberseguridad/bandit.txt
        ```

        `nl -ba` numera las líneas. Así ves de un vistazo en qué nivel vas.

## Resumen

- OverTheWire es **gratis** y ofrece wargames que se juegan por **SSH**.
- **Bandit** es el punto de partida ideal si eres nuevo en Linux.
- El patrón es: entras → resuelves → obtienes la contraseña del siguiente nivel.
- Se conecta con `ssh usuario@host -p 2220`.
- Aprendes de verdad porque **es la terminal de verdad**, sin botones.

## Checklist

- [ ] Sé qué es un wargame y qué es OverTheWire.
- [ ] Me he conectado a `bandit0` por SSH.
- [ ] He resuelto los primeros niveles de Bandit.
- [ ] Guardo cada contraseña en un fichero propio.
- [ ] Relaciono cada nivel con un comando que ya sé usar.
- [ ] Entiendo que practicar aquí es legal y en otro sitio no.

## Para ir más allá

- **OverTheWire** — Wargames oficiales. Nivel: principiante-avanzado. Idioma: (EN). **Gratis**.
  [https://overthewire.org](https://overthewire.org)
- **Chuleta de Bash** (UJACKING) — Repaso de comandos para Bandit.
  [Chuleta de Bash](../04-bash/05-chuleta-bash.md)
- **Linux · usuarios y permisos** (UJACKING) — La teoría detrás de muchos niveles de Bandit.
  [Linux · usuarios y permisos](../03-sistemas-operativos/02-linux-usuarios-y-permisos.md)

## Siguiente paso

Cuando la terminal deje de darte miedo, toca seguridad web: el mejor recurso **gratuito** que hay es
**[PortSwigger Web Security Academy](04-portswigger-web-security-academy.md)**.
