# Plan de trabajo – Propuesta ISC (R Consortium) para ARcenso

Documento vivo de seguimiento. Hay una sola versión vigente: cada vez que se actualiza, se reemplaza la anterior en el contexto del proyecto.

- **Equipo:** Andrea Gomez Vargas (autora principal y mantenedora) y Emanuel Ciardullo (coautor), ambos del INDEC
- **Plantilla:** Quarto, con `isc-proposal.qmd` como archivo principal y las secciones en `proposal/00-...` a `proposal/05-...`
- **Ejemplo de referencia:** birdnetTools 2.0 (Tseng & Wood), financiado en el ciclo 2 de 2025 por USD 7.488. Tiene un problema acotado, un MVP con una sola función, un plan de 5 meses, un presupuesto por hitos (USD 36/h) y criterios de éxito verificables.
- **Referencia de montos:** en el ciclo 2 de 2025 el ISC financió 8 proyectos por entre USD 2.500 y USD 8.000.
- **Calendario del ciclo:** la convocatoria cierra el 1/10/2026, el ISC contacta a los seleccionados el 1/11/2026 y el contrato se acepta antes del 1/12/2026.

---

## Estado por sección

| Sección | Archivo | Estado |
|---|---|---|
| Executive Summary | 00-exec-summary.qmd | Vacío (se escribe al final) |
| Signatories – Project team | 01-signatories.qmd | Completo |
| Signatories – Contributors / Consulted | 01-signatories.qmd | Vacío |
| The Problem | 02-problemdefinition.qmd | Completo (quedan citas por verificar en `references.bib`) |
| Proposal – Overview | 03-proposal.qmd | Completo (falta evidencia de uso actual) |
| Proposal – Detail (MVP, Architecture, Assumptions, Dependencies, Failure modes) | 03-proposal.qmd | Completo; decisiones de diseño a validar con Andrea |
| Project plan + Budget | 04-timeline.qmd | Vacío; contenido ya definido en el paso 1 |
| Success | 05-success.qmd | Vacío |
| YAML / aspectos técnicos | isc-proposal.qmd | Con valores de plantilla |

---

## Pasos

### Paso 1 – Definir el alcance ✅ RESUELTO
- [x] Relevamiento del estado actual del paquete (ver "Decisiones tomadas")
- [x] Alcance de cobertura censal
- [x] Ejes de trabajo
- [x] Duración, fases y fechas
- [x] Horas por persona y reparto
- [x] Tarifa y monto total

### Paso 2 – The Problem (02) ✅ RESUELTO
- [x] Explicitar a quién afecta: investigadores, docentes, organismos públicos, usuarios de estadística oficial
- [x] Trabajo previo y recursos existentes (sitio del INDEC, REDATAM, otros paquetes de R con datos argentinos) y por qué no resuelven el problema
- [x] Mencionar la fragmentación de fuentes: libros impresos, PDF, Excel y sistemas cerrados como REDATAM
- [x] Pasar la URL de rOpenSci Champions a una cita en `references.bib`

### Paso 3 – Proposal: Detail (03) ✅ RESUELTO
- [x] Ajustar el Overview a los tres ejes de trabajo y al alcance del siglo XX
- [x] **Minimum Viable Product:** concreto y verificable, coherente con el alcance
- [x] **Architecture:** nuevo formato de datos que respete el límite de tamaño de CRAN, más el pipeline semi-automatizado
- [x] **Assumptions:** disponibilidad de fuentes, efectividad de la IA, horas del equipo, tamaño, acceso a herramientas de IA
- [x] **External dependencies:** paquetes de R, fuentes de datos, infraestructura y herramientas de IA
- [x] Failure modes y cómo recuperarse (tabla en la sección 03; la sección de riesgos del paso 5 remite a ella)
- [ ] Respaldar con links o evidencia el uso actual mencionado en el Overview (queda como `TODO` en el texto)
- [ ] Opcional: figura del flujo (fuente → IA → script → validación → revisión → paquete), como la Figura 1 de birdnetTools

### Paso 4 – Project plan y presupuesto (04)
- [ ] **Start-up:** repositorio (ya existe), licencia (MIT, ya definida), guía de contribución (ya existe), esquema de reportes (por ejemplo, check-ins quincenales)
- [ ] **Technical delivery:** volcar las fases y el cronograma definidos en el paso 1
- [ ] **Other aspects:** difusión (post de anuncio y de cierre en el blog del R Consortium, redes, useR! o LatinR, reuniones del ISC, R en Buenos Aires)
- [ ] **Budget:** volcar la tabla de hitos definida en el paso 1

### Paso 5 – Success (05)
- [ ] **Definition of done:** coherente con el MVP del paso 3
- [ ] **Measuring success:** marcadores intermedios y finales (release en CRAN y R-universe, cobertura censal lograda, descargas, issues, uso en docencia)
- [ ] **Riesgos para la entrega:** la carga baja por persona (unas 3 h semanales) deja margen para imprevistos
- [ ] **Future work:** 2001, 2010 y 2022 (nacional y por jurisdicción), es decir las etapas restantes del roadmap, que se aceleran gracias al pipeline

