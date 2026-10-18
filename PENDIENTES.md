# PENDIENTES de UJACKING

Este fichero recoge **todo lo que queda por rellenar, confirmar o verificar** en la web. Se genera a
partir de los marcadores `TODO-UJACKING` repartidos por el contenido.

## Cómo localizarlos

```bash
grep -rn "TODO-UJACKING" docs/
```

Dos formatos posibles:

- Bloque destacado:

  ```markdown
  !!! warning "PENDIENTE (TODO-UJACKING)"
      Descripción de lo que falta y quién debe rellenarlo.
  ```

- Marcador en línea: `TODO-UJACKING: descripción`.

## Resumen por bloques (qué hay que hacer)

### 1. Legales y licencias (responsabilidad de la directiva / asesoría)

- **Números de artículo del Código Penal** en
  `docs/nivel-1-principiante/00-etica-y-legalidad.md`: están puestos como **orientativos** y marcados
  como pendientes. Debe revisarlos una persona con formación jurídica antes de darlos por buenos.
- **Licencia del proyecto** (`LICENSE`): propuesta CC BY-SA 4.0 (contenido) + MIT (código), pendiente
  de confirmación por la directiva.
- **ENS / normativa** citada en `docs/paths/grc.md`: verificar enlace y edición vigente.

### 2. Datos de la asociación (responsabilidad de la directiva)

- `docs/quienes-somos/index.md` y `docs/quienes-somos/fines.md`: **fecha de fundación**, **sede**,
  **CIF / registro de asociaciones**, **vinculación oficial con la UJA**, **estatutos**, **junta
  directiva** y **cuerpo técnico**. Los fines están redactados como **propuesta a validar**.
- `docs/quienes-somos/contacto.md`: **redes sociales oficiales** y **proceso de alta de socios**.
- `docs/quienes-somos/normas-comunidad.md` y `CODE_OF_CONDUCT.md`: **canal de reporte de conducta**.
- `.github/CODEOWNERS`: sustituir `@UJACKING` por el equipo real cuando exista.

### 3. Verificación de plataformas (cambian con frecuencia)

- **Política de writeups de máquinas activas** de HTB y THM (`docs/empleabilidad/writeups.md`). **No
  se afirman sus reglas**: hay que comprobarlas y actualizar la página.
- **Planes gratuitos / límites** de TryHackMe y Hack The Box
  (`docs/nivel-1-principiante/06-donde-practicar/`): nº de máquinas gratis, resets, módulos gratis de
  Academy… (sin inventar precios).
- Estado vigente de OverTheWire (wargames activos, host/puerto de Bandit), picoCTF (fechas),
  SANS Holiday Hack, LetsDefend y Blue Team Labs Online.
- **Certificaciones** (Nivel 3): formato, duración, puntuación, precio y vigencia de eJPT, CPTS, OSCP,
  Security+, PenTest+, PNPT, BSCP y ISO 27001 Lead Auditor. **Consultar siempre la web oficial.**

### 4. Verificación técnica de herramientas y versiones

- Requisitos oficiales (RAM/disco) de Kali y Parrot; fingerprints de sus claves GPG; credenciales por
  defecto de las imágenes de VM preconstruidas
  (`docs/nivel-1-principiante/03-sistemas-operativos/05-*.md` y `06-*.md`).
- Nombres de imagen Docker vigentes de DVWA, OWASP Juice Shop y WebGoat; licencia y disponibilidad de
  las **VMs de evaluación de Windows** (`.../08-maquinas-objetivo.md`).
- Nombres exactos de los menús de red en las versiones actuales de VirtualBox y VMware
  (`.../07-laboratorio-red-virtual.md`).
- Falta un **`.pcap` de práctica** para Wireshark (`.../02-redes/11-wireshark.md`).
- Falta una **versión imprimible (PDF)** de la chuleta de Bash
  (`.../04-bash/05-chuleta-bash.md`).

### 5. Recursos en español (por área)

