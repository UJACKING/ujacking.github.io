# Elegir distro de hacking

Ya sabes usar Linux y Windows. Antes de montar tu máquina de atacante hay que responder una pregunta:
**¿Kali o Parrot?** Las dos son excelentes, las dos son gratuitas y las dos sirven. Sus diferencias son
reales pero **menores** para un principiante. Lo verdaderamente importante de esta página es entender qué
es una **distro "de ataque"**, para qué sirve y por qué **no** debe ser tu sistema del día a día.

## Objetivos de aprendizaje

- Explicar qué es una **distribución de hacking** (o "de ataque") y qué la diferencia de una normal.
- Conocer las **diferencias reales** entre **Kali Linux** y **Parrot OS**.
- Decidir con criterio cuál usar y por qué.
- Entender por qué **ninguna** de las dos se usa como sistema diario.
- Conocer las **alternativas** para el uso diario sin renunciar a un laboratorio.

**Tiempo estimado:** 40–60 min.

## Requisitos previos

- **[01 · Linux · fundamentos](01-linux-fundamentos.md)**: qué es una distribución.
- **[04 · Windows · básico](04-windows-basico.md)** (contexto del otro sistema).

## Explicación

### ¿Qué es una distro "de ataque"?

Una **distribución de hacking** (también llamada "de pentesting" o "de seguridad ofensiva") es una
distribución Linux normal a la que se le ha añadido:

1. Un **conjunto enorme de herramientas** de seguridad (escaneo, explotación, análisis de red, forense…)
   ya instaladas y configuradas.
2. **Ajustes pensados para el atacante**: repositorios propios, controladores para inyectar paquetes en
   Wi-Fi, anonimato de base, etc.
3. Una **comunidad y documentación** orientadas a ese trabajo.

La ventaja es la comodidad: en lugar de instalar 200 herramientas a mano, vienen listas. La
desventaja es justo eso: llevas 200 herramientas potentes en el bolsillo, y usarlas **fuera de tu
laboratorio es ilegal**.

!!! danger "Una distro de ataque no es una licencia para atacar"
    Tener nmap o Metasploit instalados **no** te autoriza a usarlos contra nada que no sea **tu
    laboratorio** o una plataforma que te lo permita por escrito. La herramienta no es el delito; el uso
    sin autorización sí lo es. Repasa **[00 · Ética y legalidad](../00-etica-y-legalidad.md)**.

### Kali Linux

Es la distro de pentesting más conocida del mundo. Detalles que conviene saber (y que **confirma siempre
en la web oficial**, porque cambian):

- **Base:** Debian, en modelo **rolling release** (se actualiza continuamente, sin "versiones" cerradas).
- **Mantenedor:** Offensive Security.
- **Enfoque:** cobertura amplísima de herramientas; estándar de facto y el que más documentación tiene.
- **Variantes:** para **VirtualBox/VMware** (imágenes ya hechas), **WSL** (dentro de Windows), **ARM**
  (Raspberry Pi), **móvil** (Kali NetHunter) y **Live USB**.
- **Escritorio:** por defecto suele ser **Xfce** (ligero), con otras opciones disponibles.
- **Documentación y comunidad:** muy grandes, casi siempre en inglés.

