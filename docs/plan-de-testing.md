# Plan de Testing — ShopNow S.A. | Módulo de Registro y Perfil de Usuario

| Campo | Detalle |
|---|---|
| **Proyecto** | ShopNow QA — Registro y Perfil |
| **Módulo bajo prueba** | Registro de nuevo usuario y Gestión de perfil |
| **Entorno** | Staging — `https://staging.shopnow.com.ar` |
| **Metodología** | SCRUM — sprints semanales |
| **QA Tester** | Jeisson Marín Uribe Luis (QA Tester Junior) |
| **QA Lead** | Sofía Peralta |
| **Product Owner** | Valentina Díaz |
| **Scrum Master** | Rodrigo Méndez |
| **Período** | 24/08/2026 – 18/09/2026 (4 sprints) |
| **Versión del plan** | 1.2 (actualizada al cierre de la Fase 3) |

---

## 1. Objetivo

Verificar que el módulo de Registro y Perfil de Usuario cumple los 11 requerimientos funcionales y los 4 no funcionales definidos por la PO, antes de habilitar su paso a producción. El módulo es la puerta de entrada al ecosistema de ShopNow: si falla, ningún usuario nuevo puede crear una cuenta ni operar en la plataforma.

## 2. Alcance

### Incluido
- Testing funcional del formulario de registro (validaciones de email, contraseña, T&C, email de bienvenida).
- Testing funcional del panel de perfil (datos personales, cambio de contraseña, foto de perfil, direcciones de envío).
- Pruebas de compatibilidad en Chrome, Firefox y Safari mobile.
- Pruebas de interfaz y diseño responsive en 375 px, 768 px y desktop 1920×1080.
- Validación de seguridad básica: enmascarado del campo contraseña (RNF-04).
- Medición de tiempo de carga de la página de registro (RNF-01).

### Fuera de alcance
- Automatización de pruebas (Selenium, Cypress).
- Testing avanzado de APIs con Postman.
- Pruebas de carga o estrés (JMeter, k6).
- Testing de seguridad avanzado / pentesting.
- Acceso al código fuente y gestión del backlog de producto.
- Testing del flujo de compra (pertenece a otro módulo).

## 3. Estrategia de pruebas

| Tipo de prueba | Objetivo | Técnica aplicada |
|---|---|---|
| Funcional positiva | Confirmar que los flujos principales funcionan con datos válidos | Casos de flujo principal |
| Funcional negativa | Confirmar que el sistema rechaza datos inválidos con el mensaje correcto | Partición de equivalencias |
| Valores límite | Verificar el comportamiento en los bordes permitidos y fuera de ellos | Análisis de valores límite |
| Compatibilidad | Detectar diferencias entre navegadores | Ejecución cruzada Chrome / Firefox / Safari |
| Interfaz / responsive | Validar visibilidad y operabilidad de los controles | Inspección con DevTools en 375 px y 768 px |
| No funcional | Medir el tiempo de carga contra el SLA | DevTools → Network (evento *Load*) |

### Técnicas de diseño aplicadas

**Partición de equivalencias — campo Contraseña (RF-03: mínimo 8 caracteres, 1 mayúscula y 1 número)**

| Partición | Dato de ejemplo | Clase | Caso |
|---|---|---|---|
| Menos de 8 caracteres | `abc1A` | Inválida | CP-007 |
| 8 caracteres sin mayúscula | `abcde123` | Inválida | CP-008 |
| 8 caracteres sin número | `AbcdefGH` | Inválida | CP-009 |
| 8 caracteres válidos | `Abcde123` | Válida | CP-010 |
| 20 caracteres válidos | `MiClaveSegura2024!` | Válida | CP-022 |
| Campo vacío | `` | Inválida | CP-012 |

**Valores límite — campo Teléfono (10 a 11 dígitos)**

| Valor | Dígitos | Resultado esperado | Caso |
|---|---|---|---|
| `123456789` | 9 | Inválido | CP-019 |
| `1234567890` | 10 | Válido | CP-020 |
| `12345678901` | 11 | Válido | CP-020 (variante) |
| `123456789012` | 12 | Inválido | CP-019 (variante) |
| `1234ABCD90` | 10 con letras | Inválido | CP-019 (variante) |

**Valores límite — Foto de perfil (máx. 2 MB)**: 1,2 MB → válido (CP-025) · exactamente 2.048 KB → válido (CP-028) · 2,1 MB → inválido (CP-026) · formato PDF → inválido (CP-027).

**Valores límite — Direcciones de envío (máx. 5)**: 5 direcciones → válido (CP-033) · 6ª dirección → inválido (CP-034).

## 4. Entorno y datos de prueba

