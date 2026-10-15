# AGENTS.md — Instrucciones para cualquier asistente de IA

Este repositorio sigue **Spec-Driven Development (SDD)**: las especificaciones son la fuente de verdad. Estas reglas aplican sin importar qué herramienta de IA estés usando.

## Orden de lectura

1. Este archivo.
2. `docs/prd/` — qué se construye y por qué.
3. `docs/design/` — arquitectura, seguridad y modelo de datos.
4. **La spec indicada en la tarea** dentro de `docs/specs/`.

## Reglas

1. **No implementes nada sin una spec.** Si la tarea no tiene spec, pídela o propón una antes de escribir código.
2. **Una tarea a la vez.** Implementa únicamente la tarea que se te pidió, tal como está descrita en la spec.
3. **Cumple los criterios de aceptación.** Si un criterio es ambiguo o contradice el diseño, detente y pregunta; no lo interpretes en silencio.
4. **Respeta el diseño.** No cambies el modelo de datos, la arquitectura ni las decisiones de seguridad por tu cuenta. Si crees que hay que cambiarlas, propón el cambio en `docs/design/` primero.
5. **Seguridad por defecto.** Valida toda entrada en el servidor, aplica autenticación y autorización según el diseño, y no expongas detalles internos en los errores.
6. **Escribe tests.** Cubre los criterios de aceptación y los casos borde de la spec, y coloca los tests en `tests/`.
7. **Revisa tu propio código** antes de entregarlo: compáralo contra cada criterio de aceptación y menciona cualquier criterio que no hayas podido cumplir.
8. **Deja trazabilidad.** En el resumen del cambio cita la spec (por ejemplo, `docs/specs/SPEC-001-crear-tarea.md`) y las tareas implementadas.

## Formato de entrega esperado

- Archivos modificados o creados, con una línea de explicación cada uno.
- Lista de criterios de aceptación con estado (cumplido / no cumplido / pendiente de decisión).
- Supuestos que hiciste y preguntas abiertas.

## Lo que NO debes hacer

- Inventar requisitos que no estén en el PRD o en la spec.
- Eliminar o debilitar validaciones o controles de seguridad para "hacer pasar" un test.
- Tocar archivos fuera del alcance de la spec sin avisar.
