# Checklist y autoevaluación del Nivel 1

**El examen de tu propio aprendizaje.** Aquí tienes dos cosas: la **checklist completa** de todo el
Nivel 1, para comprobar casilla a casilla que no te falta nada, y un **test de 40 preguntas** con
respuestas razonadas. Al final, un criterio claro para saber si estás listo para el Nivel 2.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Revisar de un vistazo **todo** lo aprendido en el Nivel 1.
- Detectar tus puntos débiles con honestidad.
- Medir tu nivel con un test de 40 preguntas y saber interpretarlo.
- Decidir con criterio si pasas al Nivel 2 o repasas antes.

**Tiempo estimado:** 60-90 min (checklist + test + revisión de fallos).

## Requisitos previos

Lo ideal es haber completado los ocho módulos del nivel:

- [00 · Ética y legalidad](00-etica-y-legalidad.md)
- [01 · Arquitectura de ordenadores](01-arquitectura-de-ordenadores/index.md)
- [02 · Redes](02-redes/index.md)
- [03 · Sistemas operativos](03-sistemas-operativos/index.md)
- [04 · Bash](04-bash/index.md)
- [05 · Git y GitHub](05-git-y-github/index.md)
- [06 · Dónde practicar](06-donde-practicar/index.md)
- [07 · Primer laboratorio](07-primer-laboratorio.md)

## Explicación

### Cómo usar esta página

1. **Haz primero la checklist**, módulo a módulo, marcando solo lo que puedas demostrar (no lo que
   "más o menos" recuerdes).
2. **Haz luego el test** de 40 preguntas **sin mirar apuntes**. Tarda lo que necesites.
3. **Corrige** y lee las respuestas razonadas de las que hayas fallado.
4. **Decide** con el criterio de "cuándo pasar al Nivel 2".

!!! tip "Sé honesto contigo mismo"
    Marcar una casilla que no te corresponde no engaña a nadie salvo a ti. Este test no se lo enseñas
    a nadie: es una herramienta, no una nota.

### Criterio orientativo: ¿cuándo paso al Nivel 2?

- **90-100 % de aciertos:** tienes la base sólida. Al Nivel 2 sin dudarlo.
- **70-89 %:** estás listo. Repasa **solo** los temas que fallaste y adelante.
- **50-69 %:** repasa los módulos flojos y **repite el test** en unos días.
- **Menos del 50 %:** vuelve a los módulos del Nivel 1. Con calma: sin base, el Nivel 2 cuesta el
  doble.

!!! note "El 70 % es orientativo"
    No es una nota de corte oficial. Es una referencia práctica. También cuenta la checklist: si la
    tienes completa y el test te da un 65 %, probablemente estés listo igualmente.

## Checklist completa del Nivel 1

### 00 · Ética y legalidad

- [ ] Sé qué es el hacking ético y en qué se diferencia del delito informático.
- [ ] Entiendo que necesito **autorización** para tocar cualquier sistema que no sea mío.
- [ ] Conozco las reglas de mi laboratorio (aislado, sin Internet, propio).
- [ ] Sé qué hacer si encuentro una vulnerabilidad real (reportarla por el canal correcto).

### 01 · Arquitectura de ordenadores

- [ ] Sé qué hacen CPU, memoria RAM y almacenamiento.
- [ ] Entiendo qué es un bit, un byte y sus múltiplos (KB, MB, GB).
- [ ] Convierto entre binario, decimal y hexadecimal sin calculadora (números pequeños).
- [ ] Entiendo qué es un sistema operativo y para qué sirve.
- [ ] Sé qué es la virtualización y qué es un hypervisor.
- [ ] Sigo el proceso de arranque de un ordenador a grandes rasgos.

### 02 · Redes

