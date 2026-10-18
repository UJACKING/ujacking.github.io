# Windows · básico

Windows es el sistema operativo de escritorio más extendido del mundo y, por eso, el que más se ataca en
las empresas. Aunque trabajarás mucho en Linux, **necesitas saber moverte por Windows**: sus carpetas,
sus usuarios y permisos, la consola **CMD**, **PowerShell**, el **registro**, los **servicios**, el
**Visor de eventos** y el **firewall**. Esta página es la base; en Nivel 2 lo llevarás hasta Active Directory.

## Objetivos de aprendizaje

- Entender la **estructura del sistema**: unidades, carpetas clave y variables de entorno.
- Distinguir cuentas locales, administradores y usuarios estándar, y cómo funciona la **UAC**.
- Entender los permisos **NTFS** (ACL) y aplicar los básicos con `icacls`.
- Moverte por **CMD** con órdenes fundamentales.
- Dar los primeros pasos con **PowerShell** y su filosofía de objetos.
- Explicar qué es el **registro de Windows** y para qué se usa (con aviso ético).
- Ver **servicios** y **procesos** (Administrador de tareas).
- Consultar el **Visor de eventos** (Event Viewer).
- Entender el **Firewall de Windows** y sus perfiles.

**Tiempo estimado:** 90–120 min.

## Requisitos previos

- **[01 · Linux · fundamentos](01-linux-fundamentos.md)** y
  **[03 · Linux · procesos, servicios y logs](03-linux-procesos-servicios-y-logs.md)**: muchos conceptos
  (permisos, procesos, servicios, logs) se entienden mejor si vienes de Linux.
- Un Windows al que puedas acceder (tu equipo, una VM o las máquinas de evaluación que mencionamos en la
  [página 08](08-maquinas-objetivo.md)).

## Explicación

### Estructura del sistema

