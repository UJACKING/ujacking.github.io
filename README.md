# UJACKING

Recursos y guías **gratuitas** para aprender **ciberseguridad desde cero**.

🌐 **Web:** <https://ujacking.github.io/>
💬 **Discord:** <https://discord.gg/Gc4fhMn5bG>
✉️ **Contacto:** <ujackingoficial@gmail.com>

!!! warning "PENDIENTE (TODO-UJACKING)"
    Confirmar por parte de la asociación: vinculación oficial con la Universidad de Jaén (UJA),
    fecha de fundación, directiva y estatutos. Ver `PENDIENTES.md`.

## ¿Qué es esto?

Esta web es la recopilación de recursos, guías y rutas de aprendizaje de **UJACKING**, una
asociación dedicada a la divulgación y formación en ciberseguridad. Está pensada para personas que
**empiezan desde cero**: no asumimos conocimientos previos más allá de saber usar un ordenador.

El material se publica como sitio estático con **MkDocs + Material for MkDocs** y se mantiene con
**Pull Requests** de los miembros de la comunidad.

## Estructura de niveles

- **Nivel 1 · Principiante:** la base. Arquitectura de ordenadores, redes, sistemas operativos,
  Bash, Git, dónde practicar y tu primer laboratorio. *Es la prioridad y la parte más completa.*
- **Nivel 2 · Medio:** Linux avanzado, Active Directory, redes avanzadas, Python para seguridad,
  Nmap, pentesting web, Burp, Metasploit, criptografía, forense y OSINT.
- **Nivel 3 · Avanzado:** certificaciones ofensivas (eJPT, CPTS, OSCP) y otras habituales.

Además: **Ruta perfecta** (plan de 12 semanas), **Paths** (hojas de ruta por área),
**Empleabilidad** y un **glosario**.

## Ejecutar la web en local

Requisitos: Python 3.10 o superior y Git.

```bash
# 1. Clona el repositorio
git clone https://github.com/UJACKING/ujacking.github.io.git
cd ujacking.github.io

# 2. Crea y activa un entorno virtual
python3 -m venv .venv
source .venv/bin/activate        # En Windows: .venv\Scripts\activate

# 3. Instala las dependencias
pip install -r requirements.txt

# 4. Arranca el servidor de desarrollo
mkdocs serve
```

Abre <http://127.0.0.1:8000/>. El navegador se recarga solo al guardar cambios.

Para comprobar que todo compila igual que en el CI (modo estricto):

```bash
mkdocs build --strict
```

## Cómo contribuir

1. Lee [`CONTRIBUTING.md`](CONTRIBUTING.md) y el [código de conducta](CODE_OF_CONDUCT.md).
2. Haz un *fork*, crea una rama descriptiva y abre un **Pull Request**.
3. El PR debe pasar la comprobación `build` (build estricta de MkDocs).

¿Nuevo por aquí? Empieza por [Contribuir](https://ujacking.github.io/contribuir/).

## Aviso ético y legal

Todo el material ofensivo (escaneos, explotación, análisis) está pensado **exclusivamente** para
practicar contra:

- máquinas y redes **propias** de tu laboratorio aislado, o
- plataformas que **autorizan explícitamente** la práctica (TryHackMe, Hack The Box, VulnHub,
  PortSwigger Academy, etc.).

Atacar sistemas de los que no eres responsable es un delito. Esta web **no** contiene malware
funcional ni instrucciones para atacar sistemas reales. Ver
[Ética y legalidad](https://ujacking.github.io/nivel-1-principiante/00-etica-y-legalidad/).

## Licencia

- **Contenido** (textos de las guías, imágenes propias): **CC BY-SA 4.0**.
- **Código** (scripts, plantillas, configuración): **MIT**.

Ver [`LICENSE`](LICENSE).

!!! warning "PENDIENTE (TODO-UJACKING)"
    La licencia definitiva debe ser confirmada por la directiva de la asociación.