### Paso 6 – Signatories: Contributors y Consulted (01)
Se arranca en paralelo apenas estén los pasos 3 y 4.
- [ ] Definir a quién consultar: mentores de rOpenSci Champions (Luis D. Verde Arregoitia, Yanina Bellini Saibene), comunidad R, colegas
- [ ] Enviar el borrador y registrar quién dio feedback

### Paso 7 – Executive Summary (00)
- [ ] Una página con objetivo, método, entregables, resultados esperados y presupuesto

### Paso 8 – Ajustes técnicos y revisión final
- [ ] YAML: título, autores con ORCID y afiliaciones; borrar la línea de revisión de la plantilla
- [ ] Ubicar las secciones en la subcarpeta `proposal/`, que es donde apuntan los `include`
- [x] Crear `references.bib` con las citas (borrador creado en el paso 2; se completa con las citas nuevas)
- [ ] Verificar que el formato `hikmah-pdf` esté instalado; renderizar HTML y PDF
- [ ] Revisar la consistencia de fechas, montos y entregables entre secciones

---

## Decisiones tomadas

### Estado actual del paquete (relevado el 19/09/2026, versión 0.2.1)

- Funciones: `get_census()`, `check_repository()` y `arcenso_app()` (Shiny). Metadatos disponibles en `census_metadata` y `geo_metadata`.
- Infraestructura existente: CI con `R CMD check`, cobertura de tests con Codecov, licencia MIT, guía de contribución bilingüe, código de conducta, sitio pkgdown y DOI en Zenodo. El paquete no está en CRAN.
- Datos: se guardan unos 386 archivos `.rds` en `inst/extdata` (1,6 MB, alrededor de 4 KB por cuadro). Los valores numéricos están guardados como texto (`<chr>`).

| Censo | Nivel | Cuadros registrados |
|---|---|---|
| 1970 | Total país | 20 |
| 1970 | 24 jurisdicciones | 312 (13 por jurisdicción) |
| 1980 | Total país | 27 |
| **Total** | | **359** |

- Temas: estructura, fecundidad, educación, conyugal, actividad, migración, composición, habitacional y vivienda.
- Roadmap publicado: 7 etapas. La etapa 1 (1970 nacional + jurisdicciones y 1980 nacional) está completa y las etapas 2 a 7 están pendientes.

### Alcance: completar los censos del siglo XX

- **1960 completo:** publicado por el INDEC después de la última versión de ARcenso. No figura en el roadmap actual, así que hay que sumarlo.
- **1980 por jurisdicción:** etapa 5 del roadmap.
- **1991 completo, nacional y por jurisdicción:** etapas 2 y 5 del roadmap.
- Al final del proyecto, el paquete tendría todos los censos de 1960 a 1991 a nivel nacional y provincial.
- El alcance se expresa como "censo × nivel geográfico" y no en cantidad de cuadros, porque no se conoce el total de cuadros de cada publicación.

### Ejes de trabajo

1. **Ampliar la cobertura censal** según el alcance anterior.
2. **Preparar el paquete para CRAN y R-universe**, no solo en la estructura del paquete sino también adaptando el formato de las tablas para no superar el límite de espacio: tipos numéricos, compresión y consolidación de archivos. Es una mejora doble, de tamaño y de usabilidad.
3. **Semi-automatizar con IA la conversión y estandarización de cuadros**, sin perder reproducibilidad ni calidad:
   - la IA propone la extracción y la estructura tidy de cada cuadro;
   - lo que queda versionado es un script de R determinístico por cuadro o grupo de cuadros;
   - cada cuadro se valida contra totales y subtotales publicados, con tests automáticos y revisión humana;
   - la IA es parte del proceso de desarrollo, no del paquete, así que el usuario final no depende de ella.
   
   Este eje sirve tanto para las metas del proyecto como para los objetivos de largo plazo (las etapas restantes del roadmap).

### Cronograma, horas y presupuesto

Duración: 9 meses (enero a septiembre de 2027). Total: 245 horas, repartidas en partes iguales (122,5 h cada uno).

| Fase | Período | Contenido | Andrea | Emanuel | Total |
|---|---|---|---|---|---|
| 1. Diseño | Enero | Nuevo formato de datos y arquitectura, especificación del pipeline, registrar los archivos huérfanos, actualizar el roadmap | 15 | 15 | 30 |
| 2. Formato y empaquetado | Febrero – marzo | Migrar 1970 y 1980 al nuevo formato, verificar tamaño, publicar en R-universe | 25 | 15 | 40 |
| 3. Pipeline semi-automatizado | Marzo – abril | Flujo IA → script de R versionado, validación automática contra totales, protocolo de revisión humana | 15 | 35 | 50 |
| 4. Cobertura censal | Mayo – agosto | 1960, 1980 por jurisdicción y 1991 completo | 42,5 | 42,5 | 85 |
| 5. Cierre y release | Septiembre | Documentación y viñetas, testing con la comunidad, envío a CRAN, posts de difusión | 25 | 15 | 40 |
| **Total** | | | **122,5** | **122,5** | **245** |

