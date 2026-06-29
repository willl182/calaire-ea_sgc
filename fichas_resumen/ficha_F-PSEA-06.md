# Ficha Resumen: F-PSEA-06

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `F-PSEA-06` |
| **Nombre decidido** | Planificacion de ronda EA |
| **Tipo documental** | Formato |
| **Estado** | Mantener / Actualizar |
| **Prioridad** | Alta |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Formato completo de planificacion de una ronda de ensayo de aptitud. Consolida alcance tecnico, participantes, equipos exportados desde `F-PSEA-03` como `F-PSEA-04`, recursos, cronograma, responsabilidades, criterios estadisticos pre-ronda, matriz A-U y aprobaciones.

### Rol en el flujo

- [x] Registro oficial
- [x] Evidencia
- [x] Salida
- [ ] Entrada
- [ ] Criterio tecnico
- [ ] Instructivo
- [ ] Matriz
- [ ] Soporte documental

Es el registro completo aprobado antes de ejecutar la ronda.

---

## Aplicativos y tecnologia

#### Aplicativo asociado

- [x] `calaire-app`
- [ ] `pt_app`
- [ ] Ambos
- [ ] Ninguno

Se alimenta con informacion de `calaire-app` y puede conservarse como exportacion o documento controlado de planificacion.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| `F-PSEA-03` | Datos cargados por participantes | Insumo |
| `F-PSEA-04` | Equipos exportados desde el registro | Insumo |
| `F-PSEA-01` | Calendario global | Insumo |
| `F-PSEA-02` | Cronograma detallado | Insumo |
| `P-PSEA-04` | Procedimiento de planificacion | Referencia |
| `F-PSEA-07` | Preparacion y control del item | Referencia |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| `F-PSEA-05` | Ficha basica de ronda | Resumen |
| `F-PSEA-08` / `F-PSEA-09` | Ejecucion y datos oficiales posteriores | Referencia operativa |
| Participantes | Instrucciones y condiciones de ronda | Comunicacion |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-04` | Procedimiento que gobierna la planificacion | Obligatorio |
| `F-PSEA-03` | Registro de participacion y carga de datos | Obligatorio |
| `F-PSEA-04` | Equipos e instrumentos exportados | Obligatorio |
| `F-PSEA-05` | Ficha basica derivada/resumida | Obligatorio |
| `F-PSEA-07` | Preparacion del item referenciada | Obligatorio |
| `P-PSEA-14` | Medidas preventivas frente a colusion y falsificacion | Referencia |
| `DG-PSEA-02` | Aplicativo que alimenta la planificacion | Obligatorio |

---

## Limites y riesgos

#### Limites de alcance

- No es la ficha basica de ronda (eso es `F-PSEA-05`).
- No es el registro que diligencia el participante (eso es `F-PSEA-03`).
- No es el anexo tecnico de equipos exportado (eso es `F-PSEA-04`).
- No contiene resultados de aptitud (eso es `F-PSEA-13`).

#### Riesgos de interpretacion

- **Confundir con F-PSEA-05:** `F-PSEA-06` contiene la planificacion completa; `F-PSEA-05` solo resume la ronda.
- **Omitir A-U:** Debe incluir o referenciar los puntos A-U de ISO/IEC 17043:2023 7.2.1.3.
- **Planificar sin carga cerrada:** Debe usar `F-PSEA-03` cerrado y `F-PSEA-04` exportado antes de aprobar ejecucion.
- **Incluir analisis posterior:** Los datos estadisticos oficiales y resultados de aptitud van en `F-PSEA-12` y `F-PSEA-13`.

---

## Criterio minimo de elaboracion

La planificacion incluye alcance tecnico, participantes, equipos, recursos criticos, cronograma, matriz A-U, criterios estadisticos pre-ronda y aprobaciones, usando `F-PSEA-03` y `F-PSEA-04` como insumos formales.