Windows **sí** usa **letras de unidad**, al contrario que Linux. La principal es `C:\`, donde vive el
sistema. Las carpetas que debes conocer:

| Ruta | Para qué sirve |
| --- | --- |
| `C:\Windows` | El sistema operativo. Aquí está `System32`, el corazón del sistema. |
| `C:\Windows\System32` | Programas y librerías del sistema (64 bits en Windows de 64 bits). |
| `C:\Windows\SysWOW64` | Librerías de 32 bits en un Windows de 64 bits. |
| `C:\Program Files` | Programas instalados (64 bits). |
| `C:\Program Files (x86)` | Programas de 32 bits. |
| `C:\ProgramData` | Datos de aplicaciones para todos los usuarios (oculta por defecto). |
| `C:\Users\Nombre` | Carpeta personal de cada usuario (`Documentos`, `Escritorio`, `Descargas`…). |
| `C:\Users\Nombre\AppData` | Datos de aplicaciones por usuario: `Roaming`, `Local`, `LocalLow`. Oculta. |
| `C:\Windows\Temp` y `%TEMP%` | Ficheros temporales. |
| `C:\Windows\WinSxS` | Almacén de componentes del sistema (¡no tocar a mano!). |

**Variables de entorno** útiles (escríbelas tal cual en el Explorador o en la consola):

| Variable | Normalmente apunta a |
| --- | --- |
| `%SystemRoot%` | `C:\Windows` |
| `%SystemDrive%` | `C:` |
| `%USERPROFILE%` | `C:\Users\TuUsuario` |
| `%TEMP%` | Carpeta temporal del usuario |
| `%ProgramFiles%` | `C:\Program Files` |
| `%APPDATA%` | `...\AppData\Roaming` |

Puedes listarlas todas en CMD con `set` o en PowerShell con `Get-ChildItem Env:`.

### Usuarios, permisos y UAC

Windows tiene **cuentas locales** (en el propio equipo) y de **dominio** (en una empresa, gestionadas por
Active Directory, que verás en Nivel 2). Los tipos básicos:

- **Administrador:** puede cambiar todo (instalar software, modificar servicios, acceder a todo).
- **Usuario estándar:** puede usar el equipo pero no cambiar configuración del sistema.
- **System / Servicio local:** cuentas internas con las que corren servicios del sistema.
- **Invitado (Guest):** normalmente deshabilitada; nunca la actives.

La **UAC** (User Account Control) es el aviso "¿Quieres permitir que esta aplicación haga cambios?" que
salta incluso si eres administrador. Existe para que **no** trabajes siempre con privilegios totales: al
confirmar, elevas el proceso concreto. Es el "equivalente" a `sudo`, pero por ventanas.

Herramientas gráficas: `lusrmgr.msc` (Usuarios y grupos locales), `netplwiz` (cuentas), `compmgmt.msc`
(Administración de equipos).

**Permisos (ACL / NTFS):** cada fichero y carpeta tiene una **Lista de Control de Acceso** (ACL) con
entradas (ACE) que dicen **quién** puede hacer **qué**: `Full control`, `Modify`, `Read & execute`,
`Read`, `Write`, etc. Dos ideas clave:

- Los permisos **NTFS** son los que de verdad protegen un fichero.
- Los permisos de **recurso compartido (share)** solo aplican por red y actúan como un "filtro" que se
  combina con NTFS. Son famosos los fallos por compartir con "Todos: control total".

Comandos: `icacls` (ver y cambiar permisos), `takeown` (tomar propiedad), `attrib` (atributos oculto/solo
lectura).

### CMD: la consola clásica

`cmd.exe` es la consola de toda la vida. Menos potente que PowerShell, pero está en todas partes.

| Comando | Qué hace |
| --- | --- |
| `dir` | Lista el contenido (`dir /a` incluye ocultos). |
| `cd carpeta` / `cd /d D:\ruta` | Cambia de carpeta (`/d` cambia también de unidad). |
| `cls` | Limpia la pantalla. |
| `type fichero.txt` | Muestra un fichero. |
| `copy`, `move`, `del`, `ren` | Copiar, mover, borrar, renombrar. |
| `mkdir`, `rmdir /s` | Crear y borrar carpetas (`/s` recursivo). |
| `where comando` | Localiza un ejecutable. |
| `ipconfig /all` | Configuración de red. |
| `ping`, `tracert`, `netstat -ano` | Diagnóstico de red (`-ano` muestra PIDs). |
| `systeminfo` | Información del sistema. |
| `tasklist`, `taskkill /PID x /F` | Ver y matar procesos. |
| `net user`, `net localgroup` | Gestión de usuarios y grupos locales. |
| `whoami /priv` | Tus privilegios actuales. |
| `findstr "texto" fichero` | Busca texto (como `grep`). |
| `comando /?` | Ayuda del comando. |

### PowerShell: la consola moderna

PowerShell es la consola seria de Windows. Su gran diferencia: **trabaja con objetos, no con texto**. Un
comando no devuelve líneas de texto, devuelve **objetos** con propiedades, y puedes filtrarlos, ordenarlos
y encadenarlos con tuberías (`|`).

- Los comandos se llaman **cmdlets** y tienen forma `Verbo-Sustantivo`: `Get-Process`, `Stop-Service`.
- Hay **alias** cómodos: `ls`/`dir` → `Get-ChildItem`, `ps` → `Get-Process`, `cat` → `Get-Content`.

| Cmdlet | Qué hace |
| --- | --- |
| `Get-Help<cmdlet>` | Ayuda (`-Examples`, `-Full`). |
| `Get-Command` | Lista comandos disponibles. |
| `Get-ChildItem` | Lista ficheros/carpetas (`ls`, `dir`). |
| `Get-Content` | Muestra un fichero (`cat`, `type`). |
| `Get-Process` | Procesos (`ps`). |
| `Stop-Process -Name notepad -Force` | Mata un proceso. |
| `Get-Service` | Servicios y su estado. |
| `Start-Service` / `Stop-Service` | Arrancar / parar un servicio. |
| `Get-LocalUser` | Usuarios locales. |
| `Get-EventLog` / `Get-WinEvent` | Consultar eventos. |
| `Get-Acl` / `Set-Acl` | Ver y definir ACL. |
| `Select-Object`, `Where-Object`, `Sort-Object` | Proyectar, filtrar, ordenar objetos. |
| `Test-NetConnection` | Diagnóstico de red (`tnc`). |
| `Get-NetFirewallRule` | Reglas del firewall. |

La **ExecutionPolicy** controla si se pueden ejecutar scripts `.ps1` (`Get-ExecutionPolicy`,
`Set-ExecutionPolicy`). Por seguridad, Windows los bloquea por defecto.

!!! tip "Objetos, no texto"
    Compara: en CMD `tasklist` te da texto que tendrías que "recortar". En PowerShell,
    `Get-Process | Where-Object CPU -gt 100 | Sort-Object CPU -Descending` filtra y ordena **por
    propiedades reales**. Esa es la gran ventaja que usarás tanto en administración como en seguridad.

### El Registro de Windows

El **registro** es una base de datos jerárquica donde Windows y las aplicaciones guardan su
configuración: qué programas arrancan solos, asociaciones de ficheros, configuraciones de usuario,
servicios, drivers… Se abre con `regedit` en modo gráfico, o se consulta con `reg`.

**Raíces (hives) principales:**

| Clave | Contenido |
| --- | --- |
| `HKEY_LOCAL_MACHINE` (`HKLM`) | Configuración del equipo (todo el sistema). |
| `HKEY_CURRENT_USER` (`HKCU`) | Configuración del usuario actual. |
| `HKEY_CLASSES_ROOT` (`HKCR`) | Asociaciones de ficheros y tipos. |
| `HKEY_USERS` (`HKU`) | Perfiles de todos los usuarios. |
| `HKEY_CURRENT_CONFIG` (`HKCC`) | Configuración de hardware actual. |

**Para qué se usa en seguridad (con aviso ético):** los analistas miran el registro para descubrir
**persistencia de malware** y cómo está configurado el sistema. Dos rutas clásicas de autorranque:

```text
HKLM\Software\Microsoft\Windows\CurrentVersion\Run
HKCU\Software\Microsoft\Windows\CurrentVersion\Run
```

Todo lo que esté ahí se ejecuta **al iniciar sesión**. Si un programa desconocido aparece en esa clave,
es sospechoso.

!!! danger "No toques el registro a ciegas"
    El registro **no es un sitio para experimentar**. Modificar o borrar claves equivocadas puede dejar
    el sistema inutilizable y, si lo haces en un equipo ajeno, es una intromisión ilegal. Si necesitas
    verlo, **solo consulta**. Si vas a cambiar algo en tu laboratorio, exporta antes (`Archivo →
    Exportar`) y hazlo con snapshot de la VM.

### Servicios y procesos

- **Servicios:** `services.msc` (ventana) o `Get-Service` (PowerShell). Cada servicio tiene un **tipo de
  inicio**: Automático, Automático (inicio retrasado), Manual o Deshabilitado. Se consulta por línea de
  comandos con `sc query`, `sc qc nombre` (configuración).
- **Procesos:** el **Administrador de tareas** (++ctrl+shift+esc++) es tu vista rápida. Pestañas útiles:
  *Procesos* (CPU, memoria, disco, red), *Rendimiento* (gráficas), *Detalles* (PID y usuario),
  *Inicio* (qué arranca con Windows), *Servicios*, y en versiones modernas *Usuarios*.

Ruta de oro para investigar: mira primero la columna de **CPU** y **Red** ordenada, y en *Detalles* cruza
el **PID** con `netstat -ano` para saber qué proceso tiene qué conexión abierta.

### Visor de eventos (Event Viewer)

El Visor de eventos (`eventvwr.msc`) es el "log central" de Windows. Los registros principales son:

| Registro | Qué contiene |
| --- | --- |
| `Aplicación` | Eventos de programas. |
| `Seguridad` | Inicios de sesión, cambios de cuentas, uso de privilegios. |
| `Sistema` | Eventos del sistema operativo y controladores. |
| `Windows PowerShell` | Registro de actividad de PowerShell. |

Cada evento tiene nivel (**Information**, **Warning**, **Error**, **Critical**) y un **ID** que identifica
qué pasó. IDs de la vida real que conviene conocer:

| ID | Significado |
| --- | --- |
| `4624` | Inicio de sesión correcto. |
| `4625` | Inicio de sesión **fallido**. |
| `4672` | Se asignaron privilegios especiales (típico de `root`/admin). |
| `4720` / `4726` | Cuenta de usuario creada / eliminada. |
| `4688` | Se creó un proceso (si está activada la auditoría). |
| `7045` | Se instaló un servicio nuevo (muy relevante en persistencia). |
| `1102` | Se borró el registro de seguridad (¡bandera roja!). |

Filtrar por ID es la mitad del trabajo: en `Get-WinEvent` se hace con `-FilterXPath` o `-FilterHashtable`.

### Firewall de Windows

El **Firewall de Windows Defender** filtra el tráfico de red. Se gestiona en `wf.msc` (Firewall de Windows
con seguridad avanzada) o por consola. Tiene **tres perfiles**:

| Perfil | Cuándo se aplica |
| --- | --- |
| **Dominio** | El equipo está en el dominio de la empresa (gestionado por el administrador). |
| **Privada** | Red doméstica/oficina de confianza. |
| **Pública** | Redes públicas (cafeterías, aeropuertos): la más estricta. |

Cada regla es de **entrada (inbound)** o **salida (outbound)** y permite o bloquea. Por defecto, Windows
bloquea bastante entrada y permite casi toda salida.

| Comando | Qué hace |
| --- | --- |
| `netsh advfirewall show allprofiles` | Ver estado de los perfiles. |
| `netsh advfirewall firewall show rule name=all` | Ver todas las reglas. |
| `New-NetFirewallRule -DisplayName "web" -Direction Inbound -Protocol TCP -LocalPort 80 -Action Allow` | Crear una regla (PowerShell, requiere admin). |

!!! warning "Abrir puertos sin pensar"
    Cada puerto abierto es una puerta más. Abre solo lo estrictamente necesario, limita el **ámbito**
    (que la regla aplique solo a una IP/subred) y recuerda que en un laboratorio **no** debes exponer
    nada a Internet (lo veremos en la [página 07](07-laboratorio-red-virtual.md)).

## Ejemplos prácticos

### 1. Información básica en CMD

```cmd
whoami
hostname
systeminfo | findstr /C:"OS Name" /C:"OS Version"
```

```text
desktop\lucia
WIN-LAB01
OS Name:                   Microsoft Windows 11 Pro
OS Version:                10.0.22631 N/A Build 22631
```

*(salida de ejemplo)* `whoami` da DOMINIO\usuario (o EQUIPO\usuario si es cuenta local). El `| findstr`
filtra las líneas que nos interesan, igual que `grep` en Linux.

### 2. Usuarios y grupos locales

```cmd
net user
net localgroup administradores
```

```text
Cuentas de usuario de \\WIN-LAB01
-------------------------------------------------------------------------------
Administrador  DefaultAccount  invitado  lucia
El comando se ha completado correctamente.

