# Handoff - grill SGC CALAIRE-EA

## Objetivo de la sesion

Se uso el skill `grill-me` para definir la estructura organizada del SGC CALAIRE-EA, separando documentos maestros del despliegue operativo por ronda. El usuario pidio guardar la sesion y una sintesis de decisiones, y usar el skill `handoff`.

## Artefactos creados en el workspace

- `grill_sgc.md`: registro amplio de la sesion de grill, con preguntas/decisiones principales.
- `decisiones_grill_sgc.md`: sintesis ejecutiva de decisiones implementables.

No se editaron documentos controlados del SGC ni se creo aun el script auxiliar real.

## Decisiones clave

- Nueva estructura conceptual:
  - SGC maestro: documentos controlados, procedimientos, instructivos, formatos maestros, matrices, fichas y mapa.
  - Despliegue de rondas: registros y evidencias por ronda.
- La prueba piloto es una ronda, no un bloque documental independiente.
- Nueva carpeta para rondas: `02_despliegue_rondas/`.
- Estructura de cada ronda:

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

- La raiz de la ronda solo debe tener `checklist_ronda.md` y las siete carpetas.
- No README general ni README por ronda.
- Checklist simple, sin metadatos, rutas ni estados.
- Checklist general, no parametrizado por tipo de ronda.
- Registros `F-PSEA-*` y evidencias complementarias genericas van en el checklist.
- Procedimientos e instructivos no van en el checklist.

## Checklist acordado

Ver contenido exacto en `decisiones_grill_sgc.md`.

Puntos clave:

- Planificacion: `F-PSEA-01`, `02`, `04`, `05`, `05A`, `06`, `16`, `17`.
- Comunicaciones: `F-PSEA-18` y soportes de respuesta/acuses.
- Preparacion item: `F-PSEA-07` y soportes.
- Datos/preprocesamiento: `F-PSEA-08`, `09`, `10`, `12` y CSV/exportaciones.
- H/E: `F-PSEA-11`, `11A`, `11B`, `11C`, `11D`.
- Analisis/informe: `F-PSEA-13`, envio del informe y salidas/graficas/tablas.
- Cierre: evidencia de cierre, `F-PSEA-14`, `F-PSEA-15`.

## Script auxiliar definido pero no creado

Debe crearse mas adelante, solo cuando el usuario autorice edicion:

```text
01_bloque_general/02_procedimientos/
  crear_estructura_ronda.sh
  plantilla_checklist_ronda.md
```

Reglas del script:

- Bash.
- Una sola ronda por ejecucion.
- Valida `^EA-[A-Z0-9]+-[0-9]{4}-R[0-9]+$`.
- Crea bajo `02_despliegue_rondas/`.
- Crea `02_despliegue_rondas/` si falta.
- Funciona desde cualquier carpeta.
- Crea siete carpetas y `.gitkeep`.
- Crea `checklist_ronda.md` desde plantilla solo si falta.
- No borra ni sobrescribe nada.
- No copia formatos maestros.
- Imprime resumen simple.

## Mapa de navegacion

Se reviso `mapa_navegacion_sgc_pea.html`. Faltaban estos formatos frente al checklist:

- `F-PSEA-05A`
- `F-PSEA-14`
- `F-PSEA-15`
- `F-PSEA-16`
- `F-PSEA-17`

El usuario dijo que los agregara.

## Migracion

- `02_prueba_piloto_rondas/` queda temporalmente como historico/fuente de migracion.
- Migracion manual controlada por el usuario.
- Copiar, no mover.
- Mapeo temporal:

```text
02_prueba_piloto_rondas/01_ronda_simple/ -> 02_despliegue_rondas/EA-PP-2026-R1/
02_prueba_piloto_rondas/02_ronda_compleja_fase1/ -> 02_despliegue_rondas/EA-PP-2026-R2/
02_prueba_piloto_rondas/03_ronda_compleja_fase2/ -> 02_despliegue_rondas/EA-PP-2026-R3/
```

- `02_prueba_piloto_rondas/00_planificacion/` queda aparte por ahora.

## Siguiente trabajo recomendado

Cuando el usuario autorice editar:

1. Crear `plantilla_checklist_ronda.md` con el checklist exacto de `decisiones_grill_sgc.md`.
2. Crear `crear_estructura_ronda.sh` junto a `P-PSEA-03`.
3. Probar el script con una ronda temporal o real.
4. No modificar `P-PSEA-02`, `P-PSEA-03` ni el mapa salvo que el usuario lo pida explicitamente.

## Suggested skills

- `grill-me`: si se reabre decision de estructura o flujo documental.
- `handoff`: si se necesita transferir contexto a otra sesion.
- `diagnose`: si el script se implementa y falla.

