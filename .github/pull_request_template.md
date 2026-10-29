## Huella

- **Dispositivo:** <!-- fabricante, modelo y firmware -->
- **Archivo:** <!-- huellas/<categoria>/<fabricante>/<modelo>/<firmware>.json -->
- **Issue:** <!-- Closes #… -->
- **Origen de la captura:** <!-- laboratorio de HuellaIP, laboratorio que replica la maqueta, datos agregados de un ISP u otro -->
- **Etiqueta y nivel de confianza:** <!-- p. ej., benigno · media -->

## Captura

<!-- Fechas, repeticiones por estado, horas de reposo y firmware registrado antes y después de la captura. Si falta un estado, explicá por qué. -->

## Evidencia

<!-- Obligatorio para "sospechoso" y "malicioso": qué se observó, con metadatos agregados, y la fuente del IOC si corresponde. -->

## Checklist de quien aporta

- [ ] El archivo valida contra el esquema de la versión del formato que declara.
- [ ] La ruta coincide con categoría, fabricante, modelo y firmware.
- [ ] No hay contenido de comunicaciones, MAC completas, números de serie, cuentas, IPs privadas ni la IP pública del laboratorio.
- [ ] No hay dominios con identificadores únicos del equipo o de la cuenta: si los había, están reemplazados por un comodín.
- [ ] Todos los commits están firmados (`git commit -s`), y con eso certifico que la captura es mía o que tengo el consentimiento necesario.

## Notas para la revisión

<!-- Dudas, dominios a resolver, diferencias con la especificación. -->
