# Checklist de 3 preguntas

Responde sí o no. Cada "no" es tu próximo paso.

1. **¿Tu proyecto tiene un PRD versionado en el repositorio?**
   - Sí → está en `docs/prd/` y cualquier IA puede leerlo.
   - No → empieza con `plantillas/PRD.md`.

2. **¿Tus especificaciones tienen criterios de aceptación claros?**
   - Sí → cada tarea se puede verificar con un "cumple / no cumple".
   - No → reescribe los criterios hasta que dos personas lleguen a la misma conclusión. Usa `plantillas/SPEC.md`.

3. **¿Tu pipeline verifica que el código se alinea con las specs?**
   - Sí → el gate corre en cada PR y deja evidencia.
   - No → copia `.github/workflows/spec-gate.yml` y `.github/pull_request_template.md`.

## Antes de abrir un PR

- [ ] El PR enlaza a la spec que lo originó.
- [ ] Revisé la seguridad: validación de entrada, autenticación y autorización.
- [ ] Los criterios de aceptación de la spec están cumplidos o documentados como pendientes.
- [ ] Hay tests para los casos de uso y los casos borde.
- [ ] Si la IA propuso cambiar el diseño, ese cambio está en `docs/design/` y no solo en el código.
