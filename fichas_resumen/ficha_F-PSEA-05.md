# Ficha Resumen: F-PSEA-05

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `F-PSEA-05` |
| **Nombre decidido** | Ficha basica de ronda EA |
| **Tipo documental** | Formato |
| **Estado** | Mantener / Actualizar |
| **Prioridad** | Media |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Ficha breve de identificacion de una ronda. Resume codigo, fechas, alcance tecnico, participantes previstos, aplicativos y registros principales asociados. Sirve como caratula documental y control rapido del expediente.

### Rol en el flujo

- [x] Registro oficial
- [x] Evidencia
- [x] Salida
- [ ] Entrada
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

Puede generarse o actualizarse desde `calaire-app` como resumen de ronda.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| `F-PSEA-06` | Planificacion completa de ronda | Insumo |
| `F-PSEA-03` | Participantes confirmados | Referencia |
| `F-PSEA-04` | Equipos exportados por participante | Referencia |
| `P-PSEA-04` | Procedimiento de planificacion | Referencia |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| Expediente de ronda | Caratula o resumen de control | Evidencia |
| Participantes / equipo interno | Identificacion basica de la ronda | Comunicacion |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-04` | Procedimiento que gobierna la planificacion | Obligatorio |
| `F-PSEA-03` | Registro de participacion cargado en la app | Referencia |
| `F-PSEA-04` | Equipos exportados desde el registro | Referencia |
| `F-PSEA-06` | Planificacion completa de ronda | Obligatorio |
| `F-PSEA-01` | Calendario global referenciado | Referencia |
| `F-PSEA-02` | Cronograma detallado referenciado | Referencia |
| `DG-PSEA-02` | Aplicativo que puede generar la ficha | Obligatorio |

---

## Limites y riesgos

#### Limites de alcance

- No es el registro que diligencia el participante (eso es `F-PSEA-03`).
- No es el anexo tecnico de equipos (eso es `F-PSEA-04`).
- No es la planificacion completa (eso es `F-PSEA-06`).
- No contiene datos reportados por participantes (eso es `F-PSEA-08`).

#### Riesgos de interpretacion

- **Confundir con F-PSEA-06:** `F-PSEA-05` es la ficha basica; `F-PSEA-06` es la planificacion completa.
- **Sobrecargar la ficha:** Debe remitir al plan completo cuando se requiera detalle tecnico, estadistico o logistico.
- **Mantener datos desactualizados:** Debe actualizarse cuando cambie el estado de ronda o sus registros principales.

---

## Criterio minimo de elaboracion

La ficha contiene identificacion de ronda, fechas clave, alcance resumido, participantes/equipos referenciados y enlace a la planificacion completa `F-PSEA-06`, sin duplicar el contenido operativo detallado.
