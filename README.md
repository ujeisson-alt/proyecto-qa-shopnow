# Proyecto QA End-to-End — ShopNow: Módulo Registro y Perfil

![Estado](https://img.shields.io/badge/estado-cerrado-success) ![Conclusión](https://img.shields.io/badge/recomendaci%C3%B3n-NO--GO-critical) ![Casos](https://img.shields.io/badge/casos%20de%20prueba-36-blue) ![Bugs](https://img.shields.io/badge/bugs-8-orange) ![Cobertura](https://img.shields.io/badge/cobertura%20de%20requerimientos-100%25-brightgreen)

## Descripción

Testing end-to-end del módulo de Registro y Perfil de Usuario de **ShopNow S.A.**, plataforma de e-commerce argentina *(empresa ficticia — proyecto educativo)*. El módulo es la puerta de entrada de la plataforma: incluye el alta de usuarios, la gestión de datos personales, el cambio de contraseña, la foto de perfil y las direcciones de envío.

El proyecto cubrió el ciclo completo de QA: análisis de requerimientos, diseño de casos de prueba, ejecución con evidencias, reporte de defectos en Jira e informe final con recomendación GO / NO-GO.

## Mi Rol

**QA Tester Junior** — responsable del análisis de requerimientos, el diseño y la ejecución de pruebas funcionales, de compatibilidad, de interfaz y de validaciones de seguridad básica del módulo, y de la elaboración del informe final.

## Stack de Herramientas

`Jira` · `Google Sheets / Excel` · `Chrome DevTools` · `GitHub` · `Lightshot` · `SCRUM`

## Métricas del Proyecto

| Indicador | Resultado |
|---|---|
| Casos diseñados | **36** (32 del diseño base + 4 adicionales para cerrar una brecha de cobertura) |
| Casos ejecutados | **34 (94,4 %)** — 2 bloqueados y documentados |
| Passed / Failed / Blocked | **27 / 7 / 2** |
| Tasa de éxito | **75,0 %** sobre el total · **79,4 %** sobre los ejecutados |
| Bugs encontrados | **8** — 1 crítico (S1), 3 mayores (S2), 3 menores (S3), 1 trivial (S4) |
| Cobertura de requerimientos | **100 %** (11 RF + 4 RNF) |
| Técnicas aplicadas | Partición de equivalencias · Valores límite |
| Evidencias | 45 capturas nombradas por caso y por defecto |

## Hallazgos destacados

| Bug | Severidad | Hallazgo | Impacto |
|---|---|---|---|
| **BUG-002** | S1 — Crítico | En Firefox el botón "Crear cuenta" no responde: no se dispara ninguna petición a `/register` y la consola arroja `Uncaught TypeError: e.submitForm is not a function` | Bloquea el alta de usuarios en Firefox |
| **BUG-004** | S2 — Mayor (P1) | En mobile 375 px el botón "Guardar cambios" queda fuera del viewport | Impide editar el perfil desde mobile. **Reabierto** tras el retest del build 1.3 |
| **BUG-001** | S2 — Mayor | El campo contraseña muestra el texto en claro por defecto (incumple RNF-04) | Expone credenciales ante terceros |

## Conclusión

> **NO-GO recomendado.** Existe 1 defecto crítico (BUG-002) que bloquea por completo el registro en Firefox y 3 defectos mayores (BUG-001, BUG-003, BUG-004) que impactan directamente la conversión de nuevos usuarios y la experiencia mobile. El criterio de salida definido en el plan de testing exige cero defectos S1 abiertos para recomendar GO.

La justificación completa, con datos y condiciones para revertir la recomendación, está en el [informe final](informe-final/informe-final-qa-shopnow.pdf).

## Estructura del repositorio

```
proyecto-qa-shopnow/
├── README.md
├── docs/
│   ├── analisis-requerimientos.xlsx    ← 11 RF + 4 RNF con prioridad, criterio de aceptación y riesgo
│   ├── matriz-trazabilidad.xlsx        ← requerimiento ↔ casos ↔ resultado ↔ bugs
│   ├── plan-de-testing.md              ← alcance, estrategia, técnicas, criterios y cronograma
│   └── daily-reports.md                ← 14 daily reports de los 4 sprints
├── casos-de-prueba/
│   └── matriz-de-prueba.xlsx           ← 36 casos con pasos, datos y resultados reales + dashboard
├── evidencias/
│   ├── README.md
│   └── (45 capturas nombradas CP-XXX / BUG-XXX)
├── bugs/
│   ├── bug-reports-detallados.md       ← los 8 bugs con plantilla completa y ciclo de vida
│   └── reporte-bugs-resumen.xlsx       ← resumen por severidad y por estado en Jira
├── informe-final/
│   └── informe-final-qa-shopnow.pdf    ← informe de 7 páginas con las 6 secciones y el GO/NO-GO
└── presentacion/
    ├── sprint-review-qa-shopnow.pdf    ← deck de 15 diapositivas del Sprint Review (12 min)
    └── guion-sprint-review.md          ← guion, tiempos y preguntas probables con su respuesta
```

## Cómo recorrer este portafolio

1. **`docs/plan-de-testing.md`** — qué se testeó, con qué estrategia y bajo qué criterios de entrada y salida.
2. **`docs/analisis-requerimientos.xlsx`** y **`docs/matriz-trazabilidad.xlsx`** — cómo se pasó de la documentación funcional a una cobertura verificable del 100 %.
3. **`casos-de-prueba/matriz-de-prueba.xlsx`** — los 36 casos con su resultado real; la hoja *Dashboard* calcula todas las métricas con fórmulas.
4. **`bugs/bug-reports-detallados.md`** — los 8 defectos con pasos de reproducción, evidencia, impacto en el negocio y ciclo de vida simulado (New → Closed, con un Reopened).
5. **`informe-final/informe-final-qa-shopnow.pdf`** — el documento de cierre y la recomendación GO / NO-GO.
6. **`presentacion/sprint-review-qa-shopnow.pdf`** — cómo se presentaron estos resultados al equipo en el Sprint Review.

## Decisiones de testing que vale la pena destacar

- **Brecha de cobertura detectada y cerrada:** el diseño base de 32 casos dejaba sin verificar RF-10, RF-11 y RNF-01. Se diseñaron CP-033 a CP-036 antes de ejecutar, lo que llevó la cobertura del 80 % al 100 %.
- **Bloqueos documentados, no ocultados:** CP-016 quedó bloqueado por BUG-003 y CP-030 por no disponer de un dispositivo iOS. Ambos están registrados como *Blocked* con su causa, y el riesgo de CP-030 fue escalado a la QA Lead.
- **Severidad y prioridad se gestionan por separado:** BUG-004 es S2 por impacto técnico, pero P1 por impacto de negocio, ya que bloquea al tráfico mobile.
- **El retest puede reabrir un defecto:** BUG-004 volvió a fallar sobre el build 1.3 y se reabrió con evidencia nueva en lugar de cerrarse por confianza en el fix.

---

*Proyecto formativo de la Guía de proyectos para QA Tester (Talently Lab). ShopNow S.A., su entorno de staging, su equipo y los defectos descritos son ficticios y tienen fines exclusivamente educativos.*

**Autor:** Jeisson Marín Uribe Luis — QA Tester Junior · Bogotá, Colombia
