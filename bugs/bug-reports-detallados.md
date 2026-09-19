# Bug Reports — ShopNow S.A. | Módulo Registro y Perfil

> 8 defectos documentados en Jira (proyecto *ShopNow QA — Registro y Perfil*) con formato estándar de industria.
> Reportados por: Jeisson Marín Uribe Luis — QA Tester Junior · Sprint 4 · Entorno: staging (simulado, proyecto educativo).


## Índice

| ID | Título | Severidad | Prioridad | Estado | Caso vinculado |
|---|---|---|---|---|---|
| **BUG-001** | [Registro] El campo contraseña muestra el texto en claro sin interacción del usuario | S2 - Mayor | P2 - Alta | Closed | CP-010 |
| **BUG-002** | [Registro] En Firefox el botón 'Crear cuenta' no responde al clic | S1 - Crítico | P1 - Crítica | Closed | CP-029 |
| **BUG-003** | [Registro] El email de bienvenida llega a los 15 minutos | S2 - Mayor | P2 - Alta | Fixed | CP-015 (bloquea CP-016) |
| **BUG-004** | [Perfil] En mobile 375px el botón 'Guardar cambios' queda fuera del viewport | S2 - Mayor | P1 - Crítica | Reopened | CP-031 |
| **BUG-005** | [Registro] El mensaje de error por email duplicado dice 'Error inesperado' | S3 - Menor | P3 - Media | Closed | CP-005 |
| **BUG-006** | [Perfil] El sistema acepta fechas de nacimiento futuras sin mostrar error | S3 - Menor | P3 - Media | In Progress | CP-021 |
| **BUG-007** | [Foto de perfil] No se muestra la previsualización de la imagen antes de confirmar la carga | S3 - Menor | P4 - Baja | New | CP-025 |
| **BUG-008** | [Registro] El placeholder del campo 'Apellido' dice 'Ingresa tu nombre' | S4 - Trivial | P4 - Baja | New | CP-001 |


---

## BUG-001 — [Registro] El campo contraseña muestra el texto en claro sin interacción del usuario

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-001 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P2 - Alta |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RNF-04 |
| **Caso de prueba vinculado** | CP-010 |
| **Evidencia** | `evidencias/BUG-001-contrasena-visible-chrome.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- El usuario no está logueado
- Navegador sin cache (modo incógnito)

**Pasos para reproducir**

1. Ingresar a https://staging.shopnow.com.ar/registro
2. Hacer clic en el campo 'Contraseña'
3. Escribir cualquier contraseña

**Resultado obtenido**

El texto de la contraseña se muestra en claro desde el primer carácter, sin necesidad de hacer clic en el icono del ojo. RNF-04 violado.

**Resultado esperado**

Los caracteres deben mostrarse como '......' por defecto. Solo al hacer clic en el icono del ojo deben mostrarse en claro.

**Impacto en el negocio**

Exposición visual de credenciales ante terceros (shoulder surfing). Riesgo reputacional y de cumplimiento para una plataforma con 350.000 usuarios.

**Ciclo de vida del defecto**

```
New
-> In Progress
-> Fixed (comentario: 'Fix en build 1.3')
-> Retesting (CP-010 reejecutado)
-> Closed (comentario: 'Verificado en build 1.3')
```

---

## BUG-002 — [Registro] En Firefox el botón 'Crear cuenta' no responde al clic

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-002 |
| **Entorno** | Staging | Firefox 121 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S1 - Crítico |
| **Prioridad** | P1 - Crítica |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RNF-02 |
| **Caso de prueba vinculado** | CP-029 |
| **Evidencia** | `evidencias/BUG-002-boton-crear-cuenta-firefox.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- El usuario no está logueado
- Formulario completo y válido
- T&C marcado

**Pasos para reproducir**

1. Ingresar a https://staging.shopnow.com.ar/registro en Firefox
2. Completar todos los campos con datos válidos
3. Marcar el checkbox de T&C
4. Hacer clic en 'Crear cuenta'
5. Abrir DevTools (F12) > Console y Network

**Resultado obtenido**

El botón no ejecuta ninguna acción. No se genera petición a /register en la pestaña Network y la consola muestra 'Uncaught TypeError: e.submitForm is not a function'. Ningún usuario puede registrarse desde Firefox.

**Resultado esperado**