- [ ] Explico el modelo OSI y el modelo TCP/IP y sus capas.
- [ ] Distingo una dirección IP de una dirección MAC.
- [ ] Identifico IPs privadas (10.x, 172.16-31.x, 192.168.x) frente a públicas.
- [ ] Calculo la máscara, la red y el rango de hosts de un prefijo `/24` (y similares).
- [ ] Sé qué hace un switch y qué hace un router.
- [ ] Explico la diferencia entre TCP y UDP.
- [ ] Conozco los puertos de servicios habituales (22, 53, 80, 443, 3306…).
- [ ] Sé qué hacen DNS, DHCP y HTTP/HTTPS a grandes rasgos.
- [ ] Uso `ping`, `traceroute`, `ip`/`ifconfig` y `nslookup`/`dig` para diagnosticar.
- [ ] Sé capturar tráfico con Wireshark y leer una trama básica.

### 03 · Sistemas operativos

- [ ] Me muevo por Linux: `ls`, `cd`, `pwd`, `cp`, `mv`, `rm`, `cat`, `less`.
- [ ] Entiendo usuarios, grupos y permisos (`rwx`, `chmod`, `chown`).
- [ ] Sé leer la salida de `ps`, `top` y revisar logs básicos.
- [ ] Me manejo mínimamente en Windows (rutas, panel, `cmd`/PowerShell básicos).
- [ ] Sé qué distro de hacking usar (Kali/Parrot) y por qué.
- [ ] Tengo Kali o Parrot instalado en una máquina virtual.
- [ ] Tengo montada mi red virtual aislada.
- [ ] Tengo una máquina objetivo que responde en la red.

### 04 · Bash

- [ ] Distingo terminal, shell y consola.
- [ ] Uso las tuberías (`|`) y las redirecciones (`>`, `>>`, `<`).
- [ ] Filtro con `grep`, `head`, `tail`, `wc`, `sort`, `uniq`.
- [ ] Escribo un script en Bash con variables y un `if`.
- [ ] Le doy permisos de ejecución a un script (`chmod +x`) y lo ejecuto.
- [ ] Tengo mi propia chuleta de comandos a mano.

### 05 · Git y GitHub

- [ ] Explico qué es el control de versiones y para qué sirve.
- [ ] Uso `git init`, `add`, `commit`, `status` y `log`.
- [ ] Creo ramas, hago merge y resuelvo un conflicto sencillo.
- [ ] Uso remotos: `clone`, `push`, `pull`.
- [ ] Sé qué es un fork y qué es un Pull Request.
- [ ] He publicado algo con GitHub Pages.

### 06 · Dónde practicar

- [ ] Sé elegir plataforma según nivel, objetivo y presupuesto.
- [ ] Distingo Gratis, Freemium y De pago en las plataformas vistas.
- [ ] Tengo cuenta en al menos una plataforma de práctica.
- [ ] He practicado en OverTheWire Bandit o similar.
- [ ] He hecho alguna habitación guiada (TryHackMe) o su equivalente.
- [ ] He probado algún laboratorio de seguridad web (PortSwigger).
- [ ] Sé qué es un CTF y he mirado el calendario de CTFtime.

### 07 · Primer laboratorio

- [ ] Monto un laboratorio con atacante, víctima y red aislada.
- [ ] Descubro hosts vivos con `nmap -sn`.
- [ ] Escaneo puertos y detecto versiones con `nmap -sV -sC`.
- [ ] Hago un escaneo completo de puertos (`-p-`).
- [ ] Verifico servicios con `curl` y `nc`.
- [ ] Escribo un informe de pentesting con evidencia.
- [ ] Subo mi informe a Git.

## Test de autoevaluación (40 preguntas)

Elige **una** respuesta por pregunta. Al final están las respuestas razonadas.

**1.** ¿Cuándo es legal escanear una red con Nmap?
a) Nunca. b) Cuando tienes autorización por escrito del propietario o es tu laboratorio/plataforma
autorizada. c) Cuando no haces daño. d) Cuando usas `-sS`.

**2.** ¿Qué caracteriza al hacking ético?
a) Atacar cualquier cosa por curiosidad. b) Autorización, no causar daño y reportar. c) Usar Kali.
d) Tener buen antivirus.