Varios Paths piden **verificar y enlazar recursos hispanohablantes** (canales, academias, cursos) que
no se han podido confirmar: web, infraestructura, AD/red team, blue team, forense, malware,
OSINT, cloud, GRC, AppSec, criptografía, CTI, bug bounty, móvil y hardware/IoT.

### 6. Limitación del entorno de construcción

- `https://nmap.org` (y sus subpáginas) **no se pudo comprobar** desde el entorno donde se generó la
  web (bloqueo de red). Es un dominio oficial que existe; conviene revalidarlo con el workflow
  `Check links`.

## Listado completo (`grep -rn "TODO-UJACKING" docs/`)

```text
index.md:74:!!! warning "PENDIENTE (TODO-UJACKING)"
assets/favicon.svg:2:  <!-- Favicon provisional. PENDIENTE (TODO-UJACKING): sustituir por el oficial. -->
assets/logo.svg:4:    PENDIENTE (TODO-UJACKING): sustituir por el logotipo oficial de la asociación.
quienes-somos/normas-comunidad.md:102:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/contacto.md:20:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/contacto.md:35:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/contacto.md:76:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/index.md:7:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/index.md:23:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/fines.md:7:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/fines.md:26:!!! warning "PENDIENTE (TODO-UJACKING)"
quienes-somos/fines.md:87:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/seguridad-movil.md:85:- TODO-UJACKING: verificar y enlazar laboratorios/cursos de seguridad móvil en español vigentes.
paths/seguridad-movil.md:91:- Charlas de **OWASP** y **DEF CON** sobre móvil en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar listas de reproducción verificadas.
paths/analisis-de-malware-e-ingenieria-inversa.md:93:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/pentesting-web.md:96:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/grc.md:62:5. Aprende el **ENS** para el sector público español en [administracionelectronica.gob.es](https://administracionelectronica.gob.es) **(ES, Gratis)** — TODO-UJACKING: verificar la ruta exacta del documento vigente del ENS y enlazarla.
paths/grc.md:90:- **Canal YouTube general**, busca charlas de marcos y GRC; canal recomendado: [youtube.com](https://www.youtube.com) — TODO-UJACKING: fijar 2–3 canales verificados de GRC (p. ej. *Simply Cyber*) con enlace directo al canal.
paths/grc.md:92:- TODO-UJACKING: recopilar vídeos en español de ISO 27001 y ENS con enlace verificado.
paths/grc.md:108:- **ISO/IEC 27001 Lead Implementer / Lead Auditor** — varios organismos de certificación personales; busca el programa vigente. TODO-UJACKING: listar proveedores acreditados en España.
paths/pentesting-de-infraestructura.md:90:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/bug-bounty.md:94:- TODO-UJACKING: verificar y enlazar guías de bug bounty en español (blogs/comunidades) antes de recomendarlas.
paths/criptografia.md:46:4. Sigue **Computerphile** para intuiciones claras: [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlace directo al canal.
paths/criptografia.md:89:- Todas las clases del curso de **Christof Paar** están publicadas; busca "Introduction to Cryptography" en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: verificar el enlace exacto de la lista de reproducción.
paths/criptografia.md:90:- TODO-UJACKING: recopilar vídeos de criptografía en español con enlaces verificados.
paths/index.md:48:    detalle llevan marcado `TODO-UJACKING` para revisarlos antes de confiar en ellos.
paths/blue-team-soc.md:85:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/osint.md:90:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/osint.md:122:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/appsec-y-desarrollo-seguro.md:91:- DevSecOps y código seguro: busca en [youtube.com](https://www.youtube.com) — TODO-UJACKING: fijar canales concretos verificados.
paths/cyber-threat-intelligence.md:86:- TODO-UJACKING: verificar cursos de CTI en español (INTECO/INCIBE y universidades) y enlazar los vigentes.
paths/cyber-threat-intelligence.md:92:- Charlas de **conferencias de seguridad** (DEF CON, BSides, RSA) disponibles en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlaces de listas de reproducción concretas.
paths/active-directory-y-red-team.md:87:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/forense-digital-e-ir.md:87:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/cloud-security.md:88:!!! warning "PENDIENTE (TODO-UJACKING)"
paths/hardware-iot.md:88:- TODO-UJACKING: verificar y enlazar cursos/laboratorios de hardware hacking en español vigentes.
paths/hardware-iot.md:94:- **Hackaday** publica charlas y *supercon* en [youtube.com](https://www.youtube.com) **(EN, Gratis)** — TODO-UJACKING: fijar enlaces verificados.
paths/hardware-iot.md:104:- TODO-UJACKING: identificar certificaciones específicas de IoT/hardware reconocidas por el mercado y enlazar su web oficial.
nivel-2-medio/03-redes-avanzadas-y-firewalls.md:239:  <https://netfilter.org> · PENDIENTE verificar enlace concreto: TODO-UJACKING
nivel-2-medio/03-redes-avanzadas-y-firewalls.md:241:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-2-medio/01-linux-avanzado-y-privesc.md:349:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-2-medio/11-forense-y-osint.md:161:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-2-medio/11-forense-y-osint.md:297:  <https://www.shodan.io> · PENDIENTE confirmar política de uso educativa vigente: TODO-UJACKING
nivel-2-medio/08-burp-suite.md:135:    · PENDIENTE confirmar condiciones vigentes de licencia: TODO-UJACKING.
nivel-2-medio/07-seguridad-web-y-owasp-top-10.md:87:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-2-medio/07-seguridad-web-y-owasp-top-10.md:183:instalan en local (aplicaciones de práctica tipo DVWA/Juice Shop — **TODO-UJACKING**: verificar la URL
nivel-2-medio/02-windows-y-active-directory.md:163:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-2-medio/12-hardening-basico.md:132:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/07-laboratorio-red-virtual.md:139:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/06-montar-kali-y-parrot.md:123:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/06-montar-kali-y-parrot.md:172:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/06-montar-kali-y-parrot.md:240:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/05-elegir-distro-de-hacking.md:103:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md:81:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md:97:1. Descarga el archivo oficial desde la web del proyecto (Rapid7/Metasploit). TODO-UJACKING: confirmar el
nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md:102:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md:139:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/03-sistemas-operativos/08-maquinas-objetivo.md:231:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/04-bash/04-scripts-bash.md:682:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/04-bash/05-chuleta-bash.md:278:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/04-bash/02-comandos-esenciales.md:512:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/04-bash/01-terminal-shell-y-consola.md:349:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/04-bash/03-tuberias-redirecciones-y-filtros.md:373:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/05-git-y-github/04-github-forks-y-pull-requests.md:436:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/05-git-y-github/01-control-de-versiones.md:301:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/05-git-y-github/05-github-pages-y-perfil.md:317:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/02-redes/09-dispositivos-topologias-y-wifi.md:263:  TODO-UJACKING: verificar el enlace oficial estable al estándar 802.11 y añadirlo aquí.
nivel-1-principiante/02-redes/11-wireshark.md:242:!!! warning "TODO-UJACKING: falta un `.pcap` de práctica"
nivel-1-principiante/02-redes/03-subnetting.md:455:  practica con los ejercicios de esta página. TODO-UJACKING: añadir aquí un recurso concreto de
nivel-1-principiante/02-redes/index.md:52:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/00-etica-y-legalidad.md:123:   `security@` o una política de divulgación). Si no lo encuentras, márcalo como `TODO-UJACKING` en
nivel-1-principiante/00-etica-y-legalidad.md:152:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/00-etica-y-legalidad.md:171:| **Acceso ilícito a sistemas informáticos** | Entrar (o intentarlo) en un sistema sin autorización. Artículo `197 bis` `TODO-UJACKING`: número pendiente de verificar por una persona con formación jurídica. |
nivel-1-principiante/00-etica-y-legalidad.md:172:| **Descubrimiento y revelación de secretos** | Apoderarse o difundir datos o comunicaciones ajenos. Artículo `197` (y siguientes) `TODO-UJACKING`: números pendientes de verificar. |
nivel-1-principiante/00-etica-y-legalidad.md:173:| **Daños informáticos** | Borrar, alterar o inutilizar datos, programas o sistemas ajenos. Artículo `264` `TODO-UJACKING`: número pendiente de verificar. |
nivel-1-principiante/00-etica-y-legalidad.md:174:| **Estafa informática** | Conseguir un beneficio patrimonial mediante engaño (por ejemplo, *phishing*). Artículos `248` y `249` `TODO-UJACKING`: números pendientes de verificar. |
nivel-1-principiante/00-etica-y-legalidad.md:176:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/00-etica-y-legalidad.md:180:    referencias al `197 ter` y a la normativa europea pertinente `TODO-UJACKING`.
nivel-1-principiante/06-donde-practicar/05-ctfs.md:72:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/index.md:62:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/06-otras-plataformas.md:68:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/06-otras-plataformas.md:86:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/01-tryhackme.md:45:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/01-tryhackme.md:69:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/02-hack-the-box.md:61:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/03-overthewire.md:44:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-1-principiante/06-donde-practicar/03-overthewire.md:77:!!! warning "PENDIENTE (TODO-UJACKING)"
glosario.md:344:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/practicas-y-becas.md:21:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/practicas-y-becas.md:51:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/practicas-y-becas.md:55:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/practicas-y-becas.md:59:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/perfil-de-linkedin.md:106:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/writeups.md:123:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/index.md:27:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/github-como-portfolio.md:189:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/portales-de-empleo.md:30:!!! warning "PENDIENTE (TODO-UJACKING)"
empleabilidad/portales-de-empleo.md:36:!!! warning "PENDIENTE (TODO-UJACKING)"
ruta-perfecta.md:317:!!! warning "PENDIENTE (TODO-UJACKING)"
ruta-perfecta.md:322:!!! warning "PENDIENTE (TODO-UJACKING)"
nivel-3-avanzado/ejpt.md:13:    TODO-UJACKING: confirmar en la web oficial de INE Security el nombre comercial actual de la
nivel-3-avanzado/ejpt.md:49:    TODO-UJACKING: enlazar y citar el temario oficial vigente de la eJPT y actualizar esta sección
nivel-3-avanzado/oscp.md:13:    TODO-UJACKING: confirmar en la web oficial de OffSec el formato vigente del examen (tipo y
nivel-3-avanzado/index.md:11:    `TODO-UJACKING`.
nivel-3-avanzado/cpts.md:13:    TODO-UJACKING: confirmar en la web oficial de Hack The Box el nombre exacto del examen, el
nivel-3-avanzado/cpts.md:49:    TODO-UJACKING: enlazar el temario y la ruta oficial de módulos de la CPTS y actualizar esta
nivel-3-avanzado/otras-certificaciones.md:23:    TODO-UJACKING: confirmar en comptia.org el número de preguntas, la duración, la puntuación de
nivel-3-avanzado/otras-certificaciones.md:37:    TODO-UJACKING: confirmar en comptia.org el formato (preguntas + simulaciones), duración,
nivel-3-avanzado/otras-certificaciones.md:49:    TODO-UJACKING: confirmar en la web oficial de TCM Security el reglamento vigente del examen
nivel-3-avanzado/otras-certificaciones.md:63:    TODO-UJACKING: confirmar en la web oficial de PortSwigger el formato vigente del examen BSCP,
nivel-3-avanzado/otras-certificaciones.md:78:    TODO-UJACKING: indicar el organismo o los organismos de certificación concretos que ofrecen el
contribuir/index.md:20:- [ ] Los enlaces funcionan o están marcados como `TODO-UJACKING`.
contribuir/index.md:41:!!! warning "PENDIENTE (TODO-UJACKING)"
```

Total de marcas: 113 en 67 ficheros.