La cuenta debe crearse igual que en Chrome y redirigir al panel de perfil.

**Impacto en el negocio**

Bloqueo total del alta de usuarios en Firefox (aprox. 8-10% del tráfico del sitio según la analítica del PO). Pérdida directa de conversión de nuevos usuarios.

**Ciclo de vida del defecto**

```
New
-> In Progress
-> Fixed (comentario: 'Fix en build 1.3')
-> Retesting (CP-029 reejecutado en Firefox 121)
-> Closed (comentario: 'Verificado en build 1.3')
```

---

## BUG-003 — [Registro] El email de bienvenida llega a los 15 minutos

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-003 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P2 - Alta |
| **Estado actual** | Fixed |
| **Requerimiento afectado** | RF-06 |
| **Caso de prueba vinculado** | CP-015 (bloquea CP-016) |
| **Evidencia** | `evidencias/BUG-003-email-bienvenida-demora.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- Registro completado con éxito
- Casilla de correo accesible

**Pasos para reproducir**

1. Completar el registro con un email válido
2. Abrir la casilla del email registrado
3. Cronometrar el tiempo hasta la recepción
4. Repetir 3 veces

**Resultado obtenido**

El email de bienvenida llega a los 15 minutos aproximadamente (14:12, 15:03 y 15:41 en las tres mediciones). RF-06 se cumple con demora fuera del SLA definido.

**Resultado esperado**

El email de bienvenida debe llegar en menos de 2 minutos desde el alta.

**Impacto en el negocio**

El usuario nuevo no puede validar su cuenta ni acceder al link de bienvenida en su primera sesión. Aumenta el abandono en el onboarding y genera tickets de soporte.

**Ciclo de vida del defecto**

```
New
-> In Progress
-> Fixed (comentario: 'Cola de envío reconfigurada en build 1.4 - pendiente de retest')
```

---

## BUG-004 — [Perfil] En mobile 375px el botón 'Guardar cambios' queda fuera del viewport

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-004 |
| **Entorno** | Staging | Chrome 120 (modo responsive 375x667) | Windows 11 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P1 - Crítica |
| **Estado actual** | Reopened |
| **Requerimiento afectado** | RNF-03 |
| **Caso de prueba vinculado** | CP-031 |
| **Evidencia** | `evidencias/BUG-004-guardar-fuera-viewport-mobile.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- Usuario logueado
- DevTools en modo responsive 375px

**Pasos para reproducir**

1. Abrir https://staging.shopnow.com.ar/perfil con DevTools en 375px
2. Editar cualquier dato personal
3. Intentar presionar 'Guardar cambios'

**Resultado obtenido**

El botón queda por debajo del área visible y no se alcanza con scroll vertical; el contenedor tiene overflow oculto. El usuario no puede guardar cambios desde mobile.

**Resultado esperado**

Todos los controles deben ser visibles y operables en 375px, sin scroll horizontal ni recorte del contenedor.

**Impacto en el negocio**

Imposibilita la edición de perfil para el tráfico mobile, que representa la mayor parte de los usuarios de e-commerce en Argentina.

**Ciclo de vida del defecto**

```
New
-> In Progress
-> Fixed (comentario: 'Fix en build 1.3')
-> Retesting (CP-031 reejecutado)
-> Reopened (comentario: 'El botón sigue recortado en 375x667; se adjunta evidencia nueva BUG-004-retest-build13.png')
```

---

## BUG-005 — [Registro] El mensaje de error por email duplicado dice 'Error inesperado'

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-005 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P3 - Media |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RF-02 |
| **Caso de prueba vinculado** | CP-005 |
| **Evidencia** | `evidencias/BUG-005-mensaje-email-duplicado.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- Existe una cuenta previa registrada con el email de prueba

**Pasos para reproducir**

1. Ingresar a /registro
2. Completar el formulario usando un email ya registrado
3. Marcar T&C
4. Clic en 'Crear cuenta'

**Resultado obtenido**

Se muestra el mensaje genérico 'Error inesperado'. El usuario no sabe que el email ya existe ni que puede recuperar su contraseña.

**Resultado esperado**

Mensaje específico: 'Este email ya está registrado. Inicia sesión o recupera tu contraseña'.

**Impacto en el negocio**

Fricción en el alta y aumento de contactos a soporte. El usuario puede abandonar el registro creyendo que el sitio fallo.

**Ciclo de vida del defecto**

```
New
-> In Progress
-> Fixed (comentario: 'Fix en build 1.3')
-> Retesting (CP-005 reejecutado)
-> Closed (comentario: 'Verificado en build 1.3')
```

---

## BUG-006 — [Perfil] El sistema acepta fechas de nacimiento futuras sin mostrar error

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-006 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P3 - Media |
| **Estado actual** | In Progress |
| **Requerimiento afectado** | RF-07 |
| **Caso de prueba vinculado** | CP-021 |
| **Evidencia** | `evidencias/BUG-006-fecha-nacimiento-futura.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- Usuario logueado en /perfil

