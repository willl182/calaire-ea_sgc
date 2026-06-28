# Workflow detallado de implementacion del reordenamiento

## Vista general

El workflow ejecuta el reordenamiento en este orden:

```text
1. Preparar linea base
2. Crear plantilla de checklist
3. Crear script auxiliar
4. Probar script con ronda temporal
5. Alinear P-PSEA-03
6. Revisar P-PSEA-02
7. Actualizar mapa de navegacion
8. Crear rondas piloto destino
9. Copiar evidencias manualmente
10. Validar cierre
```

La regla de trabajo es avanzar de lo mecanico a lo documental: primero se crea la estructura repetible, luego se ajustan los documentos que la gobiernan, finalmente se migra contenido.

## Paso 1 - Preparar linea base

Objetivo: identificar el estado real antes de editar.

Comandos sugeridos:

```bash
find . -maxdepth 3 -type d | sort
find . -maxdepth 4 -type f | rg 'P-PSEA-0[23]|mapa_navegacion|crear_estructura|plantilla_checklist'
rg -n '02_despliegue_rondas|02_prueba_piloto_rondas|checklist_ronda|F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17' .
```

Decisiones en este paso:

- Si `02_despliegue_rondas/` no existe, el script debe crearlo.
- Si existen auxiliares previos, revisarlos antes de reemplazar.
- Si hay rondas ya creadas, no sobrescribir checklist ni reorganizar automaticamente.

Salida esperada:

- Lista de archivos a crear.
- Lista de archivos a editar.
- Confirmacion de que `02_prueba_piloto_rondas/` queda intacto.

## Paso 2 - Crear plantilla del checklist

Objetivo: crear la fuente unica para `checklist_ronda.md`.

Crear:

```text
01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md
```

Contenido:

```markdown
# Checklist documental de ronda

## 01_planificacion_ronda
- [ ] F-PSEA-01 - Calendario global de ronda
- [ ] F-PSEA-02 - Cronograma detallado de ronda
- [ ] F-PSEA-04 - Anexo tecnico de equipos e instrumentos
- [ ] F-PSEA-05 - Plan de ronda EA
- [ ] F-PSEA-05A - Hoja de registro del participante
- [ ] F-PSEA-06 - Ficha digital de ronda EA
- [ ] F-PSEA-16 - Matriz de competencia y autorizacion
- [ ] F-PSEA-17 - Evaluacion de proveedores criticos, si aplica

## 02_comunicaciones_participantes
- [ ] F-PSEA-18 - Formato de comunicacion oficial al participante
- [ ] Respuestas o acuses de recibo del participante
- [ ] Comunicaciones de aclaracion o cambios, si aplica

## 03_preparacion_item
- [ ] F-PSEA-07 - Preparacion y control del item
- [ ] Certificados de gases, equipos o patrones usados
- [ ] Evidencia de montaje, configuracion o verificacion tecnica

## 04_datos_y_preprocesamiento
- [ ] F-PSEA-08 - Datos reportados por participante
- [ ] F-PSEA-09 - Datos de participantes exportados para analisis PT
- [ ] F-PSEA-10 - Registro de preprocesamiento de datos
- [ ] F-PSEA-12 - Datos oficiales consolidados para evaluacion de aptitud
- [ ] Archivos CSV o exportaciones conservadas para trazabilidad

## 05_homogeneidad_estabilidad
- [ ] F-PSEA-11 - Homogeneidad y estabilidad del item
- [ ] F-PSEA-11A - Datos preprocesados de homogeneidad
- [ ] F-PSEA-11B - Datos preprocesados de estabilidad
- [ ] F-PSEA-11C - Resultados de homogeneidad
- [ ] F-PSEA-11D - Resultados de estabilidad

## 06_analisis_e_informe
- [ ] F-PSEA-13 - Informe final de resultados
- [ ] Evidencia de envio del informe final al participante
- [ ] Salidas, graficas o tablas generadas para el informe

## 07_cierre_sgc
- [ ] Evidencia de cierre de ronda
- [ ] F-PSEA-14 - Registro caso de queja o no conformidad, si aplica
- [ ] F-PSEA-15 - Registro de apelacion, si aplica
```

Validacion:

```bash
diff -u <(sed -n '/^```markdown$/,/^```$/p' decisiones_grill_sgc.md | sed '1d;$d') \
  '01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md'
```

