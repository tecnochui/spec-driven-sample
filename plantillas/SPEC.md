# SPEC-NNN — Nombre de la funcionalidad

| Campo | Valor |
|---|---|
| Estado | Borrador / Lista para implementar / Implementada |
| PRD | `docs/prd/PRD-NNN-nombre.md` → RF-.., RNF-.. |
| Diseño | `docs/design/SSD-NNN-nombre.md` → secciones .. |
| Autor | |

## 1. Objetivo

Una o dos frases: qué cambia para el usuario cuando esta spec esté implementada.

## 2. Alcance

**Incluye:**
- ...

**No incluye:**
- ...

## 3. Tareas

Cada tarea es pequeña (una sesión con la IA) y tiene criterios que se pueden marcar como cumplidos o no cumplidos.

### T1 — Título de la tarea

**Descripción:** ...

**Criterios de aceptación:**
- [ ] Dado ..., cuando ..., entonces ...
- [ ] Dado ..., cuando ..., entonces ...

**Casos borde:**
- ...

### T2 — Título de la tarea

...

## 4. Pruebas requeridas

| Tipo | Qué debe cubrir |
|---|---|
| Casos de uso | |
| Casos borde | |
| Seguridad | |

## 5. Definición de terminado

- [ ] Todos los criterios de aceptación están cumplidos o documentados como pendientes.
- [ ] Los tests pasan.
- [ ] La revisión humana confirmó seguridad y alineación con el diseño.
- [ ] El PR enlaza a esta spec.

## 6. Prompt sugerido para la IA

```
Lee AGENTS.md, el PRD, el diseño y esta spec.
Implementa únicamente la tarea T1.
Genera los tests de sus criterios de aceptación y casos borde.
Al terminar, lista cada criterio con su estado y los supuestos que hiciste.
```
