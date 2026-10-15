# PRD-001 — Gestor de tareas (ejemplo)

> Ejemplo ilustrativo y deliberadamente pequeño para mostrar cómo se conectan PRD, diseño y specs. Adáptalo a tu proyecto.

| Campo | Valor |
|---|---|
| Estado | Aprobado |
| Autor | Tecnochui |
| Diseño relacionado | `docs/design/SSD-001-gestor-de-tareas.md` |

## 1. Contexto y problema

Equipos pequeños y freelancers llevan sus pendientes en chats y hojas de cálculo sueltas, y pierden el rastro de qué está hecho y qué no. Se necesita una API sencilla para que cada persona gestione sus propias tareas.

## 2. Objetivos

- O-01: Que una persona autenticada pueda crear, consultar, actualizar el estado y eliminar sus tareas.
- O-02: Que los datos de una persona nunca sean visibles para otra.

## 3. Fuera de alcance

- Tareas compartidas entre usuarios.
- Notificaciones, recordatorios y fechas límite.
- Interfaz gráfica (esta versión es solo API).

## 4. Usuarios y escenarios

| Usuario | Qué necesita lograr |
|---|---|
| Persona autenticada | Anotar una tarea, ver su lista, marcarla como hecha y borrarla |

## 5. Requisitos funcionales

| ID | Requisito | Prioridad |
|---|---|---|
| RF-01 | Crear una tarea con título (obligatorio, máximo 120 caracteres) y descripción (opcional, máximo 2000 caracteres). El estado inicial es `pendiente`. | Alta |
| RF-02 | Listar las tareas propias, con filtro opcional por estado. | Alta |
| RF-03 | Cambiar el estado de una tarea propia entre `pendiente`, `en_progreso` y `hecha`. | Media |
| RF-04 | Eliminar una tarea propia. | Media |

## 6. Requisitos no funcionales

| ID | Categoría | Requisito |
|---|---|---|
| RNF-01 | Seguridad | Todos los endpoints exigen autenticación. Una persona solo puede ver y modificar sus propias tareas. |
| RNF-02 | Validación de datos | Toda entrada se valida en el servidor; los datos inválidos se rechazan con un error claro. |
| RNF-03 | Manejo de errores | Los errores no revelan detalles internos (trazas, consultas, rutas del servidor). |
| RNF-04 | Calidad | Cada requisito funcional tiene tests automáticos, incluidos casos borde y casos de acceso no autorizado. |

## 7. Métricas de éxito

- 100 % de los requisitos funcionales con tests que pasan en cada PR.
- 0 PRs fusionados sin enlace a una spec.

## 8. Riesgos y supuestos

| Riesgo o supuesto | Mitigación |
|---|---|
| La IA implementa acceso a tareas sin comprobar el dueño | RNF-01 y un test de acceso no autorizado en cada spec |
| Se asume que existe un mecanismo de autenticación | El diseño lo define; la spec indica cómo se usa |

## 9. Preguntas abiertas

- [ ] ¿Se necesitará paginación en el listado? (por ahora, fuera de alcance)
