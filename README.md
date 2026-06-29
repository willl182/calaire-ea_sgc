# Sistema de Gestion de Calidad CALAIRE-EA

Repositorio documental del Sistema de Gestion de Calidad del Programa de Ensayos de Aptitud de CALAIRE-EA para gases contaminantes criterio: CO, NO/NO2, SO2 y O3.

El repositorio organiza documentos marco, procedimientos, instructivos, formatos maestros, matrices, fichas resumen, mapas de navegacion y evidencias por ronda. Su proposito es mantener una arquitectura documental trazable para operar ensayos de aptitud alineados con ISO/IEC 17043:2023 e ISO 13528:2022.

## Como leer este repositorio

Use estos archivos como puntos de entrada:

| Archivo | Uso |
|---|---|
| `01_bloque_general/05_matrices_inventarios/Inventario Documental del SGC.md` | Inventario vigente de codigos, nombres, estados y ubicaciones. |
| `01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md` | Regla maestra de arquitectura documental. |
| `01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md` | Regla para carpetas, registros y evidencias por ronda. |
| `01_bloque_general/02_procedimientos/P-PSEA-08 Flujo tecnico de datos digitales del PEA.md` | Flujo de captura, exportacion, preprocesamiento, analisis e informe. |
| `mapa_navegacion_sgc_pea.html` | Mapa interactivo de relaciones entre documentos, aplicativos y formatos. |
| `fichas_resumen/index.html` | Indice navegable de fichas resumen documentales. |
| `doc_calaire-ea.md` | Explicacion tecnica y operativa del modelo CALAIRE-EA. |
| `documento-sgc.md` | Memoria historica de construccion, decisiones y aprendizajes del SGC. |

## Arquitectura vigente

La estructura documental vigente separa documentos maestros de evidencias de ejecucion:

| Ruta | Funcion | Regla |
|---|---|---|
| `01_bloque_general/` | SGC maestro del PEA | Contiene documentos marco, procedimientos, instructivos, formatos maestros, matrices e inventarios. |
| `02_despliegue_rondas/` | Registros y evidencias por ronda | Cada ronda conserva `checklist_ronda.md` y carpetas de etapa para planificacion, comunicaciones, preparacion, datos, H/E, analisis e informe, y cierre SGC. |
| `02_prueba_piloto_rondas/` | Fuente historica de piloto | Se conserva como fuente historica. Las evidencias vigentes se copian o reorganizan hacia `02_despliegue_rondas/` cuando corresponda. |
| `fichas_resumen/` | Capa de navegacion documental | Resume proposito, rol, entradas, salidas, relaciones y riesgos de interpretacion de cada documento. |
| `logs/` | Memoria tecnica de trabajo | Registra hallazgos, problemas, planes y estado de sesiones. No reemplaza documentos controlados. |

## Familias documentales

| Familia | Descripcion |
|---|---|
| `DG-PSEA` | Documentos generales o marco. Incluyen documentos de aplicativos como `calaire-app` y `pt_app`. |
| `P-PSEA` | Procedimientos del SGC y procedimientos tecnicos del ensayo de aptitud. |
| `I-PSEA` | Instructivos de uso o ejecucion para tareas especificas. |
| `F-PSEA` | Formatos maestros y registros diligenciables o generados por ronda. |

Los documentos maestros viven en `01_bloque_general`. Las copias diligenciadas o salidas emitidas de una ronda viven en `02_despliegue_rondas/<codigo-ronda>/`.

## Aplicativos documentados

El SGC reconoce dos componentes digitales principales:

- `DG-PSEA-02 Aplicativo calaire-app`: gestion de rondas, participantes, cronogramas, captura/exportacion de datos y casos SGC.
- `DG-PSEA-03 Aplicativo pt_app`: preprocesamiento, consolidacion, analisis estadistico, homogeneidad/estabilidad e informe final.

Ambos documentos marco viven en carpetas propias dentro de `01_bloque_general/01_documentos_marco/`, con Markdown maestro, DOCX, HTML y capturas asociadas. Las capturas son evidencia visual de soporte; no sustituyen procedimientos, instructivos ni validacion de software.

