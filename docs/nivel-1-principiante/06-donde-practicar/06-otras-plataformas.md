# Otras plataformas

**Café para todos los gustos.** Además de las plataformas con página propia en este módulo, hay muchas
otras donde practicar: máquinas descargables, retos de blue team, bug bounty, competiciones anuales y
tus propios laboratorios. Aquí tienes un mapa — y la regla de siempre: **solo nombramos lo que existe
con certeza**.

## Objetivos de aprendizaje

Al terminar esta página serás capaz de:

- Conocer plataformas alternativas para ampliar tu práctica.
- Distinguir plataformas de **red team (ofensivo)**, **blue team (defensivo)** y **bug bounty**.
- Descargar y montar una **máquina virtual vulnerable** (VulnHub, Metasploitable) en tu laboratorio.
- Montar **laboratorios propios** con aplicaciones vulnerables (Juice Shop, WebGoat, DVWA).

**Tiempo estimado:** 30-45 min de lectura.

## Requisitos previos

- [Índice del módulo](index.md): comparativa general de plataformas.
- [03 · Laboratorio de red virtual](../03-sistemas-operativos/07-laboratorio-red-virtual.md): dónde
  correr tus máquinas.
- [03 · Máquinas objetivo](../03-sistemas-operativos/08-maquinas-objetivo.md): las víctimas de tu lab.
- [00 · Ética y legalidad](../00-etica-y-legalidad.md).

## Explicación

### Red team vs blue team (en una frase)

- **Red team (ofensivo):** atacar. Buscar y explotar fallos. Plataformas como HTB, TryHackMe o VulnHub.
- **Blue team (defensivo):** defender. Detectar, investigar y responder a incidentes. Plataformas como
  LetsDefend o Blue Team Labs Online.

Practicar las dos te hace mucho más completo, y el blue team tiene muchísima demanda de empleo (lo
verás en el [path de Blue Team y SOC](../../paths/blue-team-soc.md)).

### Máquinas descargables (red team)

| Plataforma | Qué es | Modelo | Idioma |
| --- | --- | --- | --- |
| **VulnHub** | Máquinas virtuales vulnerables para descargar y montar en tu lab | **Gratis** | (EN) |
| **Metasploitable** | Máquina vulnerable "clásica" de Rapid7, para empezar | **Gratis** | (EN) |
| **OWASP Juice Shop** | Aplicación web moderna y vulnerable (Node.js) | **Gratis** | (EN) |
| **OWASP WebGoat** | Aplicación web didáctica con lecciones | **Gratis** | (EN) |
| **DVWA** | *Damn Vulnerable Web Application*: web muy simple y clásica | **Gratis** | (EN) |

Con estas practicas **sin depender de Internet ni de suscripciones**: descargas la máquina, la montas
en tu lab y a jugar. La pega: eres tú quien se configura todo (y eso también se aprende).

### Plataformas (red team y mixtas)

| Plataforma | Qué es | Modelo | Idioma |
| --- | --- | --- | --- |
| **Hack The Box** | Máquinas y Academy (tiene [página propia](02-hack-the-box.md)) | **Freemium** | (EN) |
| **TryHackMe** | Rutas guiadas (tiene [página propia](01-tryhackme.md)) | **Freemium** | (EN) |
| **Root-Me** | Retos variados y CTFs en equipo; plataforma veterana | **Freemium** | (EN/FR) |
| **pwn.college** | Doctrina de "aprender haciendo" sobre binarios/sistemas | **Gratis** | (EN) |

### Plataformas (blue team)

| Plataforma | Qué es | Modelo | Idioma |
| --- | --- | --- | --- |
| **LetsDefend** | Simulador de SOC: alertas, investigación, respuesta | **Freemium** | (EN) |
| **Blue Team Labs Online** | Retos de defensa, forense y respuesta a incidentes | **Freemium** | (EN) |
| **SANS Holiday Hack Challenge** | Reto anual gratuito de SANS (temática navideña) | **Gratis** | (EN) |

