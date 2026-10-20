# ADR 0002: Commits, push y trazabilidad

* **Estado:** Propuesta
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

La interacción de agentes con Git requiere límites estrictos para evitar sobrescribir historial, publicar cambios rotos o realizar alteraciones masivas sin trazabilidad.

## Decisión

1. **Sin push autónomo:** El agente no ejecuta `git push` salvo orden explícita del usuario.
2. **Comandos prohibidos:** Prohibido el uso de `--force`, `--amend` o `rebase` sobre commits ya publicados, así como el uso de `--no-verify`.
3. **Un cambio, un commit:** Flujo basado en Conventional Commits. Cada commit incluye sus propios tests. Nunca se commitea en estado rojo.
4. **Protección de rama principal:** La rama `main` se mantiene protegida. Cambios vía PR con checks verdes requeridos. Merge commit o rebase merge; squash deshabilitado.

## Mecanismo de control

1. Hook local `pre-push` que ejecute los mismos linters y tests que el CI.
2. Integración de `commitlint` en el flujo de CI.
3. Reglas de protección de la rama `main` aplicadas en GitHub.
4. `CODEOWNERS` protegiendo workflows de CI y scripts de gobernanza.

## Evidencia de uso

Probado operando en modo local controlando los cambios mediante revisión manual y ejecución local de tests antes de integrar a la rama principal.

## Consecuencias

### Positivas
* Historial limpio, auditable y atómico.
* Imposibilidad de desplegar código que rompa tests.

### Negativas
* Incrementa el tiempo de feedback local si los tests tardan en correr en el hook.