Si el comando con sustitucion de procesos no se quiere usar, validar manualmente contra `decisiones_grill_sgc.md`.

## Paso 3 - Crear script auxiliar

Objetivo: crear rondas con estructura minima y checklist.

Crear:

```text
01_bloque_general/02_procedimientos/crear_estructura_ronda.sh
```

Logica recomendada:

1. Activar modo estricto:

```bash
set -euo pipefail
```

2. Validar cantidad de argumentos.
3. Validar codigo con regex.
4. Resolver:

```text
script_dir = carpeta donde esta el script
repo_root = dos niveles arriba de script_dir
template = script_dir/plantilla_checklist_ronda.md
round_root = repo_root/02_despliegue_rondas/<codigo>
```

5. Verificar que la plantilla existe antes de crear estructura.
6. Crear `02_despliegue_rondas/`.
7. Crear carpeta de ronda.
8. Crear siete carpetas.
9. Crear `.gitkeep` en cada carpeta si falta.
10. Crear `checklist_ronda.md` desde plantilla si falta.
11. Imprimir resumen.

Validacion:

```bash
bash -n '01_bloque_general/02_procedimientos/crear_estructura_ronda.sh'
chmod +x '01_bloque_general/02_procedimientos/crear_estructura_ronda.sh'
```

## Paso 4 - Probar script con ronda temporal

Objetivo: asegurar que el script es seguro antes de crear rondas reales.

Crear ronda temporal:

```bash
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R1
```

Validar estructura:

```bash
find '02_despliegue_rondas/EA-TEST-2026-R1' -maxdepth 2 -print | sort
```

Validar contenido esperado:

```bash
test -f '02_despliegue_rondas/EA-TEST-2026-R1/checklist_ronda.md'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/01_planificacion_ronda'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/02_comunicaciones_participantes'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/03_preparacion_item'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/04_datos_y_preprocesamiento'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/05_homogeneidad_estabilidad'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/06_analisis_e_informe'
test -d '02_despliegue_rondas/EA-TEST-2026-R1/07_cierre_sgc'
```

Validar idempotencia:

```bash
sha256sum '02_despliegue_rondas/EA-TEST-2026-R1/checklist_ronda.md'
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R1
sha256sum '02_despliegue_rondas/EA-TEST-2026-R1/checklist_ronda.md'
```

Validar codigo invalido:

```bash
! ./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-pp-2026-r1
! ./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh PP-2026-R1
! ./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-PP-R1
```

Validar ejecucion desde otra carpeta:

```bash
cd 01_bloque_general
./02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R2
cd -
```

Decision despues de prueba:

- Si las rondas temporales molestan, borrarlas solo despues de confirmar que no contienen trabajo real.
- Si se prefiere no borrar nada, dejarlas fuera de la migracion y no usarlas como evidencia.

## Paso 5 - Alinear `P-PSEA-03`

Objetivo: convertir la estructura decidida en regla documental.

Editar:

```text
01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md
```

Cambios concretos:

1. Reemplazar la estructura minima actual por:

```text
02_despliegue_rondas/
  <codigo_ronda>/
    checklist_ronda.md
    01_planificacion_ronda/
    02_comunicaciones_participantes/
    03_preparacion_item/
    04_datos_y_preprocesamiento/
    05_homogeneidad_estabilidad/
    06_analisis_e_informe/
    07_cierre_sgc/
```

2. Agregar regla de raiz limpia:

```text
La raiz de la ronda solo contiene checklist_ronda.md y las siete carpetas de etapa.
```

3. Agregar regla de auxiliares:

```text
La estructura puede generarse con crear_estructura_ronda.sh <codigo_ronda>, usando plantilla_checklist_ronda.md. Estos archivos son auxiliares operativos asociados a este procedimiento y no documentos controlados.
```

4. Revisar la matriz de registros para que las ubicaciones por etapa coincidan con el checklist.
5. Resolver la tension de `F-PSEA-12`:
   - si se respeta el checklist, ubicarlo en `04_datos_y_preprocesamiento`;
   - si se decide que debe quedar en `06_analisis_e_informe`, actualizar checklist, plantilla, targets y decisiones.

Validacion:

```bash
rg -n 'checklist_ronda|crear_estructura_ronda|plantilla_checklist|02_despliegue_rondas|F-PSEA-12' \
  '01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md'
```