**3.** Encuentras una vulnerabilidad en la web de una tienda. ¿Qué haces?
a) Explotarla sin más. b) Publicarla en redes. c) Reportarla por el canal responsable.
d) Ignorarla.

**4.** ¿Qué significa "pentest"?
a) Un test de rendimiento. b) Una prueba de penetración autorizada para evaluar la seguridad.
c) Un tipo de virus. d) Un CTF.

**5.** ¿Cuál es la función principal de la CPU?
a) Guardar ficheros. b) Ejecutar instrucciones. c) Mostrar imágenes. d) Conectar a Internet.

**6.** ¿Cuántos bits tiene un byte?
a) 4. b) 8. c) 16. d) 32.

**7.** ¿Cuánto vale el binario `1010` en decimal?
a) 8. b) 10. c) 12. d) 16.

**8.** ¿Cuánto vale el hexadecimal `FF` en decimal?
a) 15. b) 100. c) 255. d) 256.

**9.** ¿Qué es un hypervisor?
a) Un antivirus. b) Un software que ejecuta máquinas virtuales. c) Un tipo de RAM. d) Un servidor web.

**10.** ¿Cuántas capas tiene el modelo OSI?
a) 4. b) 5. c) 7. d) 8.

**11.** ¿Qué protocolos usa la capa de transporte?
a) TCP y UDP. b) IP y ARP. c) HTTP y FTP. d) Ethernet.

**12.** La máscara `/24` equivale a:
a) 255.0.0.0. b) 255.255.0.0. c) 255.255.255.0. d) 255.255.255.255.

**13.** ¿Cuál de estas es una IP privada?
a) 8.8.8.8. b) 192.168.1.10. c) 172.40.1.1. d) 200.1.1.1.

**14.** ¿En qué capa actúa una dirección MAC?
a) Aplicación. b) Transporte. c) Enlace (capa 2). d) Red.

**15.** ¿Qué puerto usa HTTPS por defecto?
a) 21. b) 80. c) 443. d) 3389.

**16.** ¿Qué diferencia clave hay entre TCP y UDP?
a) TCP es más rápido siempre. b) TCP es orientado a conexión y fiable; UDP no. c) UDP cifra y TCP no.
d) No hay diferencia.

**17.** ¿Para qué sirve DNS?
a) Asignar IPs dinámicas. b) Traducir nombres de dominio a direcciones IP. c) Cifrar el tráfico.
d) Filtrar paquetes.

**18.** ¿Qué comando lista el contenido de un directorio?
a) `cd`. b) `ls`. c) `pwd`. d) `cat`.

**19.** Los permisos `755` significan:
a) `rwxr-xr-x`. b) `rw-r--r--`. c) `rwxrwxrwx`. d) `r-xr-xr-x`.

**20.** ¿Qué usuario tiene control total en Linux?
a) admin. b) superuser. c) root. d) guest.

**21.** ¿Qué hace `chmod +x script.sh`?
a) Borra el script. b) Añade permiso de ejecución. c) Lo copia. d) Lo cifra.

**22.** ¿Cuál es una distro orientada a pentesting?
a) Windows 11. b) Kali Linux. c) macOS. d) ChromeOS.

**23.** ¿Qué muestra `pwd`?
a) Los procesos. b) El directorio actual. c) La IP. d) La hora.

**24.** ¿Qué hace `comando > fichero.txt`?
a) Lee el fichero. b) Redirige la salida al fichero, sobrescribiéndolo. c) Lo ejecuta. d) Lo borra.

**25.** ¿Qué hace la tubería `|`?
a) Une dos ficheros. b) Pasa la salida de un comando como entrada de otro. c) Copia. d) Cifra.

**26.** ¿Qué comando busca texto que coincida con un patrón?
a) `find`. b) `grep`. c) `ls`. d) `mv`.

**27.** ¿Qué línea debe empezar un script Bash?
a) `#!/bin/bash`. b) `<?php`. c) `import os`. d) `BEGIN`.

