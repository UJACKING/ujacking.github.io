# Política de seguridad

## Qué cubre este documento

Este documento explica cómo **reportar** dos tipos de problemas:

1. **Problemas de seguridad del propio repositorio o de la web** (por ejemplo: un secreto filtrado,
   una dependencia vulnerable, un fallo en los workflows de despliegue).
2. **Contenido peligroso o inapropiado** publicado en la web (por ejemplo: una guía que podría usarse
   para atacar sistemas ajenos, enlaces a malware, datos personales filtrados).

## Cómo reportar

Envía un correo a **ujackingoficial@gmail.com** con:

- Una descripción clara del problema.
- Pasos para reproducirlo (si aplica).
- Impacto que crees que tiene.
- Cómo prefieres que te contactemos para darte seguimiento.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Definir un canal de reporte privado dedicado (correo específico de seguridad o *GitHub Security
    Advisories*) y quién forma parte del equipo que lo atiende.

Por favor, **no abras un issue público** para problemas de seguridad sensibles.

## Qué puedes esperar

- Acuse de recibo en un plazo razonable (objetivo: 72 horas).
- Confirmación del problema y, si procede, plan de corrección.
- Crédito en el aviso público si lo deseas.

!!! warning "PENDIENTE (TODO-UJACKING)"
    Concretar plazos de respuesta comprometidos y si la asociación publicará avisos de seguridad.

## Divulgación responsable

Pedimos un margen razonable para corregir el problema antes de hacerlo público. Del mismo modo, esta
comunidad se compromete a **no** exponer públicamente fallos de terceros sin haber contactado antes
con la persona u organización responsable.

## Secretos y credenciales

- **Nunca** subas tokens, contraseñas o claves al repositorio.
- Si detectas un secreto en el historial de Git, avisa de inmediato: habrá que **revocarlo** y
  reescribir el historial.

Reportar un secreto filtrado es siempre bienvenido, incluso si es tuyo.