## Paso 6 - Revisar `P-PSEA-02`

Objetivo: asegurar que la matriz maestra no contradice el procedimiento operativo.

Editar solo si hace falta:

```text
01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md
```

Revisar:

- La tabla de arquitectura documental.
- Las entradas de `F-PSEA-05A`, `F-PSEA-12`, `F-PSEA-14`, `F-PSEA-15`, `F-PSEA-16`, `F-PSEA-17`.
- Las reglas de mantenimiento.
- Las relaciones con `P-PSEA-03`.

Decision critica:

- `P-PSEA-02` puede indicar ubicacion maestra del formato.
- `P-PSEA-03` gobierna donde queda la copia diligenciada o evidencia por ronda.
- No mezclar esas dos funciones en una misma frase ambigua.

Validacion:

```bash
rg -n 'F-PSEA-05A|F-PSEA-12|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17|02_despliegue_rondas' \
  '01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md'
```

## Paso 7 - Actualizar mapa de navegacion

Objetivo: reflejar el checklist completo en el mapa visual.

Editar:

```text
mapa_navegacion_sgc_pea.html
```

Agregar nodos en `const nodes`:

```javascript
{ id: "F-PSEA-05A", label: "Hoja registro participante", family: "F", state: "Elaborado", ... }
{ id: "F-PSEA-14", label: "Queja o no conformidad", family: "F", state: "Elaborado", ... }
{ id: "F-PSEA-15", label: "Apelaciones", family: "F", state: "Elaborado", ... }
{ id: "F-PSEA-16", label: "Competencia autorizacion", family: "F", state: "Elaborado", ... }
{ id: "F-PSEA-17", label: "Proveedores criticos", family: "F", state: "Elaborado", ... }
```

Agregar relaciones en `const edges`:

```javascript
["P-PSEA-04", "F-PSEA-05A"]
["F-PSEA-05", "F-PSEA-05A"]
["P-PSEA-15", "F-PSEA-14"]
["P-PSEA-17", "F-PSEA-14"]
["P-PSEA-18", "F-PSEA-15"]
["P-PSEA-20", "F-PSEA-16"]
["P-PSEA-21", "F-PSEA-17"]
```

Actualizar rutas:

- `planning`: incluir `F-PSEA-05A`, `F-PSEA-16`, `F-PSEA-17` si se quiere mostrar planificacion completa.
- `round`: incluir todos los formatos del checklist.
- Considerar una ruta de gestion SGC para `F-PSEA-14` y `F-PSEA-15`.

Validacion:

```bash
rg -n 'F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17' mapa_navegacion_sgc_pea.html
! rg -n 'crear_estructura_ronda|plantilla_checklist_ronda' mapa_navegacion_sgc_pea.html
```

Validacion visual:

- Abrir `mapa_navegacion_sgc_pea.html` en navegador.
- Confirmar que los nodos nuevos aparecen.
- Confirmar que los filtros/rutas no rompen el render.
- Confirmar que cada nodo abre detalle y enlace de ficha si existe.

## Paso 8 - Crear rondas piloto destino

Objetivo: preparar destino limpio para copiar evidencias.

Ejecutar:

```bash
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-PP-2026-R1
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-PP-2026-R2
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-PP-2026-R3
```

Verificar:

```bash
find 02_despliegue_rondas -maxdepth 2 -type d | sort
```

Regla:

- Este paso solo crea estructura.
- No copia formatos maestros.
- No migra evidencias automaticamente.

## Paso 9 - Copiar evidencias manualmente

Objetivo: poblar cada ronda destino sin destruir la fuente historica.

Mapeo:

```text
02_prueba_piloto_rondas/01_ronda_simple/
  -> 02_despliegue_rondas/EA-PP-2026-R1/

02_prueba_piloto_rondas/02_ronda_compleja_fase1/
  -> 02_despliegue_rondas/EA-PP-2026-R2/

02_prueba_piloto_rondas/03_ronda_compleja_fase2/
  -> 02_despliegue_rondas/EA-PP-2026-R3/
```

Clasificacion por destino:

