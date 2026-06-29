# Sesion grill SGC - estructura documental y despliegue de rondas

Fecha de sesion: 2026-06-27

## Contexto inicial

Se revisaron los documentos base del SGC CALAIRE-EA:

- `doc_calaire-ea.md`
- `documento-sgc.md`
- `sgc_13528.md`
- `sgc_17043.md`
- `mapa_navegacion_sgc_pea.html`

Se uso el skill `grill-me` para definir una estructura organizada del SGC, separando documentos base del sistema y despliegue operativo por ronda, incluyendo registros de ronda.

## Lectura inicial de contexto

Los documentos revisados muestran que CALAIRE-EA cuenta con:

- Arquitectura documental basada en `DG-PSEA`, `P-PSEA`, `I-PSEA` y `F-PSEA`.
- Procedimientos tecnicos por analito para NO/NO2, CO, O3 y SO2.
- Procedimientos internos para planificacion, comunicaciones, preparacion del item, diseno estadistico, flujo de datos, informe y gestion SGC.
- Formatos maestros para calendario, cronograma, plan de ronda, ficha digital, datos, preprocesamiento, H/E, dataset oficial, informe, quejas/NC, apelaciones, competencia y proveedores.
- Un mapa de navegacion que inicialmente no incluia todos los formatos activos necesarios para el checklist de ronda.
- Evidencia historica de que la "prueba piloto" no debe operar como bloque documental independiente, sino como ronda ejecutada bajo el SGC.

## Desarrollo de la sesion de grill

### 1. Separacion entre SGC maestro y rondas

Pregunta: si el SGC debe organizarse en dos capas.

Decision:

- Separar el sistema en:
  - `01_sgc_maestro/` como capa conceptual de documentos controlados.
  - `02_despliegue_rondas/` como capa conceptual de registros/evidencias por ronda.

Nota:

- No se pidio ejecutar renombrado fisico durante la sesion.
- La estructura actual `01_bloque_general/` sigue siendo la ubicacion real activa del SGC maestro.

### 2. Naturaleza de la prueba piloto

Pregunta: si la prueba piloto independiente debe ser bloque paralelo o ronda.

Decision:

- La prueba piloto independiente es una ronda.
- No debe tratarse como otro sistema documental.

### 3. Codigo de ronda de la prueba piloto

Pregunta: como nombrar la ronda.

Decision:

- Codigo definido: `EA-PP-2026-R1`.

### 4. Carpetas de ronda

Pregunta: si la ronda debe organizarse por estados (`borrador`, `oficial`, `soporte`) o por etapas.

Decision:

- No usar estados manuales.
- Usar etapas simples que reflejen el flujo operativo.

Estructura acordada:

```text
02_despliegue_rondas/
  EA-PP-2026-R1/
    checklist_ronda.md
    01_planificacion_ronda/
    02_comunicaciones_participantes/
    03_preparacion_item/
    04_datos_y_preprocesamiento/
    05_homogeneidad_estabilidad/
    06_analisis_e_informe/
    07_cierre_sgc/
```

### 5. Relacion con procedimientos internos

Pregunta: si las carpetas deben reflejar procedimientos internos.

Decision:

- Si. Las etapas deben corresponder al flujo gobernado por los procedimientos, pero los nombres de carpetas deben ser simples.
- No usar codigos de procedimiento en los nombres de carpetas.

Relacion conceptual:

- `01_planificacion_ronda`: principalmente `P-PSEA-04`.
- `02_comunicaciones_participantes`: principalmente `P-PSEA-05`.
- `03_preparacion_item`: principalmente `P-PSEA-06` y procedimientos tecnicos por gas cuando apliquen.
- `04_datos_y_preprocesamiento`: principalmente `P-PSEA-08`.
- `05_homogeneidad_estabilidad`: `P-PSEA-06`, `P-PSEA-07` y formatos H/E.
- `06_analisis_e_informe`: `P-PSEA-07`, `P-PSEA-09`.
- `07_cierre_sgc`: procedimientos de gestion, quejas, apelaciones, NC y cierre.

