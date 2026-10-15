# SPEC-001 — Crear tarea (ejemplo)

| Campo | Valor |
|---|---|
| Estado | Lista para implementar |
| PRD | `docs/prd/PRD-001-gestor-de-tareas.md` → RF-01, RNF-01, RNF-02, RNF-03, RNF-04 |
| Diseño | `docs/design/SSD-001-gestor-de-tareas.md` → §2 (D-02, D-03), §3, §4 (`POST /tareas`), §5 |
| Autor | Tecnochui |

## 1. Objetivo

Que una persona autenticada pueda crear una tarea propia mediante `POST /tareas`.

## 2. Alcance

**Incluye:**
- El endpoint `POST /tareas`, su validación y el guardado en la tabla `tareas`.

**No incluye:**
- Listar, actualizar o eliminar tareas (otras specs).
- Emisión de tokens de autenticación.

## 3. Tareas

### T1 — Validar la entrada

**Descripción:** Validar el cuerpo de `POST /tareas` en el servidor antes de cualquier acceso a la base de datos.

**Criterios de aceptación:**
- [ ] Dado un cuerpo sin `titulo`, cuando se envía la petición, entonces responde `400` con un mensaje que indica que el título es obligatorio.
- [ ] Dado un `titulo` de más de 120 caracteres, cuando se envía, entonces responde `400`.
- [ ] Dada una `descripcion` de más de 2000 caracteres, cuando se envía, entonces responde `400`.
- [ ] Dado un `titulo` vacío o compuesto solo por espacios, cuando se envía, entonces responde `400`.

**Casos borde:**
- `titulo` con exactamente 120 caracteres (válido).
- `titulo` que no es texto (número, lista, objeto): `400`.
- Cuerpo ausente o que no es JSON válido: `400`.

### T2 — Crear y devolver la tarea

**Descripción:** Guardar la tarea con el dueño tomado del token y devolverla.

**Criterios de aceptación:**
- [ ] Dada una petición válida y autenticada, cuando se envía, entonces responde `201` con la tarea creada (`id`, `titulo`, `descripcion`, `estado`, `creada_en`).
- [ ] La tarea creada tiene estado `pendiente`.
- [ ] El `usuario_id` guardado es el del token, aunque el cuerpo incluya un `usuario_id` distinto (se ignora).
- [ ] Dada una petición sin token o con token inválido, entonces responde `401` y no se guarda nada.

**Casos borde:**
- Dos peticiones idénticas seguidas crean dos tareas distintas (no hay deduplicación en esta versión).
- Un error interno responde `500` con mensaje genérico, sin trazas ni detalles de la consulta.

## 4. Pruebas requeridas

| Tipo | Qué debe cubrir |
|---|---|
| Casos de uso | Creación exitosa con y sin descripción |
| Casos borde | Longitudes límite, tipos incorrectos, cuerpo inválido |
| Seguridad | Sin token (`401`), `usuario_id` falso en el cuerpo ignorado, error interno sin detalles |

## 5. Definición de terminado

- [ ] Todos los criterios de aceptación están cumplidos o documentados como pendientes.
- [ ] Los tests pasan.
- [ ] La revisión humana confirmó seguridad y alineación con el diseño.
- [ ] El PR enlaza a `docs/specs/SPEC-001-crear-tarea.md`.

## 6. Prompt sugerido para la IA

```
Lee AGENTS.md, docs/prd/PRD-001-gestor-de-tareas.md,
docs/design/SSD-001-gestor-de-tareas.md y docs/specs/SPEC-001-crear-tarea.md.
Implementa únicamente la tarea T1 en src/ y sus tests en tests/.
Al terminar, lista cada criterio de aceptación con su estado
y los supuestos que hiciste. No cambies el diseño.
```
