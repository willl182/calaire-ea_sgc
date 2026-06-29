# Ficha Resumen: F-PSEA-03

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `F-PSEA-03` |
| **Nombre decidido** | Registro de participacion y carga de datos del participante |
| **Tipo documental** | Registro |
| **Estado** | Mantener / Actualizar |
| **Prioridad** | Media |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Registro principal donde el participante carga o actualiza en `calaire-app` sus datos de participacion: contacto, personal autorizado, analitos, equipos, condiciones logisticas y aceptacion de condiciones. Es la fuente primaria para el seguimiento de participacion y para exportar equipos como `F-PSEA-04`.

### Rol en el flujo

- [x] Registro oficial
- [x] Evidencia
- [ ] Entrada
- [ ] Salida
- [ ] Criterio tecnico
- [ ] Instructivo
- [ ] Matriz
- [ ] Soporte documental

---

## Aplicativos y tecnologia

#### Aplicativo asociado

- [x] `calaire-app`
- [ ] `pt_app`
- [ ] Ambos
- [ ] Ninguno

Registro generado y mantenido en `calaire-app`.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| `calaire-app` | Inscripcion y confirmacion de laboratorios | Origen |
| `P-PSEA-04` | Planificacion de ronda | Referencia |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| `F-PSEA-04` | Equipos e instrumentos exportados desde el registro | Salida |
| `F-PSEA-06` | Planificacion completa de ronda | Insumo |
| `F-PSEA-09` | Datos exportados para analisis | Referencia |
| `P-PSEA-05` | Comunicaciones a participantes | Referencia |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-04` | Planificacion que define participantes | Obligatorio |
| `F-PSEA-04` | Anexo tecnico de equipos por participante | Obligatorio |
| `F-PSEA-06` | Planificacion completa alimentada por la carga del participante | Obligatorio |
| `DG-PSEA-02` | Aplicativo que gestiona la participacion | Obligatorio |
| `I-PSEA-02` | Instructivo para participante | Referencia |

---

## Limites y riesgos

#### Limites de alcance

- No es el anexo tecnico de equipos exportado (eso es `F-PSEA-04`).
- No es la ficha basica de ronda (eso es `F-PSEA-05`).
- No es la planificacion completa de ronda (eso es `F-PSEA-06`).
- No contiene datos reportados (eso es `F-PSEA-08`).
- No es el informe final (eso es `F-PSEA-13`).
- No es un instructivo de uso.

#### Riesgos de interpretacion

- **Confundir con F-PSEA-04:** `F-PSEA-03` es el registro de participacion; `F-PSEA-04` es el anexo tecnico de equipos.
- **Omitir trazabilidad:** Debe vincularse con la exportacion de equipos (`F-PSEA-04`) y la planificacion completa (`F-PSEA-06`).
- **Incluir resultados de aptitud:** Los resultados de aptitud se reportan en el informe (`F-PSEA-13`), no en el registro de participacion.

---

## Criterio minimo de elaboracion

El registro de participacion contiene la carga de datos del participante en `calaire-app`, permite cerrar su estado de participacion y exporta equipos hacia `F-PSEA-04` para alimentar la planificacion `F-PSEA-06`.