Alias local     administradores
Miembros
-------------------------------------------------------------------------------
Administrador
lucia
```

*(salida de ejemplo)* El nombre del grupo de administradores cambia según el **idioma** del sistema
(`administradores` en español, `Administrators` en inglés). Comprueba siempre cuál es el tuyo.

### 3. PowerShell: procesos que más CPU consumen

```powershell
Get-Process | Sort-Object CPU -Descending | Select-Object -First 5 Name, Id, CPU
```

```text
Name        Id       CPU
----        --       ---
firefox     5120    142,31
MsMpEng     2101     87,44
explorer    4020     33,10
```

*(salida de ejemplo)* Ordenamos objetos por la propiedad `CPU` y proyectamos solo tres columnas. Fíjate
en la diferencia con CMD: aquí no "cortamos texto", seleccionamos **propiedades de objetos**.

### 4. Consultar un evento de seguridad

```powershell
Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} -MaxEvents 3
```

```text
TimeCreated           Id LevelDisplayName Message
-----------           -- ---------------- -------
12/10/2026 13:40:01 4625 Information      Error de inicio de sesión: cuenta desconocida...
12/10/2026 13:39:58 4625 Information      Error de inicio de sesión: contraseña incorrecta...
12/10/2026 13:39:55 4625 Information      Error de inicio de sesión: cuenta desconocida...
```

*(salida de ejemplo)* Tres `4625` seguidos en segundos: patrón típico de intento de fuerza bruta. Requiere
permisos de administrador para leer el registro de Seguridad.

### 5. Ver y ajustar permisos con `icacls`

```cmd
icacls C:\Users\lucia\Documentos\proyecto
icacls C:\Users\lucia\Documentos\proyecto /grant lucia:(OI)(CI)F
```

```text
C:\Users\lucia\Documentos\proyecto WIN-LAB01\lucia:(OI)(CI)(F)
                                    BUILTIN\Administradores:(OI)(CI)(F)
