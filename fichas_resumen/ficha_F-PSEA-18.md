# Ficha Resumen: F-PSEA-18

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `F-PSEA-18` |
| **Nombre decidido** | Comunicacion participantes |
| **Tipo documental** | Formato / Registro |
| **Estado** | Implementado |
| **Prioridad** | Media |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Formato para estandarizar y registrar comunicaciones formales enviadas a participantes del PEA. Sirve como plantilla reusable para mensajes de invitacion, confirmacion, actualizacion de fechas, solicitud de formularios, envio de cronogramas, instrucciones operativas y seguimiento de acciones pendientes.

### Rol en el flujo

- [x] Registro oficial
- [x] Evidencia
- [x] Entrada
- [x] Salida
- [ ] Criterio tecnico
- [ ] Instructivo
- [ ] Matriz
- [x] Soporte documental

---

## Aplicativos y tecnologia

#### Aplicativo asociado

- [x] `calaire-app`
- [ ] `pt_app`
- [ ] Ambos
- [x] Ninguno

Puede usarse para comunicaciones registradas en `calaire-app` o por correo institucional, segun el canal autorizado por `P-PSEA-05`. Cuando se emite por correo, la evidencia debe conservar asunto, destinatarios, fecha, adjuntos y respuesta.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| `P-PSEA-05` | Procedimiento que gobierna canales, responsables y trazabilidad de comunicaciones. | Regla |
| `F-PSEA-05` | Plan de ronda con participantes, alcance, fechas y condiciones vigentes. | Insumo |
| `F-PSEA-01` | Calendario de ronda o prueba piloto. | Insumo |
| `F-PSEA-02` | Cronograma detallado de actividades. | Insumo |
| `F-PSEA-03` | Registro de participacion, cuando se solicita diligenciamiento o actualizacion en `calaire-app`. | Salida esperada |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| Evidencia de envio | Correo, registro de aplicativo, acta o documento emitido. | Evidencia |
| Respuesta del participante | Acuse, datos enviados o formato diligenciado. | Evidencia |
| `F-PSEA-03` | Registro actualizado por participante, cuando aplica. | Registro derivado |
| `F-PSEA-14` | Caso de queja o no conformidad, si la comunicacion deriva en caso formal. | Condicional |
| `F-PSEA-15` | Apelacion, si la comunicacion deriva en apelacion formal. | Condicional |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-05` | Procedimiento de comunicaciones del PEA. | Obligatorio |
| `F-PSEA-05` | Ficha basica de ronda EA. | Referencia |
| `F-PSEA-03` | Registro de participacion y carga de datos del participante. | Obligatorio cuando aplique |
| `F-PSEA-06` | Planificacion de ronda EA. | Obligatorio |
| `F-PSEA-01` | Calendario de ronda. | Referencia |
| `F-PSEA-02` | Cronograma detallado. | Referencia |
| `F-PSEA-08` | Datos reportados por participante, si la comunicacion trata reporte de datos. | Referencia |
| `F-PSEA-13` | Informe final, si la comunicacion trata cierre o emision. | Referencia |
| `F-PSEA-14` | Queja o no conformidad derivada. | Condicional |
| `F-PSEA-15` | Apelacion derivada. | Condicional |
| `P-PSEA-16` | Control de valores sensibles. | Obligatorio |
| `P-PSEA-19` | Confidencialidad operativa interna. | Obligatorio |

---

## Limites y riesgos

#### Limites de alcance

- No reemplaza `P-PSEA-05`; solo registra y normaliza comunicaciones a participantes.
- No sustituye los documentos adjuntos ni los formatos tecnicos solicitados.
- No debe usarse para emitir resultados oficiales en lugar de `F-PSEA-13`.
- No reemplaza registros de quejas, no conformidades o apelaciones.
- Debe personalizarse por participante, ronda, analitos, fechas y documentos vigentes.

#### Riesgos de interpretacion

- **Confundir plantilla con evidencia:** La plantilla maestra no es evidencia hasta que se emite y archiva una comunicacion real.
- **Divulgar informacion sensible:** No debe incluir resultados individuales, valores asignados, codigos de otros participantes ni informacion no autorizada.
- **Omitir trazabilidad:** Debe conservarse evidencia de envio, adjuntos, respuestas y cierre.
- **Usar fechas no vigentes:** Las fechas y documentos deben coincidir con el plan de ronda y cronograma aplicables.

---

## Criterio minimo de elaboracion

Cada comunicacion a participantes debe identificar emisor, destinatario, ronda, asunto, proposito, fechas relevantes, accion requerida, fecha limite, documentos adjuntos, responsable de seguimiento, evidencia de envio y estado de cierre, manteniendo alineacion con `P-PSEA-05` y control de confidencialidad segun `P-PSEA-16` y `P-PSEA-19`.
