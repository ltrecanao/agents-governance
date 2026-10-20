# ADR 0001: Roles de AGENTS.md y Skills

* **Estado:** Propuesta
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

Sin una separación clara de responsabilidades, la información sobre cómo debe actuar un agente termina duplicada, desactualizada o saturando la ventana de contexto del modelo con reglas irrelevantes para la tarea puntual.

## Decisión

Se establece una división estricta por persistencia y frecuencia de uso:

* **`AGENTS.md` (Contexto permanente):** Reglas, arquitectura y restricciones que el agente siempre debe conocer en el repositorio. Carga fija en cada sesión. Debe ser corto y acotado.
* **Skills (Procedimientos a demanda):** Guías, herramientas y procedimientos para tareas específicas. Se cargan únicamente cuando la tarea lo requiere y se liberan al terminar.

## Mecanismo de control

1. Linter en CI que valide el límite de tamaño máximo de `AGENTS.md`.
2. Linter que exija el frontmatter estructurado (`name`, `description`) en cada archivo de skill.

## Evidencia de uso

Probado delimitando reglas globales en `AGENTS.md` y aislando tareas específicas en skills a demanda, logrando menor consumo de tokens y mayor precisión.

## Consecuencias

### Positivas
* Ahorro de tokens en el prompt del agente.
* Aislamiento de responsabilidades por procedimiento.

### Negativas
* Requiere mantener actualizado el frontmatter de las skills para su correcto descubrimiento.