```

*(salida de ejemplo)* `(OI)` y `(CI)` significan que el permiso se **hereda** a ficheros y subcarpetas;
`(F)` es control total. El segundo comando **concede** control total a `lucia`, heredable.

## Errores comunes

| Error | Por qué ocurre | Solución |
| --- | --- | --- |
| `Access is denied` | No eres administrador o falta UAC. | Abre la consola "como administrador" (botón derecho). |
| Confundir permisos de *share* y NTFS | Se combinan; el más restrictivo manda. | Revisa **ambos** con `icacls` y las propiedades del recurso compartido. |
| Ejecutar `.ps1` y no funciona | La ExecutionPolicy los bloquea. | Cámbiala para la sesión; entiende **por qué** existe antes. |
| Tocar el registro "para optimizar" | Se rompe el sistema. | Solo consulta; exporta antes y trabaja en una VM. |
| No ver ficheros/carpetas | Están **ocultos**. | Activa "elementos ocultos" o usa `dir /a` / `-Force`. |
| Puertos abiertos "temporalmente" | Quedan siempre. | Revisa reglas con `Get-NetFirewallRule`; elimina lo que no uses. |

## Ejercicios

1. **Reconocimiento local.** En CMD, obtén el nombre del equipo, el usuario actual y la versión de
   Windows en tres comandos.
2. **Usuarios.** Lista las cuentas locales y averigua quién está en el grupo de administradores.
3. **PowerShell.** Muestra los 5 servicios que están **detenidos**.
4. **Eventos.** Localiza el último **inicio de sesión correcto** y el último **fallido** en el Visor de
   eventos, indicando su ID y hora.
5. **Firewall.** Comprueba el estado de los tres perfiles del firewall y explica cuál se aplicaría en una
   red pública.
6. **Permisos.** Crea una carpeta, quita el acceso a "Todos" y concédelo solo a tu usuario con `icacls`.

??? success "Solución"
    1. `hostname`, `whoami`, `systeminfo | findstr /C:"OS Name" /C:"OS Version"`.
    2. `net user` y `net localgroup administradores` (o `Administrators` si el sistema está en inglés).
    3. `Get-Service | Where-Object Status -eq "Stopped" | Select-Object -First 5`.
    4. En `eventvwr.msc` → Registros de Windows → Seguridad → *Filtrar registro actual* por ID `4624`
       (correcto) y `4625` (fallido). Por consola: `Get-WinEvent -FilterHashtable @{LogName='Security';Id=4624} -MaxEvents 1`.
    5. `netsh advfirewall show allprofiles`: los tres perfiles deben aparecer sin conexiones bloqueadas
       arbitrariamente. En una red pública se aplica el perfil **Público**, el más restrictivo.
    6. `icacls C:\ruta\carpeta /inheritance:r` (quita herencia), `icacls C:\ruta\carpeta /remove "Todos"`
       (o `Everyone`) y `icacls C:\ruta\carpeta /grant TuUsuario:(OI)(CI)F`.

## Resumen

- Windows usa **letras de unidad**; las carpetas clave son `C:\Windows\System32`, `Program Files`,
  `ProgramData` y `C:\Users`.
- Las cuentas pueden ser **administrador** o **usuario estándar**; la **UAC** evita privilegios
  permanentes.
- Los permisos son **ACL NTFS**; los de recurso compartido se combinan con ellos.
- **CMD** para lo clásico; **PowerShell** trabaja con **objetos** y tiene cmdlets `Verbo-Sustantivo`.
- El **registro** guarda configuración y claves de autorranque (persistencia); no se toca a ciegas.
- Servicios y procesos se ven en `services.msc` y el **Administrador de tareas**.
- El **Visor de eventos** es el log central; IDs como `4624`, `4625` y `7045` son lectura obligada.
- El **Firewall de Windows** tiene tres perfiles y reglas de entrada/salida.

## Checklist

- [ ] Localizo `System32`, `Program Files`, `ProgramData` y las carpetas de usuario.
- [ ] Distingo administrador, usuario estándar y entiendo qué hace la UAC.
- [ ] Leo y modifico permisos básicos con `icacls`.
- [ ] Me manejo con los comandos esenciales de CMD.
- [ ] Entiendo la filosofía de objetos de PowerShell y uso varios cmdlets.
- [ ] Sé qué es el registro y por qué no se toca a ciegas.
- [ ] Veo servicios y procesos y su relación con la red.
- [ ] Navego por el Visor de eventos y filtro por ID.
- [ ] Explico los tres perfiles del firewall y sus reglas.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Documentación de Microsoft Learn](https://learn.microsoft.com) | Documentación oficial de Windows/PowerShell | Multi | Gratis |
| [GitHub](https://github.com) | Scripts y recursos de la comunidad | Multi | Gratis |
| [TryHackMe](https://tryhackme.com) | Salas con Windows y Active Directory | EN | Freemium |

!!! note "Recursos en inglés"
    La mejor documentación de Windows está en inglés. Acostúmbrate desde ya: en ciberseguridad es la
    norma.

## Siguiente paso

Ya conoces los dos sistemas. Ahora decide **desde dónde** vas a atacar:
**[05 · Elegir distro de hacking](05-elegir-distro-de-hacking.md)**.
