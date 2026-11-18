# JustificatorIA

Informes de justificación de ayudas: lo solicitado frente a lo ejecutado. Aplicación web de un solo fichero.

**Usar la app:** https://fborrasumh.github.io/justificatoria/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24348000.svg)](https://doi.org/10.5281/zenodo.24348000)

**Idiomas:** español (por defecto), inglés, portugués; selector en la barra superior (o `?lang=en` / `?lang=pt` en la URL).

## Para qué sirve

Para el personal técnico que revisa la justificación de una convocatoria de ayudas (pensada para el Servicio de Relaciones Internacionales de la UMH y el programa PRODIC-UMH, válida para otras convocatorias). A partir de la carpeta de la convocatoria (bases y resoluciones, solicitudes y justificaciones, con una carpeta por solicitante, tal como se descarga de Google Drive) prepara un informe justificativo por solicitante y una tabla resumen.

## Qué hace el código (determinista: mismos documentos, mismo resultado)

- Lee la carpeta o el ZIP (o varios ZIP) en el navegador: PDF y Word (.docx); los .doc antiguos y los PDF escaneados se señalan.
- Empareja solicitud y justificación de cada persona aunque el nombre esté escrito distinto (tildes, «M.»/«Mª», sufijos como «_SIN SOLICITUD SEDE»); lo que no empareja, se une a mano.
- Reconoce cada anexo (III, IV, V, situación de crédito, encuesta, registro…) por el nombre del fichero o por su texto, y la anualidad por la subcarpeta; si hay dos versiones (NUEVO/ANTIGUO, CORRECTA/INCOMPLETA) usa la buena.
- Lee la fecha de la **firma digital** de cada PDF y la compara con los plazos de las bases.
- Lee la **situación de crédito de UXXI-EC**: transferencias, pagos (proveedor, NIF, importe, fechas) y crédito sin pagar; reparte los pagos entre transferencias con una **suma exacta al céntimo** y, si hay varias formas, elige la que mejor encaja con los documentos y lo avisa (el técnico puede fijar la imputación a mano).
- Lee el listado de la **resolución de concesión** (o de varias: una resolución con otro código de ayuda, como la de visitas preparatorias, sirve para no imputar sus pagos al proyecto).
- Aplica topes (por proyecto, €/hora y horas de profesorado externo), periodos de ejecución, pagos a miembros del equipo y copia literal entre anexo IV y memoria final.
- Calcula una **propuesta de dictamen** con reglas fijas: justificado, con reparos, requiere subsanación, propuesta de reintegro (con importe orientativo) o no concedido.

## Qué hace la IA (y cómo se comprueba)

- Compara lo prometido en la memoria de solicitud (actividades, objetivos, difusión, presupuesto) con lo que dicen la memoria final y la justificación económica, y propone si cada gasto encaja en los conceptos subvencionables de las bases.
- Cada afirmación lleva una **cita literal**; el código la busca en el documento. Si la IA dice «realizada» y la cita no está en la justificación, pasa a «sin evidencia». Una obligación «cumplida» sin cita verificada queda en «no consta».
- Opcionalmente, extrae el **perfil de una convocatoria nueva** a partir de sus bases (con citas que se comprueban contra las bases) y el listado de una resolución que el código no sepa leer.
- La IA **no decide**: el técnico confirma o cambia el dictamen, con motivación obligatoria si se aparta de la propuesta, y firma con su nombre.

## Otras convocatorias

Todo lo que depende de unas bases vive en el **perfil** (JSON): documentos esperados y cómo reconocerlos, plazos, periodos de ejecución, topes, conceptos subvencionables, prohibiciones, obligaciones y marcas de carpeta. Viene el de PRODIC-UMH 2025 (RR 00472/2025, con citas literales); para otra convocatoria se extrae de sus bases con la IA, se edita en la app, se exporta y se importa.

## Cómo se usa la IA

Con la propia clave de OpenAI, Google Gemini o Anthropic Claude. La clave se guarda solo en el navegador. No hace falta servidor. Una llamada por expediente; conviene probar primero con uno.

## Privacidad

- Los documentos se leen y el trabajo (textos extraídos, análisis y dictámenes) se guarda **solo en el navegador** (IndexedDB). Se puede exportar a un JSON que contiene datos personales de los solicitantes: guárdelo donde se guardan los expedientes. El JSON no incluye la clave de IA.
- Al analizar un expediente con la IA salen hacia el proveedor el texto de sus anexos y sus datos contables, con DNI/NIE (también con guion o enmascarados), correos y teléfonos sustituidos por marcas; **los nombres de las personas sí se envían** (hacen falta para cuadrar pagos). Antes del primer envío se muestra lo que sale y se pide confirmación. Compruebe con su servicio si su proveedor y su tipo de cuenta son adecuados para estos datos.

## Límites

- No sustituye la revisión del técnico: la propuesta es orientativa y la valoración de la IA sobre un gasto puede equivocarse.
- Los PDF escaneados no se leen por código. La lectura de la situación de crédito está hecha para los informes de UXXI-EC de la UMH; otros formatos se señalan como ilegibles.
- La fecha de presentación se toma de la firma digital del PDF; los documentos sin firma (p. ej. enviados por formulario) no se pueden comprobar contra el plazo, y la app lo dice.
- El reparto de pagos entre transferencias puede tener varias soluciones exactas; la app avisa y el técnico decide.
- Probado con IA simulada y con expedientes reales de PRODIC 2025 en local (lectura, firmas, situación de crédito, resolución); no probado aún con una clave real de IA.

## Ejemplo

«Ver un ejemplo (ficticio)» carga cuatro expedientes inventados (personas, proyectos, importes y documentos) sin usar la IA: uno justificado, uno que requiere subsanación (firma fuera de plazo, memoria genérica, falta la encuesta, una cita inventada por la IA que el código rechaza), uno con propuesta de reintegro (400 € sin pagar) y una solicitud no concedida.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche).


ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573)

## Cómo citar

Borrás Rocher, F. (2026). *JustificatorIA* (v1.0.0) [Software]. https://doi.org/10.5281/zenodo.24348000

## Licencia

MIT. Véase [LICENSE](LICENSE).
