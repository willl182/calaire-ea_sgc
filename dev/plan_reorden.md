# Plan detallado de reordenamiento SGC CALAIRE-EA

## Proposito

Materializar la decision tomada en el grill documental: separar claramente el SGC maestro de las evidencias generadas por ronda, crear una estructura operativa repetible para cada ronda y dejar alineados los documentos de control, el mapa de navegacion y la futura migracion manual.

Este plan no convierte la prueba piloto en un bloque documental independiente. La prueba piloto se trata como una o varias rondas dentro de `02_despliegue_rondas/`.

## Principios de implementacion

- `01_bloque_general/` es la fuente maestra del SGC.
- `02_despliegue_rondas/` es el espacio operativo de registros, copias diligenciadas, exportaciones y evidencias por ronda.
- Los formatos maestros no se copian automaticamente al crear una ronda.
- Cada ronda inicia con una estructura minima comun, no parametrizada por tipo de ronda.
- La raiz de cada ronda debe contener solo `checklist_ronda.md` y las siete carpetas de etapa.
- No se crean README generales ni README por ronda.
- La migracion desde `02_prueba_piloto_rondas/` sera manual, copiando evidencias y sin borrar la fuente historica hasta validar.
- El script auxiliar no es documento controlado y no debe tener codigo documental.
- El mapa de navegacion debe representar documentos y formatos activos, pero no debe enlazar el script ni la plantilla.

## Alcance

### Incluido

- Crear `02_despliegue_rondas/` si no existe.
- Crear `plantilla_checklist_ronda.md`.
- Crear `crear_estructura_ronda.sh`.
- Ajustar `P-PSEA-03` para describir la estructura exacta de ronda y los auxiliares.
- Revisar `P-PSEA-02` para consistencia con la separacion maestro/ronda.
- Actualizar `mapa_navegacion_sgc_pea.html` con los formatos faltantes del checklist.
- Probar la creacion de una ronda con codigo valido e invalido.
- Definir la ruta de migracion manual de las rondas piloto.

### Excluido

- Borrar o renombrar `02_prueba_piloto_rondas/`.
- Mover evidencias historicas automaticamente.
- Copiar formatos maestros dentro de cada ronda al crear estructura.
- Crear subcarpetas por estado como `borrador`, `oficial` o `soporte`.
- Convertir auxiliares tecnicos en documentos controlados.
- Reescribir procedimientos tecnicos por analito fuera de ajustes minimos de consistencia.

## Fase 0 - Confirmacion de linea base

Objetivo: asegurar que el trabajo parte de la decision ya documentada y no reabre criterios cerrados.

Actividades:

1. Tomar como fuente principal `decisiones_grill_sgc.md`.
2. Usar `handoff_grill_sgc.md` como resumen de continuidad.
3. Confirmar que existen:
   - `01_bloque_general/02_procedimientos/`
   - `01_bloque_general/04_formatos_maestros/`
   - `02_prueba_piloto_rondas/`
   - `mapa_navegacion_sgc_pea.html`
4. Confirmar si ya existe `02_despliegue_rondas/`.
5. Revisar si ya existen versiones previas de:
   - `crear_estructura_ronda.sh`
   - `plantilla_checklist_ronda.md`
   - `checklist_ronda.md` en rondas existentes

Criterio de cierre:

- Se tiene claro que archivos se crean desde cero y cuales se editan.

## Fase 1 - Crear plantilla de checklist

Objetivo: tener una fuente unica para crear `checklist_ronda.md` en cada ronda.

Archivo objetivo:

```text
01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md
```

Contenido esperado:

- Titulo `# Checklist documental de ronda`.
- Siete secciones, una por etapa.
- Lista de registros `F-PSEA-*` y evidencias complementarias genericas.
- Sin metadatos de ronda.
- Sin rutas.
- Sin estados distintos a checkbox.
- Sin procedimientos ni instructivos.

Checklist que debe contener:

- Planificacion: `F-PSEA-01`, `F-PSEA-02`, `F-PSEA-04`, `F-PSEA-05`, `F-PSEA-05A`, `F-PSEA-06`, `F-PSEA-16`, `F-PSEA-17`.
- Comunicaciones: `F-PSEA-18`, respuestas/acuses y aclaraciones/cambios.
- Preparacion del item: `F-PSEA-07`, certificados y evidencias tecnicas.
- Datos y preprocesamiento: `F-PSEA-08`, `F-PSEA-09`, `F-PSEA-10`, `F-PSEA-12`, CSV/exportaciones.
- Homogeneidad/estabilidad: `F-PSEA-11`, `F-PSEA-11A`, `F-PSEA-11B`, `F-PSEA-11C`, `F-PSEA-11D`.
- Analisis e informe: `F-PSEA-13`, evidencia de envio del informe, salidas/graficas/tablas.
- Cierre SGC: evidencia de cierre, `F-PSEA-14`, `F-PSEA-15`.

