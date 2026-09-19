# Guion del Sprint Review — ShopNow QA

> Presentación de cierre del Sprint 4 ante la PO, el Scrum Master, la QA Lead y el equipo de desarrollo.
> Duración prevista: 12 minutos de exposición + 3 minutos de preguntas.

| # | Diapositiva | Mensaje central | Tiempo |
|---|---|---|---|
| 1 | Portada | Vengo a contar en qué estado está el módulo y si podemos salir a producción | 0:30 |
| 2 | Lo que vamos a ver | Recorrido de la presentación; preguntas al final | 0:30 |
| 3 | Alcance | Qué se testeó y qué quedó explícitamente fuera | 1:00 |
| 4 | Cuatro sprints | El ciclo completo de QA, con sus entregables por sprint | 1:00 |
| 5 | Diseño de pruebas | Técnicas aplicadas y la brecha de cobertura detectada antes de ejecutar | 1:30 |
| 6 | Métricas | 36 casos, 27 Passed, 7 Failed, 2 Blocked; las fallas no están repartidas | 1:30 |
| 7 | Defectos por severidad | 8 defectos y su estado real en Jira al cierre del sprint | 1:00 |
| 8 | BUG-002 | El defecto crítico: en Firefox nadie puede registrarse | 1:30 |
| 9 | Los tres mayores | Mobile, contraseña visible y email de bienvenida | 1:30 |
| 10 | Cobertura | 100 % de requerimientos verificados; dos verificaciones parciales | 1:00 |
| 11 | NO-GO | La recomendación, dicha con calma | 0:20 |
| 12 | Cuatro datos | Por qué NO-GO, con evidencia y no con opinión | 2:00 |
| 13 | Condiciones para GO | La lista corta y concreta de lo que falta | 1:00 |
| 14 | Próximos pasos | Quién hace qué en el Sprint 5 | 1:30 |
| 15 | Cierre | Dónde está documentado todo + preguntas | 2:00 |

## Preguntas probables y cómo responderlas

**¿Cuándo podríamos salir a producción?**  
Un sprint de corrección para los cuatro bloqueantes, más dos días de regresión sobre los 36 casos. La fecha depende de cuándo lleguen los fixes, no del testing.

**¿Por qué no automatizaron las pruebas?**  
La automatización quedó fuera del alcance acordado para este ciclo. Con los 36 casos ya documentados, los 20 de regresión son los mejores candidatos para automatizar en el próximo proyecto.

**¿El NO-GO es definitivo?**  
No. Es una recomendación técnica con condiciones explícitas: cuatro defectos corregidos y verificados, un ciclo de regresión con 95 % de éxito y Safari mobile cubierto o su riesgo aceptado formalmente.

**¿Por qué BUG-004 es S2 y no S1 si bloquea mobile?**  
La severidad mide el impacto técnico y existe un camino alternativo: el usuario puede editar su perfil desde desktop. La prioridad, que la define la PO por impacto de negocio, sí es P1.

**¿Los dos casos bloqueados no deberían contarse como fallidos?**  
No: un caso bloqueado no se ejecutó, no falló. Contarlo como fallido inventaría un defecto que no observamos. Por eso se reportan aparte y con su causa.

**¿Cómo sabemos que BUG-002 no es un problema de tu máquina?**  
Se reprodujo en dos equipos distintos, con perfil limpio de Firefox, y falla el 100 % de las veces. La evidencia incluye la consola y la pestaña Network sin petición a /register.

---

El deck completo está en `presentacion/sprint-review-qa-shopnow.pdf`. Las notas del orador de cada diapositiva contienen estas mismas indicaciones.