**28.** ¿Qué comando crea un repositorio Git nuevo en la carpeta actual?
a) `git new`. b) `git init`. c) `git start`. d) `git create`.

**29.** ¿Qué hace `git commit`?
a) Sube a GitHub. b) Guarda los cambios en el historial local con un mensaje. c) Descarga un repo.
d) Borra el repositorio.

**30.** `git clone` sirve para:
a) Crear una rama. b) Copiar un repositorio remoto a tu máquina. c) Hacer commit. d) Ver el estado.

**31.** ¿Qué es un Pull Request?
a) Una descarga. b) Una propuesta de cambios para que se revisen e integren. c) Un usuario de Git.
d) Un tipo de rama.

**32.** ¿Cómo se juega a OverTheWire Bandit?
a) Instalando un programa. b) Por SSH a un servidor. c) En el navegador. d) Con un USB.

**33.** La Web Security Academy (PortSwigger) es:
a) De pago. b) Gratis y centrada en seguridad web. c) Solo para empresas. d) Un CTF anual.

**34.** ¿Qué es HTB Starting Point?
a) Un plan de pago obligatorio. b) Un conjunto de máquinas guiadas para principiantes.
c) Un antivirus. d) Un foro.

**35.** picoCTF es:
a) Un CTF de pago para expertos. b) Un CTF gratuito pensado para principiantes.
c) Una distro de Linux. d) Una herramienta de escaneo.

**36.** ¿Qué hace `nmap -sn 192.168.56.0/24`?
a) Escanea puertos. b) Descubre hosts vivos sin escanear puertos. c) Detecta versiones.
d) Escanea UDP.

**37.** ¿Para qué sirve la opción `-sV` de Nmap?
a) Modo silencioso. b) Detección de versiones de servicio. c) Escaneo rápido. d) Guardar salida.

**38.** `nmap -oA salida` sirve para:
a) Ordenar la salida. b) Guardar la salida en todos los formatos con el prefijo `salida`.
c) Cifrar. d) Nada.

**39.** ¿Qué NO debe faltar en un informe de pentesting?
a) Adornos. b) Evidencia de los hallazgos. c) El color del portátil. d) Tu contraseña.

**40.** Estás escaneando `192.168.56.0/24` porque:
a) Es una red pública. b) Es tu red de laboratorio aislada. c) Es la red del vecino.
d) Lo hace todo el mundo.

