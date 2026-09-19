# Evidencias de testing — ShopNow S.A.

Capturas de la ejecución de cada caso de prueba y de cada defecto reportado.

> **Nota sobre el entorno.** `staging.shopnow.com.ar` es un entorno **ficticio** creado con fines educativos (proyecto formativo *Guía de proyectos para QA Tester* — Talently Lab). Las capturas de esta carpeta son **evidencias simuladas** que reproducen el formato, la nomenclatura y el contenido que tendría una evidencia real: caso o bug, entorno, pasos ejecutados, resultado esperado y resultado obtenido.

## Convención de nombres

```
CP-XXX-descripcion-navegador.png     → evidencia de un caso de prueba
BUG-XXX-descripcion-navegador.png    → evidencia de un defecto
```

Cada archivo se nombra en el momento de la captura, nunca al final del sprint.

## Evidencias de casos de prueba

| Caso | Estado | Archivo |
|---|---|---|
| CP-001 | Passed | `CP-001-registro-exitoso-chrome.png` |
| CP-002 | Passed | `CP-002-email-sin-arroba-chrome.png` |
| CP-003 | Passed | `CP-003-email-sin-dominio-chrome.png` |
| CP-004 | Passed | `CP-004-email-valido-chrome.png` |
| CP-005 | Failed | `CP-005-email-duplicado-chrome.png` |
| CP-006 | Passed | `CP-006-email-vacio-chrome.png` |
| CP-007 | Passed | `CP-007-password-7-caracteres-chrome.png` |
| CP-008 | Passed | `CP-008-password-sin-mayuscula-chrome.png` |
| CP-009 | Passed | `CP-009-password-sin-numero-chrome.png` |
| CP-010 | Failed | `CP-010-password-8-caracteres-chrome.png` |
| CP-011 | Passed | `CP-011-confirmacion-distinta-chrome.png` |
| CP-012 | Passed | `CP-012-password-vacio-chrome.png` |
| CP-013 | Passed | `CP-013-tyc-sin-marcar-chrome.png` |
| CP-014 | Passed | `CP-014-tyc-marcado-chrome.png` |
| CP-015 | Failed | `CP-015-email-bienvenida-demora-chrome.png` |
| CP-016 | Blocked | `CP-016-bloqueado-por-BUG-003.png` |
| CP-017 | Passed | `CP-017-editar-nombre-chrome.png` |
| CP-018 | Passed | `CP-018-nombre-vacio-chrome.png` |
| CP-019 | Passed | `CP-019-telefono-9-digitos-chrome.png` |
| CP-020 | Passed | `CP-020-telefono-10-digitos-chrome.png` |
| CP-021 | Failed | `CP-021-fecha-futura-chrome.png` |
| CP-022 | Passed | `CP-022-cambio-password-ok-chrome.png` |
| CP-023 | Passed | `CP-023-password-actual-incorrecta-chrome.png` |
| CP-024 | Passed | `CP-024-nueva-password-debil-chrome.png` |
| CP-025 | Failed | `CP-025-foto-jpg-valida-chrome.png` |
| CP-026 | Passed | `CP-026-foto-png-2.1mb-chrome.png` |
| CP-027 | Passed | `CP-027-foto-formato-pdf-chrome.png` |
| CP-028 | Passed | `CP-028-foto-jpg-2mb-chrome.png` |
| CP-029 | Failed | `CP-029-registro-firefox.png` |
| CP-030 | Blocked | `CP-030-bloqueado-sin-dispositivo-ios.png` |
| CP-031 | Failed | `CP-031-responsive-375px-chrome.png` |
| CP-032 | Passed | `CP-032-responsive-768px-chrome.png` |
| CP-033 | Passed | `CP-033-cinco-direcciones-chrome.png` |
| CP-034 | Passed | `CP-034-sexta-direccion-chrome.png` |
| CP-035 | Passed | `CP-035-direccion-principal-unica-chrome.png` |
| CP-036 | Passed | `CP-036-tiempo-carga-registro-chrome.png` |

## Evidencias de defectos

| Bug | Severidad | Archivo |
|---|---|---|
| BUG-001 | S2 - Mayor | `BUG-001-contrasena-visible-chrome.png` |
| BUG-002 | S1 - Crítico | `BUG-002-boton-crear-cuenta-firefox.png` |
| BUG-003 | S2 - Mayor | `BUG-003-email-bienvenida-demora.png` |
| BUG-004 | S2 - Mayor | `BUG-004-guardar-fuera-viewport-mobile.png` |
| BUG-005 | S3 - Menor | `BUG-005-mensaje-email-duplicado.png` |
| BUG-006 | S3 - Menor | `BUG-006-fecha-nacimiento-futura.png` |
| BUG-007 | S3 - Menor | `BUG-007-sin-preview-foto.png` |
| BUG-008 | S4 - Trivial | `BUG-008-placeholder-apellido.png` |
| BUG-004 | S2 - Mayor | `BUG-004-retest-build13.png` (evidencia del retest que motivó la reapertura) |

**Total: 45 evidencias.**
