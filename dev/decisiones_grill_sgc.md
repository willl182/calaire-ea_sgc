# Decisiones grill SGC

## Estructura principal

- El SGC se entiende en dos capas:
  - SGC maestro: documentos controlados, procedimientos, instructivos, formatos maestros, matrices, fichas y mapa.
  - Despliegue de rondas: registros y evidencias generadas por cada ronda.
- La prueba piloto no es un bloque documental independiente; es una ronda.
- El nuevo despliegue operativo debe vivir en `02_despliegue_rondas/`.
- La carpeta vieja `02_prueba_piloto_rondas/` queda como fuente historica temporal para migracion manual.

## Estructura de cada ronda

Cada ronda tendra esta estructura:

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

Reglas:

- La raiz de la ronda solo debe contener `checklist_ronda.md` y las siete carpetas.
- No hay README por ronda ni README general en `02_despliegue_rondas/`.
- Las carpetas existen desde el inicio.
- No se usan subcarpetas por estado (`borrador`, `oficial`, `soporte`).

## Codigos de ronda

- Codigo definido para la primera ronda piloto: `EA-PP-2026-R1`.
- Patron general aceptado para script:

```regex
^EA-[A-Z0-9]+-[0-9]{4}-R[0-9]+$
```

Ejemplos validos:

- `EA-PP-2026-R1`
- `EA-GASES-2026-R2`
- `EA-PILOTO-2027-R10`

## Mapeo temporal de rondas viejas

Por ahora:

```text
02_prueba_piloto_rondas/01_ronda_simple/
  -> 02_despliegue_rondas/EA-PP-2026-R1/

02_prueba_piloto_rondas/02_ronda_compleja_fase1/
  -> 02_despliegue_rondas/EA-PP-2026-R2/

02_prueba_piloto_rondas/03_ronda_compleja_fase2/
  -> 02_despliegue_rondas/EA-PP-2026-R3/
```

- `02_prueba_piloto_rondas/00_planificacion/` queda aparte por ahora.
- La migracion sera manual.
- Se copia desde la estructura vieja; no se mueve ni se borra hasta validar.

## Checklist de ronda

- Cada ronda tiene un unico `checklist_ronda.md` en la raiz.
- Es solo un checklist, sin metadatos, sin rutas, sin estados y sin datos basicos de ronda.
- No se parametriza por tipo de ronda.
- Lista registros `F-PSEA-*` y evidencias complementarias genericas.
- No lista procedimientos ni instructivos.

Contenido acordado:

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

## Ubicacion de formatos por etapa

- `F-PSEA-01`: `01_planificacion_ronda`
- `F-PSEA-02`: `01_planificacion_ronda`
- `F-PSEA-04`: `01_planificacion_ronda`
- `F-PSEA-05`: `01_planificacion_ronda`
- `F-PSEA-05A`: `01_planificacion_ronda`
- `F-PSEA-06`: `01_planificacion_ronda`
- `F-PSEA-16`: `01_planificacion_ronda`
- `F-PSEA-17`: `01_planificacion_ronda`
- `F-PSEA-18`: `02_comunicaciones_participantes`
- `F-PSEA-07`: `03_preparacion_item`
- `F-PSEA-08`: `04_datos_y_preprocesamiento`
- `F-PSEA-09`: `04_datos_y_preprocesamiento`
- `F-PSEA-10`: `04_datos_y_preprocesamiento`
- `F-PSEA-12`: `04_datos_y_preprocesamiento`
- `F-PSEA-11`: `05_homogeneidad_estabilidad`
- `F-PSEA-11A`: `05_homogeneidad_estabilidad`
- `F-PSEA-11B`: `05_homogeneidad_estabilidad`
- `F-PSEA-11C`: `05_homogeneidad_estabilidad`
- `F-PSEA-11D`: `05_homogeneidad_estabilidad`
- `F-PSEA-13`: `06_analisis_e_informe`
- `F-PSEA-14`: `07_cierre_sgc`
- `F-PSEA-15`: `07_cierre_sgc`

## Decisiones tecnicas sobre registros

- `F-PSEA-04` es de planificacion porque documenta equipos/instrumentos del participante.
- `F-PSEA-10` no cubre H/E; cubre preprocesamiento de datos de participantes.
- H/E se controla con `F-PSEA-11` y `F-PSEA-11A-D`.
- `F-PSEA-18` es formato de comunicacion oficial al participante.
- Las respuestas, acuses y aclaraciones son evidencias complementarias.
- La evidencia de envio del informe final va en `06_analisis_e_informe`.

## Script auxiliar

Se definio un script auxiliar, aun no creado, junto a `P-PSEA-03`:

```text
01_bloque_general/02_procedimientos/
  crear_estructura_ronda.sh
  plantilla_checklist_ronda.md
```

Reglas:

- El script y la plantilla no llevan codigo documental.
- El script se asocia operativamente a `P-PSEA-03`.
- No debe estar en `scripts/`.
- Debe estar escrito en Bash.
- Crea una sola ronda por ejecucion.
- Crea siempre bajo `02_despliegue_rondas/`.
- Crea `02_despliegue_rondas/` si falta.
- Funciona desde cualquier carpeta.
- Crea las siete carpetas de etapa.
- Crea `.gitkeep` en cada carpeta.
- No elimina `.gitkeep`.
- No copia formatos maestros.
- No borra nada.
- No sobrescribe `checklist_ronda.md` existente.
- Si falta `checklist_ronda.md`, lo crea desde `plantilla_checklist_ronda.md`.
- Imprime resumen simple.

## Documentos del SGC que deben mencionar la estructura

- `P-PSEA-02` debe aclarar que los documentos maestros no son registros de ronda y que las rondas se despliegan en `02_despliegue_rondas/<codigo_ronda>/`.
- `P-PSEA-03` debe describir la estructura de ronda y mencionar los auxiliares `crear_estructura_ronda.sh` y `plantilla_checklist_ronda.md`.
- El mapa de navegacion no debe enlazar el script ni la plantilla.

## Mapa de navegacion

El mapa debe incluir todos los formatos activos del checklist.

Al revisar `mapa_navegacion_sgc_pea.html`, faltaban:

- `F-PSEA-05A`
- `F-PSEA-14`
- `F-PSEA-15`
- `F-PSEA-16`
- `F-PSEA-17`

El usuario indico que los agregara.

## Nombres de archivos dentro de ronda

- Los registros codificados conservan el codigo documental al inicio.
- No se antepone el codigo de ronda al nombre del archivo dentro de la carpeta de ronda.

Ejemplo:

```text
EA-PP-2026-R1/
  04_datos_y_preprocesamiento/
    F-PSEA-08 Datos reportados por participante.xlsx
```

- Se pueden conservar `.md`, `.xlsx`, `.csv`, `.docx` juntos si son evidencia de la ronda.
- Ningun `.md` se trata como descriptivo por defecto si esta en la ronda.

## Pendientes

- Crear `crear_estructura_ronda.sh` y `plantilla_checklist_ronda.md` cuando el usuario autorice editar.
- Incorporar referencias minimas en `P-PSEA-02` y `P-PSEA-03` si no quedaron ya ajustadas.
- Agregar nodos faltantes al mapa.
- Migrar manualmente evidencias copiando desde `02_prueba_piloto_rondas/` a `02_despliegue_rondas/`.

