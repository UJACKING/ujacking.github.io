# Nivel 2 · Medio

Aquí pasas de "entender" a **saber hacer**. El Nivel 2 asume que dominas los fundamentos del
[Nivel 1](../nivel-1-principiante/index.md) y te lleva a la práctica real del pentesting y de la
defensa, con ejercicios en laboratorio.

!!! info "¿Estás listo para el Nivel 2?"
    Si has terminado la [checklist del Nivel 1](../nivel-1-principiante/08-checklist-y-autoevaluacion.md)
    y sacas al menos un 70 % en su test, sí. Si no, mejor consolidar el Nivel 1 antes.

## Mapa del nivel

| Módulo | Qué cubre |
| --- | --- |
| [01 · Linux avanzado y escalada de privilegios](01-linux-avanzado-y-privesc.md) | SUID, cron, capabilities, vectores típicos de `privesc`. |
| [02 · Windows y Active Directory](02-windows-y-active-directory.md) | Dominios, usuarios, grupos, GPOs, Kerberos a alto nivel. |
| [03 · Redes avanzadas y firewalls](03-redes-avanzadas-y-firewalls.md) | VLANs, `iptables`/`nftables`, VPN, proxies. |
| [04 · Python para seguridad](04-python-para-seguridad.md) | Sockets, `requests`, automatización de tareas. |
| [05 · Nmap en profundidad](05-nmap-en-profundidad.md) | Tipos de escaneo, scripts NSE, sigilo y detección. |
| [06 · Metodología de pentesting](06-metodologia-de-pentesting.md) | Fases: reconocimiento, enumeración, explotación, post-explotación, informe. |
| [07 · Seguridad web y OWASP Top 10](07-seguridad-web-y-owasp-top-10.md) | Vulnerabilidades web y cómo se explotan (en laboratorio). |
| [08 · Burp Suite](08-burp-suite.md) | Proxy de intercepción, repeater, intruder. |
| [09 · Introducción a Metasploit](09-introduccion-a-metasploit.md) | Framework, módulos, sesiones. |
| [10 · Criptografía aplicada](10-criptografia-aplicada.md) | Simétrica, asimétrica, hashes, PKI, casos reales. |
| [11 · Forense y OSINT](11-forense-y-osint.md) | Evidencias, artefactos, inteligencia de fuentes abiertas. |
| [12 · Hardening básico](12-hardening-basico.md) | Endurecer Linux, Windows y servicios. |

## Cómo trabajarlo

- Cada módulo tiene **contenido real y ejercicios**, con profundidad media: no es una enciclopedia,
  es una guía para practicar.
- Necesitarás tu **laboratorio** del Nivel 1 funcionando. Sin máquinas objetivo no hay nada que hacer.
- Ten a mano la [chuleta de Bash](../nivel-1-principiante/04-bash/05-chuleta-bash.md) y practica en
  plataformas como [TryHackMe](../nivel-1-principiante/06-donde-practicar/01-tryhackme.md) o
  [Hack The Box](../nivel-1-principiante/06-donde-practicar/02-hack-the-box.md).

!!! danger "Recuerda"
    Todo lo ofensivo se practica **solo** contra tu laboratorio o plataformas que lo autorizan.
    Nada de escanear o atacar redes ajenas.

## Siguiente paso

Cuando domines el Nivel 2 y quieras orientarte a certificaciones, pasa al
**[Nivel 3 · Avanzado](../nivel-3-avanzado/index.md)**.