### 6. Ajuste conceptual de P-PSEA-02 y P-PSEA-03

Pregunta: si era necesario ajustar `P-PSEA-02` y `P-PSEA-03`.

Decision:

- Si, conceptualmente.
- `P-PSEA-02` debe fijar la arquitectura documental maestra y diferenciar documentos maestros de registros de ronda.
- `P-PSEA-03` debe fijar la estructura simple de cada ronda y el control de registros/evidencias.

Restriccion:

- El usuario aclaro que ya ajusto esos procedimientos por aparte.
- No se editaron archivos.

### 7. Checklist de ronda

Pregunta: si cada ronda debe contener formatos vacios o solo registros diligenciados.

Decision:

- La ronda no debe crearse con formatos maestros vacios.
- Debe crearse con un `checklist_ronda.md` en la raiz.
- Los formatos maestros se copian manualmente cuando se diligencien.
- Mas adelante se puede evaluar automatizar la copia.

### 8. Ubicacion del checklist

Pregunta: checklist unico en raiz o checklist por etapa.

Decision:

- Un solo `checklist_ronda.md` en la raiz de cada ronda.
- El checklist se organiza por etapas.

### 9. Naturaleza del checklist

Pregunta: si el checklist debe tener datos basicos, metadatos, rutas o estados.

Decision:

- No.
- Es un checklist simple.
- No debe tener metadatos.
- No debe tener rutas.
- No debe tener estados.
- Solo checks.

### 10. Alcance del checklist

Pregunta: si el checklist debe incluir solo formatos `F-PSEA` o tambien evidencias complementarias.

Decision:

- Debe incluir ambos:
  - Registros codificados `F-PSEA-*`.
  - Evidencias complementarias genericas.

### 11. Checklist general vs parametrizado por tipo de ronda

Pregunta: si el checklist depende del tipo de ronda.

Decision:

- No.
- El checklist es general para cualquier ronda.
- Todavia no se parametrizan tipos de ronda.

### 12. Organizacion interna del checklist

Pregunta: si listar por codigo o por actividad/evidencia.

Decision:

- Organizar por actividad/etapa.
- Dentro de cada actividad, listar los codigos documentales y evidencias complementarias.

### 13. Procedimientos e instructivos en checklist

Pregunta: si incluir procedimientos e instructivos como documentos aplicables.

Decision:

- No.
- El checklist lista solo registros/evidencias generadas de la ronda.
- Los procedimientos e instructivos permanecen en el SGC maestro como reglas.

### 14. Nombres de evidencias complementarias

Pregunta: si definir una convencion de nombres para evidencias complementarias.

Decision:

- No.
- Dejarlas genericas, sin convencion.

### 15. Carpetas vacias

Pregunta: si las carpetas de etapa deben existir desde el inicio.

Decision:

- Si.
- Cada ronda debe crearse con las siete carpetas desde el inicio.

### 16. Script auxiliar para crear ronda

Pregunta: si debe existir un script auxiliar.

Decision:

- Si.
- Debe estar junto a `P-PSEA-03`, no en `scripts/`.
- Tambien la plantilla del checklist debe estar junto a `P-PSEA-03`.
- El script y la plantilla no deben llevar codigo documental.

Ubicacion acordada:

```text
01_bloque_general/02_procedimientos/
  crear_estructura_ronda.sh
  plantilla_checklist_ronda.md
```

### 17. Destino del script

Pregunta: donde crea la estructura.

Decision:

- Siempre crea en `02_despliegue_rondas/`.
- Crea `02_despliegue_rondas/` si no existe.

### 18. Comportamiento del script

Decisiones:

- Recibe un unico argumento: codigo de ronda.
- Crea una sola ronda por ejecucion.
- Valida codigo de ronda con patron:

```regex
^EA-[A-Z0-9]+-[0-9]{4}-R[0-9]+$
```

