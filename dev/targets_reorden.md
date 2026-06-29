# Targets esperados del reordenamiento SGC CALAIRE-EA

## Target 1 - Auxiliares de ronda

Estado esperado:

- Existe `01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md`.
- Existe `01_bloque_general/02_procedimientos/crear_estructura_ronda.sh`.
- El script tiene permiso de ejecucion.
- Ninguno de los dos archivos tiene codigo documental `P-PSEA`, `I-PSEA` o `F-PSEA`.

Validacion:

```bash
test -f '01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md'
test -f '01_bloque_general/02_procedimientos/crear_estructura_ronda.sh'
test -x '01_bloque_general/02_procedimientos/crear_estructura_ronda.sh'
```

## Target 2 - Checklist maestro de ronda

Estado esperado:

- La plantilla contiene solo el checklist acordado.
- No contiene metadatos de ronda.
- No contiene rutas.
- No contiene estados distintos a checkboxes.
- No lista procedimientos ni instructivos.
- Incluye todos los formatos del checklist:

```text
F-PSEA-01
F-PSEA-02
F-PSEA-04
F-PSEA-05
F-PSEA-05A
F-PSEA-06
F-PSEA-07
F-PSEA-08
F-PSEA-09
F-PSEA-10
F-PSEA-11
F-PSEA-11A
F-PSEA-11B
F-PSEA-11C
F-PSEA-11D
F-PSEA-12
F-PSEA-13
F-PSEA-14
F-PSEA-15
F-PSEA-16
F-PSEA-17
F-PSEA-18
```

Validacion:

```bash
rg 'F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17|F-PSEA-18' \
  '01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md'
```

## Target 3 - Script idempotente

Estado esperado:

- El script recibe exactamente un codigo de ronda.
- Acepta codigos como `EA-PP-2026-R1`.
- Rechaza codigos como `EA-pp-2026-r1`, `PP-2026-R1` o `EA-PP-R1`.
- Crea `02_despliegue_rondas/` si falta.
- Crea una sola ronda por ejecucion.
- No sobrescribe `checklist_ronda.md`.
- No borra ni mueve nada.
- No copia formatos maestros.

Validacion:

```bash
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R1
./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-TEST-2026-R1
! ./01_bloque_general/02_procedimientos/crear_estructura_ronda.sh EA-pp-2026-r1
```

## Target 4 - Estructura exacta de ronda

Estado esperado:

Cada ronda creada por el script tiene esta forma:

```text
02_despliegue_rondas/<codigo_ronda>/
  checklist_ronda.md
  01_planificacion_ronda/
  02_comunicaciones_participantes/
  03_preparacion_item/
  04_datos_y_preprocesamiento/
  05_homogeneidad_estabilidad/
  06_analisis_e_informe/
  07_cierre_sgc/
```

Cada carpeta de etapa contiene `.gitkeep`.

La raiz de la ronda no contiene README ni formatos copiados automaticamente.

Validacion:

```bash
find '02_despliegue_rondas/EA-TEST-2026-R1' -maxdepth 2 -print | sort
```

## Target 5 - `P-PSEA-03` alineado

Estado esperado:

- Describe `02_despliegue_rondas/<codigo_ronda>/`.
- Incluye `checklist_ronda.md` en la raiz.
- Declara que la raiz de la ronda solo contiene el checklist y siete carpetas.
- Menciona `crear_estructura_ronda.sh` y `plantilla_checklist_ronda.md` como auxiliares operativos.
- No trata los auxiliares como documentos controlados.
- Ubica `F-PSEA-12` de forma consistente con el checklist.

Validacion:

```bash
rg -n 'checklist_ronda|crear_estructura_ronda|plantilla_checklist|02_despliegue_rondas|F-PSEA-12' \
  '01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md'
```

## Target 6 - `P-PSEA-02` consistente

Estado esperado:

- Mantiene `01_bloque_general/` como SGC maestro.
- Mantiene `02_despliegue_rondas/` como espacio de registros/evidencias por ronda.
- Declara que la prueba piloto es una ronda, no un bloque documental independiente.
- No registra instancias diligenciadas por ronda como documentos maestros.
- No contradice `P-PSEA-03`.

Validacion:

```bash
rg -n '01_bloque_general|02_despliegue_rondas|prueba piloto|ronda|P-PSEA-03' \
  '01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md'
```

## Target 7 - Mapa de navegacion completo

Estado esperado:

`mapa_navegacion_sgc_pea.html` contiene nodos para:

```text
F-PSEA-05A
F-PSEA-14
F-PSEA-15
F-PSEA-16
F-PSEA-17
```

Tambien conserva los nodos ya esperados del flujo:

```text
F-PSEA-01
F-PSEA-02
F-PSEA-04
F-PSEA-05
F-PSEA-06
F-PSEA-07
F-PSEA-08
F-PSEA-09
F-PSEA-10
F-PSEA-11
F-PSEA-11A
F-PSEA-11B
F-PSEA-11C
F-PSEA-11D
F-PSEA-12
F-PSEA-13
F-PSEA-18
```

El mapa no enlaza:

```text
crear_estructura_ronda.sh
plantilla_checklist_ronda.md
```

Validacion:

```bash
rg -n 'F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17' mapa_navegacion_sgc_pea.html
! rg -n 'crear_estructura_ronda|plantilla_checklist_ronda' mapa_navegacion_sgc_pea.html
```

## Target 8 - Rondas piloto destino

Estado esperado:

Existen las estructuras destino:

```text
02_despliegue_rondas/EA-PP-2026-R1/
02_despliegue_rondas/EA-PP-2026-R2/
02_despliegue_rondas/EA-PP-2026-R3/
```

Cada una tiene `checklist_ronda.md` y las siete carpetas.

Validacion:

```bash
find 02_despliegue_rondas -maxdepth 2 -type d | sort
```

## Target 9 - Migracion historica preservada

Estado esperado:

- `02_prueba_piloto_rondas/` sigue existiendo.
- No se borran ni se mueven los archivos historicos.
- La migracion se hace copiando hacia `02_despliegue_rondas/`.
- `02_prueba_piloto_rondas/00_planificacion/` queda aparte por ahora.

Validacion:

```bash
test -d '02_prueba_piloto_rondas'
test -d '02_prueba_piloto_rondas/00_planificacion'
```

## Target 10 - Criterio final integrado

Estado esperado:

El reordenamiento se considera cerrado cuando:

- Los auxiliares existen y funcionan.
- El checklist se genera igual para cada ronda.
- La estructura de ronda es estable e idempotente.
- `P-PSEA-02` y `P-PSEA-03` estan alineados.
- El mapa contiene todos los formatos activos del checklist.
- Las rondas piloto destino pueden crearse sin alterar la fuente historica.

Validacion final sugerida:

```bash
rg -n '02_despliegue_rondas|checklist_ronda|F-PSEA-05A|F-PSEA-14|F-PSEA-15|F-PSEA-16|F-PSEA-17' \
  decisiones_grill_sgc.md \
  '01_bloque_general/02_procedimientos/P-PSEA-02 Matriz documental basica del PEA.md' \
  '01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md' \
  mapa_navegacion_sgc_pea.html
```