| Elemento | Configuración |
|---|---|
| URL | `https://staging.shopnow.com.ar` |
| Navegadores | Chrome 120, Firefox 121, Safari mobile |
| Resoluciones | Desktop 1920×1080 · Tablet 768 px · Mobile 375 px |
| Emails de prueba | `qa_test01@mail.com` … `qa_test07@mail.com` (incremental) |
| Contraseña de prueba | `TestPass1234!` (cumple RF-03) |
| Usuario de test | `qa_tester@shopnow.com.ar` / `ShopNow2024!` |
| Herramientas | Jira · Google Sheets · Chrome DevTools · GitHub · Lightshot |

> Las credenciales listadas son ficticias y pertenecen a un entorno educativo simulado.

## 5. Criterios de entrada y salida

**Criterios de entrada**
- Los 11 RF y 4 RNF están documentados y aprobados por la PO.
- La matriz de trazabilidad cubre el 100 % de los requerimientos.
- El entorno de staging está desplegado y accesible.
- El proyecto en Jira tiene el Epic, las Stories y el Sprint activo.

**Criterios de salida**
- El 100 % de los casos diseñados fue ejecutado o formalmente bloqueado y documentado.
- Todos los defectos encontrados están reportados en Jira con evidencia y caso vinculado.
- Cero defectos S1 (críticos) abiertos para recomendar GO.
- El informe final está emitido con recomendación GO / NO-GO justificada con datos.

## 6. Criterios de severidad y prioridad

| Severidad | Definición | Prioridad | Definición |
|---|---|---|---|
| S1 — Crítico | Bloquea una funcionalidad esencial, sin workaround | P1 — Crítica | Debe corregirse antes del go-live |
| S2 — Mayor | Afecta gravemente una función importante; hay workaround parcial | P2 — Alta | Se corrige en el sprint actual |
| S3 — Menor | Falla de comportamiento o mensaje que no impide completar el flujo | P3 — Media | Se planifica para el siguiente sprint |
| S4 — Trivial | Defecto cosmético o de texto, sin impacto funcional | P4 — Baja | Se atiende cuando haya capacidad |

> Severidad la define QA según el impacto técnico; prioridad la define el PO según el impacto en el negocio. Por eso BUG-004 es S2 pero P1: no es crítico técnicamente, pero bloquea al tráfico mobile.

## 7. Ciclo de vida del defecto

```
New → In Progress → Fixed → Retesting → Closed
                                  ↓
                              Reopened → In Progress → …
```

- **New**: el bug fue reportado por QA con pasos y evidencia.
- **In Progress**: el desarrollador está trabajando en la corrección.
- **Fixed**: el dev informa el fix indicando el build (ej. "Fix en build 1.3").
- **Retesting**: QA reejecuta el caso de prueba vinculado sobre el build indicado.
- **Closed**: el fix fue verificado ("Verificado en build 1.3").
- **Reopened**: el retest sigue fallando; se reabre con evidencia nueva.

## 8. Entregables

| Entregable | Ubicación |
|---|---|
| Análisis de requerimientos | `docs/analisis-requerimientos.xlsx` |
| Matriz de trazabilidad | `docs/matriz-trazabilidad.xlsx` |
| Plan de testing | `docs/plan-de-testing.md` |
| Daily reports | `docs/daily-reports.md` |
| Matriz de casos de prueba con resultados | `casos-de-prueba/matriz-de-prueba.xlsx` |
| Bug reports detallados | `bugs/bug-reports-detallados.md` |
| Resumen de bugs | `bugs/reporte-bugs-resumen.xlsx` |
| Evidencias | `evidencias/` |
| Informe final | `informe-final/informe-final-qa-shopnow.pdf` |

## 9. Cronograma

| Sprint | Semana | Foco | Horas |
|---|---|---|---|
| Sprint 1 | 24–30/08/2026 | Análisis de requerimientos, matriz de trazabilidad, setup de Jira | 8–10 h |
| Sprint 2 | 31/08–06/09/2026 | Diseño de los 36 casos de prueba | 10–12 h |
| Sprint 3 | 07–13/09/2026 | Ejecución, evidencias y actualización de la matriz | 12–15 h |
| Sprint 4 | 14–18/09/2026 | Reporte de defectos, informe final y portafolio | 12–14 h |

## 10. Riesgos del proyecto de testing

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| No contar con dispositivo iOS para Safari mobile | Alta | Medio | Documentar el caso como *Blocked* y escalar a la QA Lead para gestionar un laboratorio de dispositivos |
| Demoras en el envío de emails que bloqueen la verificación | Media | Alto | Definir una ventana de espera máxima y documentar el bloqueo (ocurrió: BUG-003 bloqueó CP-016) |
| Fixes que lleguen sin build identificado | Media | Medio | Exigir el número de build en el comentario de *Fixed* antes de retestear |
| Brechas de cobertura en requerimientos sin casos | Media | Alto | Revisar la matriz de trazabilidad al cerrar cada fase (se detectó y corrigió: CP-033 a CP-036) |
