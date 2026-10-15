# Spec-Driven Development con IA — repositorio de ejemplo

Material de la charla **"Spec-Driven Development con IA: del PRD al código sin perder el rumbo"**, presentada en GitHub Dev Days Venezuela por **Tecnochui**.

La idea en una línea: **la IA escribe código rápido, pero necesita contexto estructurado.** En vez de un prompt cada vez más largo, versionas especificaciones en el repositorio y se las das a la IA que uses. La metodología es **agnóstica a la herramienta**: sirve igual con Claude, ChatGPT, DeepSeek, Gemini, Antigravity, Cursor, GitHub Copilot o cualquier otra.

## Qué hay en este repositorio

```
spec-driven-ejemplo/
├── README.md                     ← estás aquí
├── AGENTS.md                     ← reglas que cualquier IA debe leer primero
├── CHECKLIST.md                  ← las 3 preguntas para aplicarlo mañana
├── plantillas/
│   ├── PRD.md                    ← plantilla de requisitos (Fase 1)
│   ├── SSD.md                    ← plantilla de diseño (Fase 2)
│   └── SPEC.md                   ← plantilla de spec y tareas (Fase 3)
├── docs/
│   ├── prd/PRD-001-gestor-de-tareas.md
│   ├── design/SSD-001-gestor-de-tareas.md
│   └── specs/SPEC-001-crear-tarea.md
├── src/                          ← aquí vive el código generado
├── tests/                        ← aquí viven los tests
└── .github/
    ├── pull_request_template.md  ← obliga a enlazar la spec en cada PR
    └── workflows/spec-gate.yml  ← el gate de gobernanza ligera
```

El **ejemplo** (un gestor de tareas con API REST) es deliberadamente pequeño. Sirve para ver cómo se conectan los documentos entre sí: la spec referencia el PRD y el diseño, y el PR referencia la spec.

## El flujo en 6 fases

| Fase | Qué haces | Dónde queda |
|---|---|---|
| 1. Especificación (PRD) | Con tu IA, generas requisitos de alto nivel y por módulo | `docs/prd/` |
| 2. Diseño (SSD) | A partir del PRD, generas arquitectura, seguridad y modelo de datos | `docs/design/` |
| 3. Specs y tareas | Specs de implementación que referencian PRD y diseño, con tareas y criterios de aceptación | `docs/specs/` |
| 4. Implementación y QA | La IA implementa **una tarea**, genera tests (casos de uso y edge cases) y revisa su propio código | `src/`, `tests/` |
| 5. Validación y cierre | Revisión humana enfocada en seguridad y alineación con la spec; el PR enlaza la spec | Pull Request |
| 6. Repo como fuente de verdad | Todo el contexto vive en GitHub; cualquier IA puede continuar mañana | Todo el repo |

## Cómo darle este contexto a tu IA

El contenido es el mismo; lo que cambia es la forma de entregarlo.

| Herramienta | Cómo consume el contexto |
|---|---|
| Claude | Projects, archivos adjuntos, MCP |
| ChatGPT | Archivos, GPTs personalizados, Projects |
| DeepSeek | Carga de archivos y contexto largo |
| Gemini | Integración con Drive y documentos |
| Cursor / Antigravity / Copilot | Leen el repositorio directamente |

Regla práctica: pídele a tu IA que lea primero `AGENTS.md`, luego el PRD, el diseño y, por último, **una sola spec**, y que implemente **una sola tarea** a la vez.

## El gate de GitHub Actions

`.github/workflows/spec-gate.yml` corre en cada Pull Request y comprueba dos cosas:

1. Que la descripción del PR enlaza a una spec con el formato `docs/specs/SPEC-NNN-nombre.md`.
2. Que ese archivo existe en el repositorio.

No distingue qué herramienta generó el código: distingue **procesos**. Si un PR realmente no necesita spec (por ejemplo, un cambio de documentación), se le puede poner la etiqueta `sin-spec` y el gate se salta; así la excepción queda visible y auditable.

> **Referencia:** este enfoque se alinea de forma ligera con el NIST AI RMF (marco de gestión de riesgos de IA): la gobernanza no es un PDF, es un workflow que deja evidencia automatizada en cada PR.

## Cómo empezar en tu proyecto

1. Copia `plantillas/`, `AGENTS.md`, `.github/` y `CHECKLIST.md` a tu repositorio.
2. Crea tu `docs/prd/PRD-001-...md` desde `plantillas/PRD.md` (puedes pedirle a tu IA que lo redacte contigo y luego lo revisas tú).
3. Genera el diseño en `docs/design/` y revisa especialmente la parte de seguridad.
4. Escribe una spec por cada funcionalidad en `docs/specs/`, con criterios de aceptación verificables.
5. Pide la implementación tarea por tarea y abre un PR por spec, enlazándola en la descripción.
6. Activa el gate y ajusta la expresión regular si usas otra convención de nombres.

## Notas

- Los archivos de ejemplo son **ilustrativos**: adáptalos a tu proyecto, no los copies tal cual.
- Si tu herramienta de IA usa un archivo de instrucciones propio (por ejemplo `CLAUDE.md`, `.github/copilot-instructions.md` o reglas de Cursor), puedes dejarlo apuntando a `AGENTS.md` para mantener una sola fuente de verdad.
- Elige la licencia que prefieras antes de publicar el repositorio.