Criterio de cierre:

- La plantilla coincide con el checklist acordado en `decisiones_grill_sgc.md`.

## Fase 2 - Crear script auxiliar de estructura

Objetivo: automatizar la estructura minima de una ronda sin tocar evidencias ni formatos maestros.

Archivo objetivo:

```text
01_bloque_general/02_procedimientos/crear_estructura_ronda.sh
```

Reglas funcionales:

- Bash.
- Recibe exactamente un argumento: codigo de ronda.
- Valida el patron:

```regex
^EA-[A-Z0-9]+-[0-9]{4}-R[0-9]+$
```

- Funciona desde cualquier carpeta.
- Resuelve la raiz del repo a partir de la ubicacion del script.
- Crea `02_despliegue_rondas/` si falta.
- Crea `02_despliegue_rondas/<codigo_ronda>/`.
- Crea estas carpetas:

```text
01_planificacion_ronda/
02_comunicaciones_participantes/
03_preparacion_item/
04_datos_y_preprocesamiento/
05_homogeneidad_estabilidad/
06_analisis_e_informe/
07_cierre_sgc/
```

- Crea `.gitkeep` dentro de cada carpeta de etapa.
- Crea `checklist_ronda.md` desde `plantilla_checklist_ronda.md` solo si falta.
- No sobrescribe `checklist_ronda.md` existente.
- No elimina `.gitkeep`.
- No borra archivos.
- No copia formatos maestros.
- Imprime resumen simple al final.

Casos de error:

- Sin argumento: mostrar uso y salir con codigo distinto de cero.
- Mas de un argumento: mostrar uso y salir con codigo distinto de cero.
- Codigo invalido: explicar patron esperado y salir con codigo distinto de cero.
- Plantilla ausente: no crear checklist y reportar error, o fallar antes de crear estructura segun se prefiera para evitar rondas incompletas.

Criterio de cierre:

- El script crea una ronda valida de forma idempotente y rechaza codigos invalidos.

## Fase 3 - Alinear `P-PSEA-03`

Objetivo: que el procedimiento de control de registros refleje la estructura operativa acordada.

Archivo objetivo:

```text
01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md
```

Cambios esperados:

1. En la seccion de estructura simple de ronda, incluir `checklist_ronda.md` en la raiz.
2. Declarar que la raiz de la ronda solo contiene:
   - `checklist_ronda.md`
   - siete carpetas de etapa
3. Listar la estructura bajo `02_despliegue_rondas/<codigo_ronda>/`.
4. Mencionar que la estructura inicial puede generarse con:

```bash
01_bloque_general/02_procedimientos/crear_estructura_ronda.sh <codigo_ronda>
```

5. Aclarar que `crear_estructura_ronda.sh` y `plantilla_checklist_ronda.md` son auxiliares operativos asociados a `P-PSEA-03`, no documentos controlados.
6. Alinear ubicaciones de registros con el checklist.
7. Revisar especialmente `F-PSEA-12`, porque el checklist lo ubica en `04_datos_y_preprocesamiento`.

Criterio de cierre:

- `P-PSEA-03` permite reconstruir la estructura de una ronda sin consultar el handoff.

## Fase 4 - Revisar consistencia de `P-PSEA-02`

Objetivo: mantener la matriz documental como control maestro sin mezclarla con instancias de ronda.

Archivo objetivo:

```text
01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md
```

Cambios esperados:

1. Confirmar que `01_bloque_general/` queda como SGC maestro.
2. Confirmar que `02_despliegue_rondas/` queda como registros/evidencias por ronda.
3. Confirmar que la prueba piloto es ronda y no bloque documental independiente.
4. Revisar ubicaciones de copias diligenciadas para que no contradigan `P-PSEA-03`.
5. Revisar especialmente `F-PSEA-12`.
6. No listar cada instancia diligenciada por ronda.

Criterio de cierre:

- `P-PSEA-02` y `P-PSEA-03` usan la misma arquitectura y no se contradicen.

## Fase 5 - Actualizar mapa de navegacion

Objetivo: que el mapa represente todos los formatos activos del checklist y las relaciones documentales principales.

Archivo objetivo:

```text
mapa_navegacion_sgc_pea.html
```

Nodos faltantes a agregar:

- `F-PSEA-05A`
- `F-PSEA-14`
- `F-PSEA-15`
- `F-PSEA-16`
- `F-PSEA-17`

Relaciones minimas esperadas:

- `P-PSEA-04` -> `F-PSEA-05A`
- `F-PSEA-05` -> `F-PSEA-05A`
- `P-PSEA-15` -> `F-PSEA-14`
- `P-PSEA-17` -> `F-PSEA-14`
- `P-PSEA-18` -> `F-PSEA-15`
- `P-PSEA-20` -> `F-PSEA-16`
- `P-PSEA-21` -> `F-PSEA-17`
- `P-PSEA-03` -> formatos de cierre y gestion que quedan como evidencias de ronda cuando apliquen.

