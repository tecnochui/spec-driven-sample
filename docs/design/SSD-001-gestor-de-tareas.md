# SSD-001 — Diseño: gestor de tareas (ejemplo)

| Campo | Valor |
|---|---|
| Estado | Aprobado |
| PRD relacionado | `docs/prd/PRD-001-gestor-de-tareas.md` |
| Autor | Tecnochui |

## 1. Visión general de la arquitectura

API REST sobre una base de datos relacional. El lenguaje y el framework se eligen por proyecto; este diseño no los fija.

```
[Cliente] → [API REST] → [Base de datos relacional]
               │
               └─ middleware de autenticación (en todas las rutas)
```

## 2. Decisiones técnicas

| ID | Decisión | Motivo | Alternativas descartadas |
|---|---|---|---|
| D-01 | Base de datos relacional | Las tareas pertenecen a un usuario y tienen un estado acotado; el modelo es simple y relacional | Base documental |
| D-02 | Autenticación mediante token en la cabecera `Authorization: Bearer <token>` | Mantiene la API sin estado | Sesiones en servidor |
| D-03 | El identificador del dueño sale **siempre del token**, nunca del cuerpo de la petición | Evita que alguien cree o lea tareas a nombre de otro | Enviar `usuario_id` en el cuerpo |

## 3. Modelo de datos

| Entidad | Campos | Reglas |
|---|---|---|
| `usuarios` | `id`, `email` | `email` único |
| `tareas` | `id`, `usuario_id`, `titulo`, `descripcion`, `estado`, `creada_en`, `actualizada_en` | `titulo` obligatorio, máx. 120; `descripcion` opcional, máx. 2000; `estado` ∈ {`pendiente`, `en_progreso`, `hecha`}; `usuario_id` referencia a `usuarios` |

## 4. Interfaces

| Interfaz | Entrada | Salida | Errores |
|---|---|---|---|
| `POST /tareas` | `titulo`, `descripcion?` | `201` + tarea creada | `400` datos inválidos, `401` sin autenticar |
| `GET /tareas?estado=` | filtro opcional | `200` + lista de tareas propias | `400` estado inválido, `401` |
| `PATCH /tareas/{id}` | `estado` | `200` + tarea actualizada | `400`, `401`, `404` si no existe o no es del usuario |
| `DELETE /tareas/{id}` | — | `204` | `401`, `404` si no existe o no es del usuario |

## 5. Seguridad

| Tema | Decisión | Requisito PRD |
|---|---|---|
| Autenticación | Token obligatorio en todos los endpoints (D-02) | RNF-01 |
| Autorización | Toda consulta filtra por el `usuario_id` del token (D-03). Si la tarea es de otra persona se responde `404`, no `403`, para no revelar que existe | RNF-01 |
| Validación de entrada | Longitudes, tipos y valores permitidos validados en el servidor antes de tocar la base de datos | RNF-02 |
| Manejo de errores | Mensajes genéricos al cliente; el detalle técnico solo en los registros del servidor | RNF-03 |
| Acceso a datos | Consultas parametrizadas; nunca concatenar entrada del usuario en SQL | RNF-02 |

## 6. Trazabilidad

| Requisito PRD | Sección de este diseño |
|---|---|
| RF-01 | §3, §4 (`POST /tareas`) |
| RF-02 | §4 (`GET /tareas`) |
| RF-03 | §3 (`estado`), §4 (`PATCH`) |
| RF-04 | §4 (`DELETE`) |
| RNF-01 | §2 (D-02, D-03), §5 |
| RNF-02 | §3, §5 |
| RNF-03 | §5 |

## 7. Preguntas abiertas

- [ ] ¿Cómo se emiten y se renuevan los tokens? (fuera del alcance de este ejemplo)