**Pasos para reproducir**

1. Ingresar a /perfil
2. Seleccionar la fecha de nacimiento 15/01/2030
3. Guardar cambios
4. Recargar la página

**Resultado obtenido**

La fecha futura se guarda y persiste tras recargar, sin ninguna validación ni mensaje de error. RF-07 incumplido.

**Resultado esperado**

El sistema debe rechazar fechas posteriores a la fecha actual con el mensaje 'La fecha de nacimiento no puede ser futura'.

**Impacto en el negocio**

Datos demográficos inválidos en la base de usuarios; afecta segmentación de campañas y validaciones de edad mínima.

**Ciclo de vida del defecto**

```
New
-> In Progress (asignado al equipo backend, build 1.4)
```

---

## BUG-007 — [Foto de perfil] No se muestra la previsualización de la imagen antes de confirmar la carga

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-007 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P4 - Baja |
| **Estado actual** | New |
| **Requerimiento afectado** | RF-09 |
| **Caso de prueba vinculado** | CP-025 |
| **Evidencia** | `evidencias/BUG-007-sin-preview-foto.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- Usuario logueado en /perfil
- Archivo JPG válido menor a 2 MB disponible

**Pasos para reproducir**

1. Ingresar a /perfil
2. Clic en 'Cambiar foto'
3. Seleccionar un JPG de 1,2 MB
4. Observar el área de previsualización antes de confirmar

**Resultado obtenido**

No se muestra ninguna previsualización; el área queda vacía hasta que la carga se confirma y la página se refresca.

**Resultado esperado**

Debe mostrarse una miniatura de la imagen seleccionada antes de confirmar, para permitir cancelar si es la foto equivocada.

**Impacto en el negocio**

El usuario sube la foto a ciegas y debe repetir el proceso si se equivoca. Impacto bajo en negocio, alto en experiencia.

**Ciclo de vida del defecto**

```
New (reportado y priorizado para el backlog del Sprint 5)
```

---

## BUG-008 — [Registro] El placeholder del campo 'Apellido' dice 'Ingresa tu nombre'

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-008 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S4 - Trivial |
| **Prioridad** | P4 - Baja |
| **Estado actual** | New |
| **Requerimiento afectado** | RF-07 |
| **Caso de prueba vinculado** | CP-001 |
| **Evidencia** | `evidencias/BUG-008-placeholder-apellido.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 15/09/2026 |

**Precondiciones**

- El usuario no está logueado

**Pasos para reproducir**

1. Ingresar a https://staging.shopnow.com.ar/registro
2. Observar el texto placeholder del campo 'Apellido'

**Resultado obtenido**

El placeholder del campo 'Apellido' muestra el texto 'Ingresa tu nombre'.

**Resultado esperado**

El placeholder debe decir 'Ingresa tu apellido'.

**Impacto en el negocio**

Confusión menor en el formulario de alta. No bloquea el flujo pero afecta la percepción de calidad del producto.

**Ciclo de vida del defecto**

```
New (reportado y priorizado para el backlog del Sprint 5)
```

---

## Resumen por severidad

| Severidad | Cantidad | Bugs |
|---|---|---|
| S1 — Crítico | 1 | BUG-002 |
| S2 — Mayor | 3 | BUG-001, BUG-003, BUG-004 |
| S3 — Menor | 3 | BUG-005, BUG-006, BUG-007 |
| S4 — Trivial | 1 | BUG-008 |

**Bloqueantes para producción:** BUG-002 (S1) y los tres S2 (BUG-001, BUG-003, BUG-004). Ver la justificación completa en `informe-final/informe-final-qa-shopnow.pdf`.