```text
01_planificacion_ronda/
  F-PSEA-01, F-PSEA-02, F-PSEA-04, F-PSEA-05, F-PSEA-05A, F-PSEA-06, F-PSEA-16, F-PSEA-17

02_comunicaciones_participantes/
  F-PSEA-18, correos, acuses, respuestas, aclaraciones

03_preparacion_item/
  F-PSEA-07, certificados, montaje, configuracion, verificacion tecnica

04_datos_y_preprocesamiento/
  F-PSEA-08, F-PSEA-09, F-PSEA-10, F-PSEA-12, CSV y exportaciones trazables

05_homogeneidad_estabilidad/
  F-PSEA-11, F-PSEA-11A, F-PSEA-11B, F-PSEA-11C, F-PSEA-11D

06_analisis_e_informe/
  F-PSEA-13, evidencia de envio, salidas, graficas, tablas

07_cierre_sgc/
  evidencia de cierre, F-PSEA-14, F-PSEA-15
```

Reglas de copia:

- Copiar, no mover.
- Mantener nombre de archivo con codigo documental al inicio.
- No anteponer codigo de ronda al archivo.
- Si un archivo sirve a dos etapas, ubicarlo donde se usa principalmente.
- Si hay duda, dejarlo sin copiar hasta decidir.
- Despues de copiar, marcar el item correspondiente en `checklist_ronda.md`.

## Paso 10 - Validacion final

Objetivo: confirmar que estructura, documentos y mapa quedaron coherentes.

Validaciones de archivos:

```bash
test -f plan_reorden.md
test -f workflow_reorden.md
test -f targets_reorden.md
test -f '01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md'
test -x '01_bloque_general/02_procedimientos/crear_estructura_ronda.sh'
```

Validacion de estructura:

```bash
find 02_despliegue_rondas -maxdepth 3 -print | sort
```

Validacion documental:

```bash
rg -n '02_despliegue_rondas|checklist_ronda|crear_estructura_ronda|plantilla_checklist' \
  '01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md' \
  '01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md'
```

Validacion del mapa:

```bash
rg -n 'F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17' mapa_navegacion_sgc_pea.html
```

Validacion negativa:

```bash
! rg -n 'crear_estructura_ronda|plantilla_checklist_ronda' mapa_navegacion_sgc_pea.html
```

## Puntos de decision durante la ejecucion

### Decision 1 - Ubicacion de `F-PSEA-12`

Situacion:

- El checklist del grill ubica `F-PSEA-12` en `04_datos_y_preprocesamiento`.
- Algunas referencias actuales lo asocian a `06_analisis_e_informe`.

Resolucion recomendada:

- Mantener `F-PSEA-12` en `04_datos_y_preprocesamiento`, porque es dato oficial consolidado previo al analisis y soporta trazabilidad de datos.
- Dejar `F-PSEA-13`, graficas, tablas y salidas del informe en `06_analisis_e_informe`.

### Decision 2 - Tratamiento de rondas temporales

Situacion:

- Las pruebas pueden crear `EA-TEST-2026-R1` y `EA-TEST-2026-R2`.

Resolucion recomendada:

- Usarlas solo para validacion.
- Borrarlas despues si no contienen trabajo real, o dejarlas claramente fuera de migracion.

### Decision 3 - Migracion de `00_planificacion`

Situacion:

- `02_prueba_piloto_rondas/00_planificacion/` contiene material transversal historico.

Resolucion recomendada:

- No migrarlo en bloque.
- Revisar archivo por archivo y copiar solo lo que corresponda a una ronda o a un maestro.

## Orden de ejecucion recomendado

1. Crear `plantilla_checklist_ronda.md`.
2. Crear `crear_estructura_ronda.sh`.
3. Probar script con `EA-TEST-2026-R1`.
4. Ajustar `P-PSEA-03`.
5. Ajustar `P-PSEA-02` solo donde contradiga a `P-PSEA-03`.
6. Actualizar `mapa_navegacion_sgc_pea.html`.
7. Crear `EA-PP-2026-R1`, `EA-PP-2026-R2`, `EA-PP-2026-R3`.
8. Copiar evidencias manualmente.
9. Validar targets.

## Resultado esperado

Al finalizar, el SGC queda con una frontera clara:

- El bloque general conserva documentos maestros y control documental.
- El despliegue de rondas conserva evidencias y registros por ejecucion.
- Cada ronda nueva se puede crear de forma repetible.
- La migracion historica puede hacerse sin perder trazabilidad ni alterar la fuente vieja.