- Acepta ejemplos como:
  - `EA-PP-2026-R1`
  - `EA-GASES-2026-R2`
  - `EA-PILOTO-2027-R10`
- No acepta espacios ni rutas raras.
- Funciona aunque se ejecute desde cualquier carpeta.
- Usa su propia ubicacion para encontrar la plantilla y calcular la raiz del repo.
- Crea las siete carpetas de etapa.
- Crea `.gitkeep` en cada carpeta.
- Si la ronda existe, completa faltantes.
- No borra nada.
- No sobrescribe `checklist_ronda.md` si ya existe.
- Si falta `checklist_ronda.md`, lo crea desde `plantilla_checklist_ronda.md`.
- Imprime resumen simple al final.
- No elimina `.gitkeep` automaticamente cuando la carpeta deje de estar vacia.

### 19. Lenguaje del script

Pregunta: Bash o Python.

Decision:

- Bash.

### 20. Plantilla del checklist

Decision:

- `plantilla_checklist_ronda.md` contiene solo el checklist.
- No contiene `.gitkeep`.
- No contiene metadatos.
- No contiene rutas.

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

### 21. Ubicacion de formatos especificos

Decisiones:

- `F-PSEA-04` va en `01_planificacion_ronda`, porque es informacion de equipos/instrumentos del participante para planificar la ronda, no del item de ensayo.
- `F-PSEA-05A` va en `01_planificacion_ronda`.
- `F-PSEA-16` va en `01_planificacion_ronda`.
- `F-PSEA-17` va en `01_planificacion_ronda`, si aplica.
- `F-PSEA-18` va en `02_comunicaciones_participantes`.
- `F-PSEA-07` va en `03_preparacion_item`.
- `F-PSEA-08`, `F-PSEA-09`, `F-PSEA-10` y `F-PSEA-12` van en `04_datos_y_preprocesamiento`.
- `F-PSEA-11` y `F-PSEA-11A-D` van juntos en `05_homogeneidad_estabilidad`.
- `F-PSEA-13` y evidencia de envio del informe final van en `06_analisis_e_informe`.
- `F-PSEA-14` y `F-PSEA-15` van en `07_cierre_sgc`.

### 22. Alcance de F-PSEA-10

Pregunta: si `F-PSEA-10` cubre tambien preprocesamiento de H/E.

Decision:

- No.
- `F-PSEA-10` corresponde al preprocesamiento de datos de participantes para analisis PT.
- H/E se controla con `F-PSEA-11` y `F-PSEA-11A-D`.

### 23. Comunicaciones

Pregunta: si debe existir formato oficial de comunicaciones.

Decision:

- Si.
- Se adopta `F-PSEA-18` como formato de comunicacion oficial al participante.
- Ya esta en elaboracion segun el usuario.
- Lo demas son correos, respuestas, acuses o comunicaciones complementarias.
- El envio del informe final al participante queda en `06_analisis_e_informe`, no en `02_comunicaciones_participantes`.

### 24. Mapa de navegacion

Pregunta: si todos los formatos del checklist aparecen en `mapa_navegacion_sgc_pea.html`.

Resultado de revision:

Formatos encontrados en el mapa:

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

Faltaban en el mapa frente al checklist:

```text
F-PSEA-05A
F-PSEA-14
F-PSEA-15
F-PSEA-16
F-PSEA-17
```

Decision:

- Estos formatos deben estar en el mapa.
- El usuario los agregara.

Ubicaciones acordadas:

- `F-PSEA-05A`: planificacion.
- `F-PSEA-16`: planificacion.
- `F-PSEA-17`: planificacion.
- `F-PSEA-14`: cierre.
- `F-PSEA-15`: cierre.

### 25. Migracion de estructura vieja

Pregunta: si `02_despliegue_rondas/` reemplaza por completo `02_prueba_piloto_rondas/`.

Decision:

- `02_despliegue_rondas/` sera la nueva estructura.
- `02_prueba_piloto_rondas/` queda temporalmente como historico/fuente de migracion.

Pregunta: si las carpetas actuales se consolidan en una sola ronda.

Decision:

- No.
- Cada carpeta representa una ronda diferente por ahora.

Mapeo temporal acordado:

```text
02_prueba_piloto_rondas/01_ronda_simple/
  -> 02_despliegue_rondas/EA-PP-2026-R1/

02_prueba_piloto_rondas/02_ronda_compleja_fase1/
  -> 02_despliegue_rondas/EA-PP-2026-R2/

02_prueba_piloto_rondas/03_ronda_compleja_fase2/
  -> 02_despliegue_rondas/EA-PP-2026-R3/
```

Pregunta: que hacer con `02_prueba_piloto_rondas/00_planificacion/`.

Decision:

- Queda aparte por ahora como material historico/general de planificacion.

Pregunta: migracion manual o script.

Decision:

- Migracion manual.
- Copiar, no mover.
- El usuario controlara la migracion.

### 26. Raiz de cada ronda

Pregunta: que puede vivir en la raiz de cada ronda.

Decision:

- Solo `checklist_ronda.md` y las siete carpetas.
- No README.
- No otros archivos sueltos.

### 27. Nombres de archivos dentro de ronda

Pregunta: si los registros codificados deben conservar codigo documental al inicio.

Decision:

- Si.

Pregunta: si agregar codigo de ronda al nombre de archivo.

Decision:

- No dentro de la carpeta de ronda.
- La ruta ya identifica la ronda.

Ejemplo:

```text
EA-PP-2026-R1/
  04_datos_y_preprocesamiento/
    F-PSEA-08 Datos reportados por participante.xlsx
```

### 28. Multiples extensiones por registro

Pregunta: si se pueden conservar `.md`, `.xlsx`, `.csv`, `.docx` juntos.

Decision:

- Si.
- Si estan en la ronda, son registro/evidencia de la ronda.
- No tratar `.md` como descriptivo por defecto.

### 29. Formatos maestros

Pregunta: si el script debe copiar formatos maestros.

Decision:

- No por ahora.
- Se copian manualmente cuando se diligencien.
- Luego se puede revisar si se automatiza.

### 30. Referencias en P-PSEA-02 y P-PSEA-03

Pregunta: si los procedimientos deben mencionar los auxiliares.

Decision:

- Si, de forma minima.
- `P-PSEA-02`: mencionar que los registros de ronda se despliegan en `02_despliegue_rondas/<codigo_ronda>/` y no forman parte del inventario maestro.
- `P-PSEA-03`: mencionar que la estructura inicial puede generarse con `crear_estructura_ronda.sh <codigo_ronda>` usando `plantilla_checklist_ronda.md`.
- No codificar script ni plantilla como documentos `P`, `I` o `F`.

### 31. Mapa y auxiliares

Pregunta: si el mapa debe enlazar al script y plantilla.

Decision:

- No.
- El mapa representa el SGC documental.
- El script y la plantilla son auxiliares operativos referenciados por `P-PSEA-03`.

## Estado final de la sesion

No se editaron los documentos del SGC durante la sesion de grill.

Pendientes acordados:

1. Crear en una sesion posterior, cuando el usuario lo autorice:
   - `01_bloque_general/02_procedimientos/crear_estructura_ronda.sh`
   - `01_bloque_general/02_procedimientos/plantilla_checklist_ronda.md`
2. Ajustar referencias en `P-PSEA-02` y `P-PSEA-03` si no quedaron ya incorporadas por el usuario.
3. Agregar al mapa los formatos faltantes:
   - `F-PSEA-05A`
   - `F-PSEA-14`
   - `F-PSEA-15`
   - `F-PSEA-16`
   - `F-PSEA-17`
4. Migrar manualmente/copiar evidencias desde `02_prueba_piloto_rondas/` hacia `02_despliegue_rondas/` cuando corresponda.