## Flujo basico de una ronda

Una ronda se documenta como una cadena de evidencias:

1. Planificacion: calendario, cronograma, plan de ronda, ficha digital y registro de participante.
2. Comunicaciones: invitaciones, instrucciones, confirmaciones y respuestas.
3. Preparacion del item: equipos, gases, setpoints, verificaciones y condiciones de ensayo.
4. Datos y preprocesamiento: datos reportados, exportacion oficial, revision de estructura, unidades y consistencia.
5. Homogeneidad y estabilidad: registros y subformatos `F-PSEA-11A` a `F-PSEA-11D`.
6. Analisis e informe: dataset oficial, scores, interpretacion, revision y emision del informe.
7. Cierre SGC: quejas, apelaciones, no conformidades, acciones correctivas, competencia o proveedores cuando aplique.

## Reglas de vigencia

Cuando exista conflicto entre documentos o versiones previas, prevalecen:

1. `01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md`
2. `01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md`
3. `01_bloque_general/02_procedimientos/P-PSEA-08 Flujo tecnico de datos digitales del PEA.md`
4. `01_bloque_general/05_matrices_inventarios/Inventario Documental del SGC.md`
5. `mapa_navegacion_sgc_pea.html`

Reglas operativas importantes:

- No reconstruir procedimientos tecnicos por gas desde fichas, transcripciones o Markdown generado. Los `.docx` originales por analito son la fuente valida.
- No reintroducir `indice_capturas.md`, carpetas tecnicas `dgpsea02`/`dgpsea03` ni metadatos no uniformes en `DG-PSEA-02` y `DG-PSEA-03`.
- No tratar logs, scripts auxiliares o capturas como documentos controlados.
- Todo documento nuevo debe incorporarse primero en `P-PSEA-02`, luego en el inventario y finalmente en el mapa de navegacion.
- Los formatos maestros no deben confundirse con copias diligenciadas de ronda.

## Formatos clave

| Codigo | Uso principal |
|---|---|
| `F-PSEA-01` | Calendario global de ronda. |
| `F-PSEA-02` | Cronograma detallado. |
| `F-PSEA-04` | Anexo tecnico de equipos e instrumentos. |
| `F-PSEA-05` | Ficha basica de ronda EA. |
| `F-PSEA-06` | Planificacion de ronda EA. |
| `F-PSEA-07` | Preparacion y control del item. |
| `F-PSEA-08` | Datos reportados por participante. |
| `F-PSEA-09` | Datos exportados para analisis PT. |
| `F-PSEA-10` | Registro de preprocesamiento. |
| `F-PSEA-11` | Homogeneidad y estabilidad del item. |
| `F-PSEA-12` | Datos oficiales consolidados para evaluacion de aptitud. |
| `F-PSEA-13` | Informe final de resultados. |
| `F-PSEA-14` | Registro de queja, trabajo no conforme, no conformidad o accion correctiva. |
| `F-PSEA-15` | Registro de apelaciones. |
| `F-PSEA-16` | Matriz de competencia y autorizacion. |
| `F-PSEA-17` | Evaluacion de proveedores criticos. |
| `F-PSEA-18` | Comunicacion participantes. |

## Herramientas y generacion

Algunos DOCX y HTML se generaron desde Markdown con Pandoc y plantillas institucionales. Esto aplica estilos y estructura, pero no equivale a una revision visual fina en Word. Los documentos generados deben revisarse visualmente antes de uso formal externo.

El mapa de navegacion es un HTML estatico y puede abrirse directamente en el navegador:

```bash
xdg-open mapa_navegacion_sgc_pea.html
```

## Estado actual

El SGC tiene una arquitectura documental amplia y navegable, con separacion entre documentos maestros y evidencias por ronda, documentos marco de aplicativos, procedimientos tecnicos, formatos maestros, fichas resumen y mapa interactivo. Los controles que requieren seguimiento continuo son consistencia entre inventario, mapa, fichas y documentos activos; revision visual de DOCX generados; preservacion de procedimientos originales por gas; y alineacion entre criterios estadisticos documentados, codigo y reportes emitidos.
