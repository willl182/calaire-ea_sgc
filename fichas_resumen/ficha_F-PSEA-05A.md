# Ficha Resumen: F-PSEA-05A

## Identificacion

| Campo | Valor |
|---|---|
| **Codigo** | `F-PSEA-05A` |
| **Nombre decidido** | Hoja de registro del participante |
| **Tipo documental** | Subformato / registro |
| **Estado** | Elaborado |
| **Prioridad** | Media |
| **Clase de ficha** | Ficha activa |

---

## Proposito y rol

### Proposito operativo

Registra informacion del participante requerida para formalizar o confirmar su participacion en una ronda del PEA. Funciona como subformato asociado al plan de ronda (`F-PSEA-05`) y a la planificacion gobernada por `P-PSEA-04`.

### Rol en el flujo

- [x] Registro oficial
- [x] Evidencia
- [x] Entrada
- [x] Salida
- [ ] Criterio tecnico
- [ ] Instructivo
- [ ] Matriz
- [x] Soporte documental

La plantilla maestra vive en `01_bloque_general/04_formatos_maestros/`; las copias diligenciadas se conservan como evidencia de planificacion en la ronda.

---

## Aplicativos y tecnologia

#### Aplicativo asociado

- [x] `calaire-app`
- [ ] `pt_app`
- [ ] Ambos
- [ ] Ninguno

Puede diligenciarse o registrarse con soporte de `calaire-app` y conservarse como copia documental de ronda cuando aplique.

---

## Flujo de datos

#### Entradas principales

| Codigo / fuente | Descripcion | Rol en el flujo |
|---|---|---|
| `P-PSEA-04` | Procedimiento de planificacion de ronda. | Regla |
| `F-PSEA-05` | Plan de ronda EA. | Referencia |
| `F-PSEA-06` | Ficha digital de ronda EA. | Referencia |
| Participante | Datos de contacto, laboratorio, equipos o informacion solicitada. | Entrada |

#### Salidas principales

| Codigo / destino | Descripcion | Rol en el flujo |
|---|---|---|
| `02_despliegue_rondas/<ronda>/01_planificacion_ronda/` | Copia diligenciada cuando aplique. | Evidencia |
| `F-PSEA-05` | Plan de ronda actualizado o soportado por el registro. | Referencia |
| `F-PSEA-18` | Comunicacion que solicita o confirma el diligenciamiento. | Referencia |

---

## Relaciones documentales

#### Documentos relacionados

| Codigo | Relacion | Tipo de vinculo |
|---|---|---|
| `P-PSEA-04` | Procedimiento que gobierna la planificacion. | Obligatorio |
| `F-PSEA-05` | Plan de ronda al que se asocia. | Obligatorio |
| `F-PSEA-06` | Ficha digital que puede consolidar informacion de registro. | Referencia |
| `F-PSEA-18` | Comunicacion formal al participante. | Referencia |
| `P-PSEA-03` | Control de conservacion como evidencia de ronda. | Obligatorio |

---

## Limites y riesgos

#### Limites de alcance

- No sustituye el plan de ronda (`F-PSEA-05`).
- No sustituye los datos reportados por participante (`F-PSEA-08`).
- No es un procedimiento de comunicaciones (`P-PSEA-05`).
- No debe conservarse como maestro dentro de cada ronda; solo se conserva la copia diligenciada.

#### Riesgos de interpretacion

- **Confundir maestro con evidencia:** la plantilla en `01_bloque_general/04_formatos_maestros/` no es evidencia hasta que se diligencia para una ronda.
- **Duplicar datos tecnicos:** la informacion tecnica detallada del reporte de resultados pertenece a `F-PSEA-08`.
- **Omitir trazabilidad:** la copia diligenciada debe poder asociarse con participante, ronda, fecha y comunicacion relacionada.

---

## Criterio minimo de elaboracion

La hoja de registro del participante debe identificar participante, ronda, datos solicitados, responsable o fuente de diligenciamiento y relacion con el plan de ronda. La copia diligenciada se conserva en `02_despliegue_rondas/<ronda>/01_planificacion_ronda/` cuando aplique.