??? success "Respuestas razonadas"
    **1. b)** Necesitas autorización por escrito o que sea tu lab/plataforma autorizada. "No hago daño"
    o "uso `-sS`" no te dan permiso. Escanear sin autorización es delito.

    **2. b)** Hacking ético = autorización + no causar daño + reportar. La herramienta (Kali) es solo
    eso, una herramienta.

    **3. c)** Reportar por el canal responsable (política de divulgación o `security.txt`). Explotarla
    es delito; publicarla sin avisar puede ser irresponsable.

    **4. b)** "Pentest" = *penetration test*: prueba de penetración **autorizada** para evaluar la
    seguridad.

    **5. b)** La CPU ejecuta instrucciones. Guardar ficheros es cosa del almacenamiento; mostrar
    imágenes, de la GPU.

    **6. b)** Un byte son **8 bits**. (Un *nibble* son 4 bits.)

    **7. b)** `1010` = 8 + 0 + 2 + 0 = **10**.

    **8. c)** `FF` = 15 × 16 + 15 = **255** (el mayor valor de un byte).

    **9. b)** Un hypervisor es el software que ejecuta máquinas virtuales (VirtualBox, VMware, KVM).

    **10. c)** OSI tiene **7** capas (física, enlace, red, transporte, sesión, presentación,
    aplicación).

    **11. a)** La capa de transporte usa **TCP y UDP**. IP/ARP son de red/enlace; HTTP/FTP, de
    aplicación.

    **12. c)** `/24` = **255.255.255.0**.

    **13. b)** `192.168.1.10` es privada. También lo son `10.x.x.x` y `172.16-31.x.x`. `8.8.8.8` (DNS
    público) y `200.1.1.1` son públicas; `172.40.1.1` está fuera del rango privado.

    **14. c)** La MAC es de **capa de enlace (2)**. La IP es de capa de red (3).

    **15. c)** HTTPS usa el puerto **443**. El 80 es HTTP; el 21, FTP; el 3389, RDP.

    **16. b)** TCP es orientado a conexión y fiable (con acuses de recibo); UDP no garantiza entrega ni
    orden. Que uno sea "más rápido siempre" es falso.

    **17. b)** DNS traduce nombres de dominio a direcciones IP. Asignar IPs dinámicas es DHCP.

    **18. b)** `ls` lista el contenido. `cd` cambia de directorio; `pwd` muestra dónde estás; `cat`
    muestra un fichero.

    **19. a)** `7 = rwx`, `5 = r-x`. Así, `755` = **`rwxr-xr-x`**.

    **20. c)** **root** es el superusuario con control total.

    **21. b)** `chmod +x` **añade permiso de ejecución**. No copia ni cifra nada.

    **22. b)** **Kali Linux** está orientada a pentesting (como Parrot).

    **23. b)** `pwd` muestra el **directorio actual** (*print working directory*).

    **24. b)** `>` redirige la salida a un fichero **sobrescribiéndolo**. `>>` sería añadir sin borrar.

    **25. b)** La tubería envía la salida de un comando como **entrada del siguiente**.

    **26. b)** `grep` busca texto por patrón. `find` busca ficheros por nombre/atributos.

    **27. a)** El *shebang* `#!/bin/bash` indica con qué intérprete ejecutar el script.

    **28. b)** `git init` inicializa un repositorio en la carpeta actual.

    **29. b)** `git commit` registra los cambios en el **historial local**. Subir a GitHub es `push`.

    **30. b)** `git clone` copia un repositorio remoto a tu máquina.

    **31. b)** Un Pull Request es una **propuesta de cambios** para revisión e integración (típico en
    colaboraciones).

    **32. b)** Bandit se juega por **SSH** a su servidor (puerto 2220).

    **33. b)** La Web Security Academy es **gratis** y está centrada en **seguridad web**.

    **34. b)** Starting Point es un conjunto de **máquinas guiadas** para principiantes en HTB.

    **35. b)** picoCTF es un CTF **gratuito para principiantes**.

    **36. b)** `-sn` es *no port scan*: descubre **hosts vivos sin escanear puertos**.

    **37. b)** `-sV` activa la **detección de versiones** de los servicios.

    **38. b)** `-oA` guarda la salida en **todos los formatos** con ese prefijo (`.nmap`, `.xml`,
    `.gnmap`).

    **39. b)** La **evidencia** (comandos y salidas reales) es lo que da valor a un informe. Sin ella,
    son opiniones.

    **40. b)** Porque es tu **red de laboratorio aislada**. Escanear redes públicas o ajenas es
    intrusismo y delito.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| Marcar todo sin probarlo | Optimismo | Marca solo lo que puedas demostrar con un comando |
| Mirar apuntes durante el test | Inseguridad | Hazlo primero sin mirar; ya repasarás |
| Frustrarse con un 60 % | Expectativas | Es normal: repasa y repite; el 70 % es orientativo |
| "Aprobé, no repaso nada" | Exceso de confianza | Repasa **los temas que fallaste**, siempre |
| Estudiar solo teoría | Pereza de practicar | La checklist exige práctica: hazla en tu lab |

## Ejercicios

1. **Autochequeo sin mirar.** Haz el test completo y anota solo el número de aciertos. No corrijas
   todavía.

    ??? success "Solución"
        Respuesta válida = un número entre 0 y 40. No hay "solución" que copiar: el objetivo es tener
        una **medida honesta** antes de ver las respuestas. Guarda ese número.

