# HuellaIP: huellas

**Las huellas publicadas de HuellaIP: el comportamiento de red normal de cada dispositivo, por modelo y firmware.**

Cada huella describe con quién habla un dispositivo, cuántas sesiones abre, cuánto tráfico mueve y a qué ritmo, en cada estado de uso. Los routers comparan el tráfico real contra la huella para detectar cuándo un equipo empieza a comportarse como malware.

> [!NOTE]
> **Estado: fase 0.** Todavía no hay huellas publicadas. Las primeras cuatro, de dispositivos cableados medidos en el laboratorio del proyecto, están previstas para la fase 2 del prototipo. Si querés proponer una, empezá por [CONTRIBUTING.md](CONTRIBUTING.md).

## In English

This repository holds the published *huellas* (Spanish for "footprints") of the HuellaIP project: network behavior profiles of home and small-business devices, one file per device model and firmware version. Each profile is a valid MUD file (RFC 8520) with a quantitative extension. Profiles are released under CC-BY-4.0. Metadata only, never content. The format, lab and tools live in [`huellaip/huellaip`](https://github.com/huellaip/huellaip).

## Qué es una huella

Una huella es un archivo JSON que cumple dos cosas a la vez:

- Es un archivo **MUD** válido ([RFC 8520](https://www.rfc-editor.org/info/rfc8520)): cualquier herramienta que entienda MUD puede leer los destinos permitidos.
- Lleva, dentro del contenedor MUD, la extensión **`huellaip-perfil`**, con las métricas de cada estado de uso (`encendido`, `reposo`, `activo` e `interaccion`):
  - sesiones concurrentes;
  - bytes subidos y bajados por hora;
  - conexiones nuevas por minuto;
  - periodicidad de los keepalives;
  - destinos esperados (dominios y ASN);
  - versiones de TLS observadas.

El formato se define en el repo [`huellaip/huellaip`](https://github.com/huellaip/huellaip), en `especificacion/`. Si este README y la especificación dicen cosas distintas, manda la especificación.

## Estructura del repositorio

```text
huellas/
├── README.md
├── LICENSE                 CC-BY-4.0
├── CONTRIBUTING.md         cómo proponer y revisar una huella
├── huellas/
│   └── <categoria>/<fabricante>/<modelo>/<firmware>.json
└── .github/                plantillas de issues y PR, y la validación automática
```

Un ejemplo de ruta: `huellas/camara/fabricante-ejemplo/x1/2.4.1.json`. Las reglas para armar la ruta están en [CONTRIBUTING.md](CONTRIBUTING.md#dónde-va-el-archivo).

## Etiquetas y niveles de confianza

Cada huella declara una **etiqueta**, que describe el comportamiento observado de ese modelo con ese firmware. No es un juicio sobre la marca: una huella no recomienda ni desaconseja dispositivos.

| Etiqueta | Qué significa |
|---|---|
| `benigno` | No se observó nada que su categoría no haga normalmente |
| `sospechoso` | Se observó un comportamiento anómalo para su categoría, sin un indicador de compromiso confirmado |
| `malicioso` | El comportamiento coincide con un indicador de compromiso (IOC) documentado. La huella cita la fuente |

Cada huella declara también un **nivel de confianza**:

| Nivel | Criterio (propuesta del plan, se fija en la metodología de captura) |
|---|---|
| `baja` | Una sesión por estado, en un solo laboratorio |
| `media` | Las repeticiones mínimas completas y 72 horas de reposo |
| `alta` | Nivel `media` más una réplica en un segundo laboratorio o con datos de un ISP |

## Cómo usar una huella

- **Para leerla:** cada archivo es JSON legible. La parte MUD sirve sin cambios en herramientas que ya entienden MUD.
- **Para cargarla en un router:** los exportadores de [`huellaip/huellaip`](https://github.com/huellaip/huellaip) van a generar las reglas. El primero, para RouterOS, está previsto para la fase 3 del prototipo; después viene OpenWrt.
- **Con prudencia:** usá las reglas en modo solo alerta. Una huella refleja un firmware y unas condiciones de captura concretos, así que un desvío es una señal para revisar, no una prueba de compromiso.

## Privacidad

Las huellas solo tienen metadatos agregados. Nunca incluyen:

- contenido de las comunicaciones;
- capturas ni logs crudos;
- direcciones MAC completas (como mucho, el OUI, que identifica al fabricante);
- números de serie;
- cuentas, correos ni otros identificadores personales;
- direcciones IP privadas ni la IP pública del laboratorio o de quien aporta.

Cada propuesta pasa por un chequeo de privacidad antes de publicarse. Si encontrás un dato que no debería estar, avisá por el canal privado: [huellaip@googlegroups.com](mailto:huellaip@googlegroups.com).

## Cómo participar

- **Proponer una huella:** seguí [CONTRIBUTING.md](CONTRIBUTING.md).
- **Revisar huellas:** cualquiera puede comentar los PRs abiertos. La aprobación final la da el comité técnico.
- **Aportar código, metodología o laboratorio:** andá a [`huellaip/huellaip`](https://github.com/huellaip/huellaip).

## Licencia y atribución

Las huellas se publican bajo [Creative Commons Atribución 4.0 Internacional](LICENSE) (CC-BY-4.0). Se pueden usar, adaptar y redistribuir con cualquier fin, también comercial, siempre que se reconozca la autoría.

Cómo atribuir una huella:

> Huella de *\<fabricante\> \<modelo\>*, firmware *\<versión\>*. HuellaIP, aportada por *\<aportante\>*. CC-BY-4.0. https://github.com/huellaip/huellas

Las huellas se ofrecen tal como están, sin garantías, como dice la licencia.

## Gobernanza

Este repositorio se rige por la [gobernanza de HuellaIP](https://github.com/huellaip/huellaip/blob/main/GOVERNANCE.md). Cada huella necesita dos aprobaciones, y una de ellas tiene que ser de alguien del comité técnico. Quien revisa no puede pertenecer a la organización que aporta la huella ni a una que fabrique o venda ese dispositivo.

## Contacto

- **Preguntas y propuestas:** issues de este repositorio, o el repo [`huellaip/huellaip`](https://github.com/huellaip/huellaip).
- **Datos sensibles publicados por error o problemas de seguridad:** [huellaip@googlegroups.com](mailto:huellaip@googlegroups.com). No abras un issue público.