!!! warning "PENDIENTE (TODO-UJACKING)"
    El **Holiday Hack Challenge** se celebra una vez al año y su edición y estructura cambian. Verifica
    fechas, estado y requisitos vigentes en [https://www.sans.org](https://www.sans.org) antes de
    publicar. Lo mismo para el modelo gratuito/de pago de **LetsDefend** y **Blue Team Labs Online**:
    confirma las condiciones actuales en sus webs.

### Bug bounty (ganar dinero, nivel avanzado)

El **bug bounty** consiste en que empresas te pagan por reportar vulnerabilidades en sus sistemas
legítimamente. Es legal porque **ellos te autorizan** mediante un programa. **No es para empezar**: es
un destino al que llegarás después de dominar la seguridad web (mira
[el path de bug bounty](../../paths/bug-bounty.md)). Plataformas conocidas:

- **HackerOne** — [https://www.hackerone.com](https://www.hackerone.com)
- **Bugcrowd** — [https://www.bugcrowd.com](https://www.bugcrowd.com)
- **Intigriti** — [https://www.intigriti.com](https://www.intigriti.com)
- **YesWeHack** — [https://www.yeswehack.com](https://www.yeswehack.com)

!!! warning "PENDIENTE (TODO-UJACKING)"
    Hay más plataformas de bug bounty y su catálogo de programas cambia a diario. Añade las que
    consideréis relevantes tras verificarlas, y enlaza siempre solo el dominio raíz.

### Laboratorios propios (el plan definitivo)

Tu mejor plataforma eres tú montando tu laboratorio. Con **VirtualBox** o **VMware** recreas redes
completas: un atacante (tu Kali), una víctima (Metasploitable o una VM de VulnHub) y, si quieres,
servicios en [Docker](https://docs.docker.com) (Juice Shop corre en un contenedor).

Ventajas:

- Controlas todo, sin límites de plan ni de tiempo.
- Practicas **montar** las cosas, no solo romperlas.
- Puedes repetir hasta que te salga de memoria.

Esto es exactamente lo que harás de principio a fin en el
**[Primer laboratorio](../07-primer-laboratorio.md)** del Nivel 1.

!!! danger "Aviso ético"
    Las máquinas de VulnHub y las apps vulnerables son **legales solo dentro de tu laboratorio
    aislado**. Nunca las expongas a Internet ni las dejes accesibles en una red compartida (wifi
    pública, red de la universidad). Y no ataques nunca un sistema ajeno, ni "solo un escaneo".

## Ejemplos prácticos

**1. Montar una VM de VulnHub.** El flujo es:

1. Descarga el `.ova` o `.vdi` desde [https://www.vulnhub.com](https://www.vulnhub.com).
2. Impórtalo en VirtualBox: **Archivo → Importar servicio virtualizado** (para `.ova`).
3. Configura la red en **"Red interna"** o **"Adaptador solo-anfitrión"** para dejarla aislada.
4. Arranca y descubre su IP.

**2. Descubrir la IP de la máquina recién arrancada.** Asumiendo el rango de tu red solo-anfitrión:

```bash
sudo nmap -sn 192.168.56.0/24
```

```text
Nmap scan report for 192.168.56.101
Host is up (0.00042s latency).   (salida de ejemplo)
```

`-sn` hace un *ping sweep*: descubre hosts vivos **sin** escanear puertos. Perfecto para saber qué IP
tiene tu nueva víctima.

**3. Levantar Juice Shop con Docker** (si tienes Docker instalado). El nombre de la imagen puede
cambiar: confírmalo en la documentación del proyecto en [https://owasp.org](https://owasp.org).

```bash
docker run --rm -p 3000:3000 bkimminich/juice-shop
```

```text
info: Server listening on port 3000   (salida de ejemplo)
```

Luego abres `http://localhost:3000` en el navegador. `--rm` borra el contenedor al pararlo; `-p
3000:3000` publica el puerto.

**4. Comprobar que tu víctima está aislada.** Desde tu Kali, mira tus interfaces:

```bash
ip -brief address
```

```text
lo      UNKNOWN  127.0.0.1/8
eth0    UP       10.0.2.15/24
vboxnet0 UP      192.168.56.1/24   (salida de ejemplo)
```

Si tu interfaz de laboratorio (por ejemplo `vboxnet0`) no tiene salida a Internet, vas por buen camino:
has aislado la red.

## Errores comunes

| Error | Causa | Solución |
| --- | --- | --- |
| La VM de VulnHub no arranca | Imagen corrupta o formato erróneo | Vuelve a descargarla; usa `.ova` para importar |
| No encuentro la IP de la víctima | Red mal configurada | Usa "solo-anfitrión" y `nmap -sn` |
| La app vulnerable es accesible desde fuera | Red en modo "puente" (bridge) | Cámbiala a "red interna"/"solo-anfitrión" |
| "Quiero empezar por bug bounty" | Nivel inadecuado | Domina antes web con PortSwigger |
| Mezclo blue y red team sin criterio | Falta de foco | Elige un objetivo y profundiza |

## Ejercicios

1. **Clasifica plataformas.** Indica si cada una es red team, blue team o bug bounty: LetsDefend,
   VulnHub, HackerOne, Blue Team Labs Online.

    ??? success "Solución"
        - **LetsDefend:** blue team.
        - **VulnHub:** red team (máquinas descargables).
        - **HackerOne:** bug bounty.
        - **Blue Team Labs Online:** blue team.

2. **Descarga y monta una VM de VulnHub.** Busca una etiquetada para principiantes, impórtala y
   averigua su IP.

    ??? success "Solución"
        ```bash
        # tras configurarla en modo "solo-anfitrión" y arrancarla:
        sudo nmap -sn 192.168.56.0/24
        ```

        Debes obtener una IP nueva (salida de ejemplo: `192.168.56.101`). Si hay varias, compara con
        las anteriores para identificar la recién añadida.

3. **Levanta una app web vulnerable.** Instala y arranca OWASP Juice Shop (o DVWA) con Docker y accede
   desde el navegador.

    ??? success "Solución"
        ```bash
        docker run --rm -p 3000:3000 bkimminich/juice-shop
        # abre http://localhost:3000
        ```

        Si `docker` no existe: instálalo siguiendo [https://docs.docker.com](https://docs.docker.com).
        Verás la web vulnerable funcionando.

4. **Diseña tu laboratorio completo.** Dibuja (en Markdown/ASCII) tu laboratorio ideal: atacante,
   víctima y red.

    ??? success "Solución"
        Ejemplo válido:

        ```text
        [Kali - atacante] 192.168.56.10
                 |
        (Red solo-anfitrión 192.168.56.0/24, sin Internet)
                 |
        [Metasploitable - víctima] 192.168.56.101
        [Juice Shop - Docker] 192.168.56.1:3000 (extensión de la víctima)
        ```

5. **Compara gratis vs freemium.** Elige dos plataformas de esta página (una gratis y una freemium) y
   explica en qué se diferencia la experiencia.

    ??? success "Solución"
        Ejemplo: **VulnHub** (gratis) te da control total pero exiges montarlo todo tú; **LetsDefend**
        (freemium) te da un SOC ya montado y guiado, pero funciones avanzadas pueden requerir pago. La
        diferencia clave: **control vs comodidad**.

6. **Investiga una plataforma para blue team.** Entra en la web de Blue Team Labs Online y anota qué
   tipo de retos ofrece.

    ??? success "Solución"
        Deberías ver retos de categorías como **forense, análisis de logs, OSINT, respuesta a
        incidentes** (nombres exactos según la web actual). No hace falta resolver ninguno todavía:
        el objetivo es que sepas **qué hay ahí**.

## Resumen

- Hay vida más allá de las plataformas grandes: máquinas descargables, blue team y bug bounty.
- **VulnHub, Metasploitable, Juice Shop, WebGoat y DVWA** te dan laboratorios gratis en casa.
- **LetsDefend** y **Blue Team Labs Online** son las puertas del blue team.
- El **bug bounty** es legal, pero es un objetivo avanzado, no un punto de partida.
- Tu **laboratorio propio** (VirtualBox/VMware + Docker) es el plan más completo.

## Checklist

- [ ] Sé la diferencia entre red team, blue team y bug bounty.
- [ ] Conozco al menos dos plataformas de máquinas descargables.
- [ ] He montado (o planeado montar) una VM de VulnHub o Metasploitable.
- [ ] He visto cómo levantar una app web vulnerable con Docker.
- [ ] Sé qué es un programa de bug bounty y por qué es legal.
- [ ] Mantengo mi laboratorio aislado de Internet.

## Para ir más allá

- **VulnHub** — Máquinas virtuales vulnerables. Nivel: variable. Idioma: (EN). **Gratis**.
  [https://www.vulnhub.com](https://www.vulnhub.com)
- **Root-Me** — Retos y CTFs. Nivel: principiante-avanzado. Idioma: (EN/FR). **Freemium**.
  [https://www.root-me.org](https://www.root-me.org)
- **LetsDefend** — Simulador de SOC. Nivel: principiante-medio. Idioma: (EN). **Freemium**.
  [https://letsdefend.io](https://letsdefend.io)
- **Blue Team Labs Online** — Retos defensivos. Nivel: principiante-medio. Idioma: (EN).
  **Freemium**. [https://blueteamlabs.online](https://blueteamlabs.online)
- **pwn.college** — Aprender haciendo sobre sistemas. Nivel: medio-avanzado. Idioma: (EN). **Gratis**.
  [https://pwn.college](https://pwn.college)
- **OWASP** — Proyectos y apps vulnerables (Juice Shop, WebGoat). Nivel: todos. Idioma: (EN).
  **Gratis**. [https://owasp.org](https://owasp.org)
- **Docker** — Contenedores para tus laboratorios. Idioma: (EN). **Gratis**.
  [https://docs.docker.com](https://docs.docker.com)

## Siguiente paso

Ya sabes dónde practicar. Hora de montarlo todo tú mismo de principio a fin:
**[Primer laboratorio](../07-primer-laboratorio.md)**.