La carga es de unas 3 horas semanales por persona.

Tarifa: USD 22,45/h (USD 5.500 / 245 h). Total: **USD 5.500**.

| Hito de pago | Fases | Período | Horas | Monto (USD) |
|---|---|---|---|---|
| 1. Diseño y formato | 1–2 | Enero – marzo | 70 | 1.571 |
| 2. Pipeline y cobertura | 3–4 | Marzo – agosto | 135 | 3.031 |
| 3. Cierre y release | 5 | Septiembre | 40 | 898 |
| **Total** | | | **245** | **5.500** |

Alternativa con tarifa redonda: 250 h a USD 22/h también suma USD 5.500 (5 h más, por ejemplo en la fase 5).

### The Problem (paso 2)

- Estructura de la sección: el problema (fragmentación de fuentes y cambios de clasificación entre rondas), a quién afecta, trabajo previo y por qué no alcanza, estado actual de ARcenso y qué habilita resolverlo.
- Trabajo previo citado: sitio del INDEC, bases REDATAM y los paquetes `redatam` y `redatamx`, y las muestras de microdatos de IPUMS International (1970–2010).
- Argumento de diferenciación: ninguna de esas fuentes ofrece los cuadros oficiales publicados por el INDEC en formato tidy. REDATAM cubre solo rondas recientes e IPUMS usa muestras que no reproducen las cifras oficiales y no incluye 1960. ARcenso es complementario, no un duplicado.
- `references.bib` tiene las entradas `arcenso`, `ropensci_champions_2024`, `redatam`, `redatamx` e `ipums_international`.

### Proposal (paso 3)

- **MVP:** versión en R-universe con el nuevo formato de datos, los cuadros de 1970 y 1980 migrados, la interfaz actual sin cambios (`get_census()`, `check_repository()`, `arcenso_app()`) y 1991 nacional incorporado con el pipeline y validado contra totales publicados.
- **Capa de datos:** valores numéricos como números, cuadros consolidados y comprimidos (por ejemplo, un archivo por censo), `census_metadata` ampliado con la fuente y el estado de validación de cada cuadro, y el cambio oculto detrás de las funciones existentes.
- **Plan B por tamaño:** separar los datos en un paquete aparte distribuido por R-universe y enviar el paquete principal a CRAN (cita `anderson_eddelbuettel_2017`).
- **Pipeline en `data-raw/`:** (1) fuente registrada, (2) extracción asistida por IA con la transcripción intermedia versionada en fuentes escaneadas, (3) script de R determinístico, (4) validación automática contra totales y entre cuadros, (5) revisión cruzada por el integrante que no procesó el cuadro. Mayormente base R.
- **Failure modes:** fuente inaccesible o de baja calidad, extracción con IA menos precisa de lo esperado, exceso de tamaño para CRAN, demoras del equipo; cada uno con su forma de recuperarse.

---

## Pendientes / preguntas abiertas

- [ ] Link y referencia de la publicación de 1960 del INDEC; niveles geográficos disponibles
- [ ] 1980 por jurisdicción: el README dice "Jurisdiction-level data not available". ¿Falta en el paquete o no hay fuente accesible? Si es lo segundo, es un supuesto crítico
- [ ] 27 archivos `.rds` sin registrar en `census_metadata`: cuadro 13 de 1970 (24 jurisdicciones), cuadro 10 nacional de 1970 y cuadros 3 y 5 de vivienda de 1980. ¿Es intencional?
- [ ] Si la semi-automatización usa APIs pagas, ¿el costo es elegible para el ISC o se cubre por otro lado?
- [ ] Verificar si el vínculo laboral con el INDEC tiene restricciones para cobrar un grant externo (el ISC usa un acuerdo estándar de consultor individual)
- [ ] Decidir entre la tarifa de USD 22,45 (245 h) o la de USD 22 (250 h)
- [ ] `references.bib`: verificar las entradas marcadas con `% VERIFICAR` (título del post de rOpenSci, versiones en CRAN de `redatam` y `redatamx`, versión de IPUMS)
- [ ] Confirmar desde qué ronda hay bases REDATAM públicas del INDEC (¿1991 o 2001?) y ajustar la frase "only available for recent rounds" si hace falta
- [ ] ¿Hay otros paquetes de R con datos censales argentinos que convenga mencionar en The Problem?
- [ ] Validar con Andrea las decisiones de diseño del paso 3 (MVP, formato de datos, plan B, pipeline)
- [ ] Evidencia de uso actual de ARcenso: charla en useR! 2025, cursos, materiales docentes, usuarios
- [ ] `references.bib`: verificar la entrada `anderson_eddelbuettel_2017`
