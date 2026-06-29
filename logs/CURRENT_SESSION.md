# Session State: CALAIRE-EA SGC

**Last Updated**: 2026-06-29 08:53 America/Bogota

## Session Objective

Alinear los formatos F-PSEA-03 a F-PSEA-06 segun la decision del usuario: F-PSEA-03 es la carga de datos del participante en calaire-app, F-PSEA-04 es equipos exportados desde F-PSEA-03, F-PSEA-05 es ficha basica de ronda, F-PSEA-06 es planificacion completa y F-PSEA-05A desaparece de activos.

## Current State

- [x] Creado `F-PSEA-03 Registro de participacion` como formato maestro MD/DOCX.
- [x] Renombrado y reescrito `F-PSEA-05` como `Ficha basica de ronda EA`.
- [x] Renombrado y reescrito `F-PSEA-06` como `Planificacion de ronda EA`.
- [x] Retirado `F-PSEA-05A` de formatos maestros, mapa, inventarios, checklist y fichas activas.
- [x] Actualizados mapa, inventario documental, diccionario, arbol maestro, matriz documental, control de registros, instructivos I-PSEA-02/I-PSEA-03 y documentos marco DG-PSEA-02/DG-PSEA-03.
- [x] Renombrados archivos de planificacion en rondas EA-PP-2026-R1/R2/R3 para F-PSEA-05 y F-PSEA-06.
- [x] Regenerados HTML de fichas y DOCX/HTML derivados principales con Pandoc.

## Critical Technical Context

- `F-PSEA-05A` solo debe aparecer en `fichas_resumen/retirados/`, `para_quitar/` o menciones explicitas de retiro/exclusion.
- Flujo documental vigente: `F-PSEA-03 -> F-PSEA-04 -> F-PSEA-06 -> F-PSEA-05`.
- El mapa fue validado con Node: 56 nodos y 50 IDs referenciados sin nodos faltantes.
- Hay cambios previos del usuario en el arbol de trabajo, especialmente reubicacion de DG-PSEA-02/DG-PSEA-03 a carpetas propias y movimiento de material antiguo a `para_quitar/`; no revertirlos.

## Next Steps

1. Revisar visualmente `mapa_navegacion_sgc_pea.html` si se desea validar layout.
2. Si se prepara commit, agrupar estos cambios como ajuste documental F-PSEA-03/04/05/06 y retiro de F-PSEA-05A.
