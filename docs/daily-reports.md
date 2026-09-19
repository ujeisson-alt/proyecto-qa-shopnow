# Daily Reports — ShopNow QA | Módulo Registro y Perfil

> Formato SCRUM: ¿qué hice ayer? · ¿qué voy a hacer hoy? · ¿tengo algún bloqueo?
> QA Tester: Jeisson Marín Uribe Luis — Reporta a: Sofía Peralta (QA Lead)

---

## Sprint 1 — Análisis y Planificación

### Día 1 / Sprint 1 — 25/08/2026
**¿Qué hice ayer?** → Leí dos veces la documentación del módulo: la primera como usuario que quiere registrarse, la segunda como tester buscando puntos de falla. Dibujé los dos flujos (registro en 6 pasos, edición de perfil en 4 pasos).
**¿Qué voy a hacer hoy?** → Relevar los requerimientos funcionales RF-01 a RF-07 en la planilla de análisis.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 1 — 26/08/2026
**¿Qué hice ayer?** → Completé el relevamiento de los requerimientos funcionales RF-01 a RF-07 y anoté 12 preguntas abiertas sobre el módulo.
**¿Qué voy a hacer hoy?** → Documentar RF-08 a RF-11 y los no funcionales RNF-01 a RNF-04, y comenzar la matriz de trazabilidad.
**¿Tengo algún bloqueo?** → Sí: no tengo claro el criterio exacto de "fortaleza de contraseña" para RF-03. Asumo mínimo 8 caracteres, 1 mayúscula y 1 número, y lo consulto con la QA Lead.

### Día 3 / Sprint 1 — 27/08/2026
**¿Qué hice ayer?** → Cerré los 15 requerimientos (11 RF + 4 RNF) con ID, descripción, prioridad, criterio de aceptación y riesgo. La QA Lead confirmó el criterio de RF-03.
**¿Qué voy a hacer hoy?** → Configurar el proyecto en Jira (Epic, Stories del Sprint 1, labels de severidad) y armar la primera versión de la matriz de trazabilidad.
**¿Tengo algún bloqueo?** → No.

### Día 4 / Sprint 1 — 28/08/2026
**¿Qué hice ayer?** → Dejé el Sprint 1 activo en Jira con las tres Stories y sus criterios de aceptación.
**¿Qué voy a hacer hoy?** → Revisar la matriz de trazabilidad buscando requerimientos sin casos asociados antes de pasar a la Fase 2.
**¿Tengo algún bloqueo?** → No, pero detecté un riesgo: RF-10, RF-11 y RNF-01 no tienen casos previstos en el diseño base. Lo llevo a la planificación de la Fase 2.

---

## Sprint 2 — Diseño de Casos de Prueba

### Día 1 / Sprint 2 — 01/09/2026
**¿Qué hice ayer?** → Cerré la Fase 1 con los 15 requerimientos documentados y Jira configurado.
**¿Qué voy a hacer hoy?** → Diseñar los casos de los flujos 1 y 2 (registro y validación de contraseña) aplicando partición de equivalencias.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 2 — 03/09/2026
**¿Qué hice ayer?** → Escribí CP-001 a CP-016 (registro, contraseña, T&C y email de bienvenida).
**¿Qué voy a hacer hoy?** → Diseñar CP-017 a CP-032 (perfil, cambio de contraseña, foto y compatibilidad/responsive) aplicando valores límite.
**¿Tengo algún bloqueo?** → No.

### Día 3 / Sprint 2 — 05/09/2026
**¿Qué hice ayer?** → Completé los 32 casos del diseño base y los cargué en Jira como subtareas del sprint.
**¿Qué voy a hacer hoy?** → Cerrar la brecha detectada en la Fase 1: diseñar CP-033 a CP-036 para cubrir RF-10, RF-11 y RNF-01, y actualizar la matriz de trazabilidad.
**¿Tengo algún bloqueo?** → No. Con los 4 casos adicionales la cobertura de requerimientos llega al 100 %.

---

## Sprint 3 — Ejecución de Pruebas

### Día 1 / Sprint 3 — 08/09/2026
**¿Qué hice ayer?** → Cerré el diseño con 36 casos y la matriz de trazabilidad al 100 %.
**¿Qué voy a hacer hoy?** → Ejecutar CP-001 a CP-018 en Chrome, capturando evidencia de cada caso.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 3 — 10/09/2026
**¿Qué hice ayer?** → Ejecuté CP-001 a CP-018. Encontré 3 fallas: contraseña visible en claro (CP-010), mensaje genérico en email duplicado (CP-005) y demora de 15 minutos en el email de bienvenida (CP-015).
**¿Qué voy a hacer hoy?** → Ejecutar CP-019 a CP-036, incluyendo compatibilidad en Firefox y responsive en 375 px y 768 px.
**¿Tengo algún bloqueo?** → Sí: CP-016 queda bloqueado porque el email de bienvenida no llega dentro de la ventana de ejecución (causa: la falla detectada en CP-015).

### Día 3 / Sprint 3 — 12/09/2026
**¿Qué hice ayer?** → Ejecuté CP-019 a CP-036. Encontré una falla crítica: en Firefox el botón "Crear cuenta" no responde y la consola muestra `Uncaught TypeError: e.submitForm is not a function`.
**¿Qué voy a hacer hoy?** → Repetir la falla de Firefox en una segunda máquina para confirmar que es reproducible y no un problema de mi entorno, y cerrar la matriz con los resultados reales.
**¿Tengo algún bloqueo?** → Sí: CP-030 (Safari mobile) queda bloqueado por no disponer de dispositivo iOS. Escalado a la QA Lead.

---

## Sprint 4 — Reporte, Cierre y Portafolio

### Día 1 / Sprint 4 — 15/09/2026
**¿Qué hice ayer?** → Confirmé la falla de Firefox en una segunda máquina: es reproducible al 100 %.
**¿Qué voy a hacer hoy?** → Documentar los 8 bugs en Jira con plantilla completa, evidencia y caso vinculado.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 4 — 16/09/2026
**¿Qué hice ayer?** → Documenté BUG-001 a BUG-008 con severidad, prioridad e impacto en el negocio.
**¿Qué voy a hacer hoy?** → Simular el ciclo de vida completo en BUG-001, BUG-002 y BUG-005, y retestear BUG-004 sobre el build 1.3.
**¿Tengo algún bloqueo?** → No.

### Día 3 / Sprint 4 — 17/09/2026
**¿Qué hice ayer?** → Cerré BUG-001, BUG-002 y BUG-005 verificados en el build 1.3. Reabrí BUG-004: el botón sigue recortado en 375×667.
**¿Qué voy a hacer hoy?** → Redactar el informe final con las métricas reales y la recomendación GO / NO-GO.
**¿Tengo algún bloqueo?** → No.

### Día 4 / Sprint 4 — 18/09/2026
**¿Qué hice ayer?** → Emití el informe final con recomendación **NO-GO** justificada en 1 bug S1 y 3 bugs S2.
**¿Qué voy a hacer hoy?** → Publicar el repositorio en GitHub con todos los artefactos y preparar la presentación del Sprint Review.
**¿Tengo algún bloqueo?** → No.