2. **Corrige y clasifica tus fallos.** Con las respuestas razonadas, anota a qué **módulo** pertenece
   cada fallo.

    ??? success "Solución"
        Ejemplo válido:

        ```markdown
        Fallos: Q12 (redes), Q19 (sistemas), Q38 (laboratorio)
        Módulo más flojo: redes -> repasar subnetting y puertos.
        ```

        Lo evaluable es que identifiques **dónde** está tu debilidad, no solo cuántas has fallado.

3. **Recalcula tu porcentaje.** Multiplica tus aciertos por 2,5 para obtener el porcentaje y sitúate
   en el criterio de "cuándo pasar al Nivel 2".

    ??? success "Solución"
        ```text
        Porcentaje = aciertos x 2.5
        Ejemplo: 30 aciertos -> 75 % -> listo para Nivel 2 (repasando los fallos).
        ```

4. **Repasa un tema flojo en 20 minutos.** Coge el módulo de tus fallos y relee **solo** la sección
   correspondiente. Anota una frase con lo que habías olvidado.

    ??? success "Solución"
        Ejemplo válido: "Había olvidado que `/24` = 255.255.255.0 y deja 254 hosts útiles (la .0 es
        red y la .255, broadcast)."

5. **Demuestra la base con comandos.** En tu laboratorio, encadena los comandos que demuestran tres
   casillas de la checklist de redes y sistemas (por ejemplo, `ip a`, `ping`, `nmap -sn`).

    ??? success "Solución"
        ```bash
        ip -brief address
        ping -c 2 192.168.56.101
        sudo nmap -sn 192.168.56.0/24
        ```

        Respuesta válida = las tres salidas demuestran, respectivamente, que sabes ver tus interfaces,
        comprobar conectividad y descubrir hosts. Eso son tres casillas **probadas**, no supuestas.

6. **Decide tu siguiente paso y escríbelo.** Con tu porcentaje y checklist, escribe una frase: "Paso
   al Nivel 2 el <fecha>" o "Repaso <módulo> durante <n> días".

    ??? success "Solución"
        Ejemplos válidos:
        - "80 % + checklist completa → paso al Nivel 2 el 2026-10-25."
        - "55 % → repaso Redes y Bash durante 7 días y repito el test."

## Resumen

- Esta página junta la **checklist completa** del Nivel 1 y un **test de 40 preguntas**.
- Marca solo lo que puedas **demostrar**; el test, hazlo **sin apuntes**.
- Criterio orientativo: **70 %** para pasar al Nivel 2 (90 %+ = base sólida).
- Los fallos son el mejor mapa: te dicen exactamente qué repasar.
- La teoría sin práctica no cuenta: la checklist del módulo 07 exige un laboratorio real.

## Checklist

- [ ] He completado la checklist de los 8 módulos.
- [ ] He hecho el test de 40 preguntas sin mirar apuntes.
- [ ] He corregido con las respuestas razonadas.
- [ ] Sé en qué módulos estoy flojo.
- [ ] He calculado mi porcentaje.
- [ ] He decidido: paso al Nivel 2 o repaso antes.
- [ ] Tengo por escrito mi siguiente paso.

## Para ir más allá

- **Glosario de UJACKING** — Cualquier término que se te haya olvidado.
  [Glosario](../glosario.md)
- **Ruta perfecta** — Cómo encajar el estudio en tu semana.
  [Ruta perfecta](../ruta-perfecta.md)
- **Cómo hacer writeups** — Convierte tu aprendizaje en portfolio.
  [Writeups](../empleabilidad/writeups.md)
- **Nivel 2 · Medio** — Lo que viene después si estás listo.
  [Nivel 2 · Medio](../nivel-2-medio/index.md)

## Siguiente paso

Si has llegado hasta aquí y la checklist está razonablemente completa: **enhorabuena**, tienes los
fundamentos. El siguiente destino es el **[Nivel 2 · Medio](../nivel-2-medio/index.md)**, donde
pasarás de "entender" a "hacer" con profundidad.
