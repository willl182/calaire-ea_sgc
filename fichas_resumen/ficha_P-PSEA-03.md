# Ficha Resumen: P-PSEA-03

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `P-PSEA-03` |
| **Nombre decidido** | Control de registros y evidencias del PEA |
| **Tipo documental** | Procedimiento con matrices anexas |
| **Estado** | Elaborado |
| **Prioridad** | Alta |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Establece como se identifican, clasifican, ubican y cierran los registros y evidencias generadas por cada ronda o evento del PEA. Define la estructura operativa de `02_despliegue_rondas/<codigo_ronda>/`, con `checklist_ronda.md` como unico archivo en la raiz y siete carpetas de etapa. Es la contraparte operativa de `P-PSEA-02` (matriz documental).

### Rol en el flujo

- [x] Criterio tecnico
- [ ] Matriz
- [x] Evidencia
- [ ] Entrada
- [ ] Salida
- [ ] Registro oficial
- [ ] Instructivo
- [ ] Soporte documental

Funciona como procedimiento de control operativo de registros/evidencias y como punto de trazabilidad para el checklist de ronda y las evidencias por etapa.

---

## Aplicativos y tecnologia

#### Aplicativo asociado

- [x] `calaire-app`
- [x] `pt_app`
- [ ] Ambos
- [ ] Ninguno

Recibe registros desde ambos aplicativos; el procedimiento define como se controlan, en que etapa se conservan y como se verifica el cierre documental de la ronda.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| Ronda o evento PEA | Ejecucion de una ronda piloto o EA | Insumo |
| `F-PSEA-01` a `F-PSEA-18` | Formatos, registros y evidencias generados durante la ronda, segun aplique | Referencia |
| `P-PSEA-06` | Preparacion y control del item | Referencia |
| `P-PSEA-08` | Flujo tecnico de datos y anexos CSV | Referencia |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| `02_despliegue_rondas/<codigo_ronda>/` | Estructura operativa de la ronda | Salida de control |
| `checklist_ronda.md` | Checklist documental en la raiz de la ronda | Salida de control |
| `P-PSEA-02` | Referencia cruzada con matriz documental | Referencia |
| `F-PSEA-13` | Informe que consolida evidencias | Salida |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-02` | Diferencia de alcance / Referencia | Obligatorio |
| `P-PSEA-08` | Flujo de datos y anexos CSV, de los cuales algunos alimentan registros/evidencias | Obligatorio |
| `F-PSEA-11` | Registro de H/E como evidencia | Obligatorio |
| `F-PSEA-10` | Registro de preprocesamiento como evidencia | Obligatorio |
| `F-PSEA-12` | Dataset oficial conservado en `04_datos_y_preprocesamiento` | Obligatorio |
| `F-PSEA-14` a `F-PSEA-17` | Evidencias de cierre SGC, competencia y proveedores cuando apliquen | Condicional |

---

## Limites y riesgos

#### Limites de alcance

- No lista procedimientos, instructivos ni aplicativos como catalogo documental (eso es `P-PSEA-02`).
- No describe el flujo tecnico interno de los CSV ni del preprocesador (eso va en `P-PSEA-08`).
- No reemplaza el control documental institucional ni la gestion macro de versiones.
- No define criterios estadisticos ni reglas de decision.

#### Riesgos de interpretacion

- **Confundir con P-PSEA-02:** `P-PSEA-03` es evidencia por ronda; `P-PSEA-02` es catalogo de documentos.
- **Promover archivos tecnicos a F-PSEA:** Los archivos tecnicos internos del preprocesador se describen como anexos de flujo en `P-PSEA-08`; `P-PSEA-03` solo los trackea cuando quedan como registros o evidencias conservadas.
- **Incluir aplicativos como evidencia:** Los aplicativos (`DG-PSEA-02`, `DG-PSEA-03`) no son registros de ronda.
- **Convertir auxiliares en documentos controlados:** `crear_estructura_ronda.sh` y `plantilla_checklist_ronda.md` son auxiliares operativos asociados al procedimiento; no reciben codigo documental ni se enlazan como nodos del mapa.
- **Ensuciar la raiz de ronda:** La raiz solo contiene `checklist_ronda.md` y las siete carpetas de etapa.

---

## Criterio minimo de elaboracion

El procedimiento define como se controlan los registros y evidencias del PEA, fija la estructura `02_despliegue_rondas/<codigo_ronda>/`, ubica `F-PSEA-12` en `04_datos_y_preprocesamiento`, conserva `F-PSEA-13` en `06_analisis_e_informe` y usa `07_cierre_sgc` para cierre, quejas/NC y apelaciones cuando apliquen, sin duplicar el flujo tecnico descrito en `P-PSEA-08` ni el catalogo documental de `P-PSEA-02`.

## Evidencia de elaboracion

| Campo | Valor |
|---|---|
| **Archivo maestro** | `01_bloque_general/02_procedimientos/P-PSEA-03 Control de registros y evidencias del PEA.md` |
| **Resultado** | Se materializa el procedimiento de control de registros y evidencias con estructura de ronda, checklist documental, ubicaciones por etapa y controles especificos para datos, H/E, informe y cierre SGC. |