Web oficial: [https://www.kali.org](https://www.kali.org)

### Parrot OS

Es la otra gran referencia, con una filosofía algo distinta: **más centrada en la privacidad** y en un
sistema más ligero.

- **Base:** Debian, también **rolling release**.
- **Enfoque:** pentesting **+ privacidad** + forense. Incluye utilidades como **AnonSurf** (para enrutar
  tráfico por la red **Tor**) y herramientas de anonimato.
- **Ediciones:** una orientada a seguridad (**Security**) y otra para **uso doméstico** (**Home**), además
  de variantes para cloud y otros usos.
- **Escritorio:** por defecto suele ser **MATE**, con otras opciones.
- **Tamaño y consumo:** tiende a ser **más ligera** que Kali en instalaciones por defecto.

Web oficial: [https://parrotsec.org](https://parrotsec.org)

!!! warning "Sé prudente con las versiones y ediciones"
    Kali y Parrot cambian de escritorio, ediciones y paquetes con frecuencia. No memorices "la edición
    X es la que trae Y": **consulta la web oficial** en el momento de descargar.

### Kali vs Parrot: comparación honesta

| Criterio | Kali Linux | Parrot OS |
| --- | --- | --- |
| Base | Debian (rolling) | Debian (rolling) |
| Ecosistema y documentación | El más grande; referencia en tutoriales | Bueno, algo menor |
| Enfoque | Cobertura máxima de herramientas | Privacidad + pentesting + forense |
| Peso de la instalación | Medio (depende de la edición) | Suele ser más ligero |
| Anonimato por defecto | No de serie | Incluye utilidades tipo AnonSurf |
| Uso como sistema diario | Desaconsejado | Desaconsejado (pero su edición *Home* está pensada para ello) |
| Recursos recomendados | Consulta la web oficial | Consulta la web oficial |

Para un principiante, la respuesta práctica es simple:

- Si quieres el **camino con más tutoriales y ayuda**, empieza con **Kali**.
- Si te importa un sistema **más ligero y con enfoque en privacidad** y ya te manejas, **Parrot** es igual
  de válido.
- **Da igual con cuál empieces**: las herramientas son las mismas y las vas a poder usar en las dos.

### Requisitos: cuidado con los números

Aquí **no hay cifras universales**. Los requisitos dependen de la edición, del escritorio y de si añades
máquinas objetivo en la misma máquina. En lugar de darte números inventados:

!!! warning "PENDIENTE (TODO-UJACKING)"
    Confirmar y actualizar las cifras mínimas y recomendadas de RAM/disco para Kali y Parrot **desde sus
    webs oficiales** (https://www.kali.org y https://parrotsec.org) cuando se revise el contenido.

**Orientación** (referencial, no oficial): para virtualizar con holgura lo normal es trabajar con **8–16 GB
de RAM** en el equipo anfitrión, reservando **2–4 GB** a la máquina de ataque y **1–2 GB** a cada objetivo
ligero. El disco de la VM de ataque suele ir de **20 GB hacia arriba**. Ajusta según tu equipo.

### ¿Por qué NO usar una distro de ataque como sistema diario?

Es una de las preguntas que más se hacen los principiantes: "si Kali lo hace todo, ¿por qué no lo instalo
y ya está?". Hay tres razones de peso:

1. **Seguridad.** Vas a navegar por Internet, leer correo y abrir ficheros con un sistema que trae
   herramientas ofensivas, servicios activados y configuraciones pensadas para atacar. Si te comprometen
   esa máquina, comprometen **tu arma**. Además, una distro de ataque no está endurecida pensada para
   producción.
2. **Estabilidad.** Al ser **rolling release**, los paquetes cambian continuamente y pueden romper
   cosas. Un sistema de trabajo debe ser **aburrido y estable**, no la última versión de todo.
3. **Separación de identidades.** Si tu sistema de ataque y tu vida personal son el mismo, un writeup
   filtrado o una acción sin autorización te señalan directamente a ti. **Separa siempre** el sistema de
   ataque del sistema personal.

!!! tip "La forma correcta de trabajar"
    - **Sistema diario:** una distro estable y normal (Ubuntu, Debian, Fedora, Linux Mint, o tu Windows).
    - **Sistema de ataque:** Kali o Parrot, **en una máquina virtual aislada** (lo montas en la
      [página 06](06-montar-kali-y-parrot.md)).
    - **Objetivos:** otras VMs en una red interna (páginas
      [07](07-laboratorio-red-virtual.md) y [08](08-maquinas-objetivo.md)).

Así, si estropeas la VM de ataque practicando, la restauras con un **snapshot** en segundos y tu equipo
real sigue intacto.

### Alternativas y matices

- **WSL (Windows Subsystem for Linux):** te permite tener Linux dentro de Windows. Cómodo para estudiar y
  para usar algunas herramientas. Tiene límites con la red y la virtualización; para un laboratorio
  completo, sigue siendo mejor una VM. Comprueba en la documentación oficial qué soporta tu versión.
- **Contenedores Docker:** perfectos para **levantar objetivos web** (páginas 07 y 08), pero no sustituyen
  a una VM de ataque.
- **Distros normales con herramientas sueltas:** puedes instalar las herramientas que necesites en Ubuntu
  o Debian y tener un laboratorio sin cambiar de sistema. Es lo que hacen algunos profesionales.

## Ejemplos prácticos

Comprobar qué distribución tienes delante (sirve igual en Kali y en Parrot):

```bash
cat /etc/os-release | head -n 6
cat /etc/debian_version
```

```text
PRETTY_NAME="Kali GNU/Linux rolling"
NAME="Kali GNU/Linux"
ID=kali
ID_LIKE=debian
```

*(salida de ejemplo para Kali. En Parrot verás `ID=parrot` y su nombre correspondiente.)* `debian_version`
te confirma la base común de ambas.

Comprobar cuándo se actualizó un paquete concreto del sistema de seguridad:

```bash
apt policy nmap
```

```text
nmap:
  Instalados: 7.94+git20230807.3be01efb1-3
  Candidato:  7.94+git20230807.3be01efb1-3
```

*(salida de ejemplo)* Verás la versión instalada y la disponible en los repositorios. No fijes una versión
"de moda": lo importante es tener el repositorio oficial y actualizar.

## Errores comunes

| Error | Por qué ocurre | Solución |
| --- | --- | --- |
| Instalar Kali como sistema principal | Parece cómodo. | Usa tu sistema normal y Kali en una VM. |
| Comparar "cuál es mejor" hasta el infinito | Distrae del aprendizaje. | Elige una (Kali suele ser el camino con más ayuda) y empieza. |
| Añadir repositorios de otras distros | Rompe la coherencia del sistema. | Usa **solo** los repositorios oficiales de tu distro. |
| Creer que traer herramientas == ser atacante | Confundir herramienta con conocimiento. | Aprende los fundamentos: redes, sistemas, metodología. |
| AnonSurf = anonimato total | Uso indebido de Tor. | Es una herramienta más; no te vuelve invisible por sí sola. |

## Ejercicios

1. **Investiga la versión vigente.** Entra en las webs oficiales de Kali y Parrot y anota: qué ediciones
   ofrecen hoy y para qué sirve cada una.
2. **Compara tres puntos.** Elabora tu propia tabla con tres diferencias que te importen a ti (escritorio,
   peso, herramientas incluidas).
3. **Decide y justifica.** Elige Kali o Parrot y escribe dos frases explicando por qué.
4. **Requisitos reales.** Consulta en la web oficial los requisitos recomendados y anótalos para tu
   equipo.
5. **Uso diario.** Propón un plan en el que tu sistema diario y tu sistema de ataque estén **separados**,
   usando los recursos de tu equipo.

??? success "Solución"
    1. Las ediciones cambian; por eso el ejercicio consiste en consultarlas. Kali ofrece variantes de
       escritorio y formatos (VM, ARM, WSL, móvil…); Parrot ofrece al menos una edición *Security* y una
       *Home*, además de otras. No hay una respuesta "fija": lo importante es saber dónde mirarlo.
    2. Ejemplo de tabla personal: *(1)* escritorio por defecto, *(2)* peso de la ISO/instalación,
       *(3)* si incluye utilidades de privacidad como AnonSurf.
    3. Respuesta libre, pero bien justificada. Ej.: "Elijo Kali porque casi todos los tutoriales están
       hechos para ella, y al empezar necesito ayuda".
    4. En las webs oficiales aparecen los requisitos; apúntalos y compáralos con tu RAM y disco libres.
       Si no te llega, plantéate usar **WSL** o una VM ligera con menos escritorio.
    5. Plan válido: sistema diario estable + Kali/Parrot en VM (2–4 GB) + objetivos ligeros (1–2 GB) +
       snapshots. Si el equipo es flojo, **no enciendas todo a la vez**.

## Resumen

- Una **distro de hacking** es Linux + herramientas de seguridad + repositorios propios.
- **Kali** = máxima cobertura, más documentación y ecosistema (Debian rolling).
- **Parrot** = enfoque en **privacidad** y ligereza (Debian rolling), con edición *Home* para el día a día.
- Para empezar, cualquiera de las dos vale; los tutoriales empujan hacia Kali.
- **Nunca** como sistema diario: riesgo de seguridad, inestabilidad y falta de separación de identidades.
- La pauta correcta: **sistema diario estable + distro de ataque en VM + objetivos aislados**.

## Checklist

- [ ] Sé qué es una distro de hacking y qué la diferencia de una normal.
- [ ] Conozco las diferencias reales entre Kali y Parrot.
- [ ] He decidido con qué distro empiezo y por qué.
- [ ] Entiendo por qué no debo usar Kali/Parrot como sistema diario.
- [ ] Sé cuáles son las alternativas para el uso diario (distro normal, WSL).
- [ ] Tengo claro que todo se practica en laboratorio o plataforma autorizada.

## Para ir más allá

| Recurso | Tipo | Idioma | Precio |
| --- | --- | --- | --- |
| [Kali Linux](https://www.kali.org) | Web y documentación oficial | EN | Gratis |
| [Parrot OS](https://parrotsec.org) | Web y documentación oficial | EN | Gratis |
| [Ubuntu](https://ubuntu.com) | Sistema recomendado para el día a día | Multi | Gratis |
| [Debian](https://www.debian.org) | Sistema estable para el día a día | Multi | Gratis |

## Siguiente paso

Elegida la distro, vamos a montarla bien y **verificando la descarga**:
**[06 · Montar Kali y Parrot](06-montar-kali-y-parrot.md)**.