Rutas del mapa a revisar:

- `planning`: debe incluir `F-PSEA-05A`, `F-PSEA-16`, `F-PSEA-17` si se interpretan como evidencias de planificacion.
- `round`: debe incluir todos los formatos esperados del checklist.
- Puede agregarse una ruta `sgc` o equivalente para quejas, apelaciones, competencia y proveedores si la interfaz lo permite sin sobrecargar el mapa.

Regla negativa:

- No enlazar `crear_estructura_ronda.sh`.
- No enlazar `plantilla_checklist_ronda.md`.

Criterio de cierre:

- El mapa contiene todos los formatos activos del checklist y no presenta auxiliares tecnicos como documentos del SGC.

## Fase 6 - Validar script y estructura

Objetivo: comprobar que la automatizacion cumple las reglas y no altera contenido existente.

Pruebas minimas:

1. Ejecutar con codigo valido:

```bash
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R1
```

2. Verificar que existe:

```text
02_despliegue_rondas/EA-TEST-2026-R1/checklist_ronda.md
```

3. Verificar que existen las siete carpetas de etapa.
4. Verificar que cada carpeta contiene `.gitkeep`.
5. Ejecutar de nuevo el mismo comando y confirmar que no sobrescribe el checklist.
6. Ejecutar desde una subcarpeta y confirmar que crea bajo la raiz del repo.
7. Ejecutar con codigo invalido, por ejemplo:

```bash
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-pp-2026-r1
```

8. Confirmar que falla con mensaje claro.

Criterio de cierre:

- La estructura generada es correcta, estable e idempotente.

## Fase 7 - Crear rondas piloto destino

Objetivo: preparar los destinos operativos para la migracion manual.

Rondas esperadas:

```text
02_despliegue_rondas/EA-PP-2026-R1/
02_despliegue_rondas/EA-PP-2026-R2/
02_despliegue_rondas/EA-PP-2026-R3/
```

Mapeo temporal:

```text
02_prueba_piloto_rondas/01_ronda_simple/
  -> 02_despliegue_rondas/EA-PP-2026-R1/

02_prueba_piloto_rondas/02_ronda_compleja_fase1/
  -> 02_despliegue_rondas/EA-PP-2026-R2/

02_prueba_piloto_rondas/03_ronda_compleja_fase2/
  -> 02_despliegue_rondas/EA-PP-2026-R3/
```

Reglas:

- Crear estructuras con el script.
- Copiar evidencias manualmente.
- No mover archivos desde la fuente historica.
- No borrar `02_prueba_piloto_rondas/`.
- Dejar `02_prueba_piloto_rondas/00_planificacion/` aparte por ahora.

Criterio de cierre:

- Las tres rondas destino existen con estructura minima y checklist.

## Fase 8 - Migracion manual controlada

Objetivo: poblar cada ronda destino con evidencias historicas copiadas desde la estructura vieja.

Estrategia:

1. Copiar primero registros claramente asociados a etapa.
2. Mantener nombres de archivo con codigo documental al inicio.
3. No anteponer el codigo de ronda a los nombres de archivos dentro de la ronda.
4. Conservar `.md`, `.xlsx`, `.csv`, `.docx` juntos si son evidencia de la misma etapa.
5. Marcar avance en `checklist_ronda.md`.
6. Registrar dudas o conflictos antes de mover contenido ambiguo.

Criterio de cierre:

- Cada ronda destino tiene evidencias copiadas y checklist actualizado.

## Riesgos y controles

| Riesgo | Impacto | Control |
|---|---:|---|
| Confundir maestro con registro diligenciado | Alto | Mantener maestros solo en `01_bloque_general/04_formatos_maestros/`. |
| Sobrescribir checklist de una ronda existente | Alto | Script crea checklist solo si falta. |
| Migrar moviendo en vez de copiando | Alto | Migracion manual por copia, sin borrado de historico. |
| Contradiccion entre checklist, P-PSEA-02 y P-PSEA-03 | Medio | Revisar ubicacion por formato, especialmente `F-PSEA-12`. |
| Mapa incompleto | Medio | Validar que todos los formatos del checklist tengan nodo o razon documentada. |
| Auxiliares tratados como documentos controlados | Medio | No asignar codigo documental ni enlazarlos desde el mapa. |

## Criterio final de exito

El reordenamiento queda implementado cuando:

- Existe `02_despliegue_rondas/`.
- El script crea rondas validas con estructura exacta.
- La plantilla genera el checklist acordado.
- `P-PSEA-02` y `P-PSEA-03` no se contradicen.
- El mapa incluye los formatos faltantes del checklist.
- Las rondas piloto destino pueden crearse sin tocar la fuente historica.
