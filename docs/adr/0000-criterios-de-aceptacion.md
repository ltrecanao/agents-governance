# ADR 0000: Criterios de aceptación de ADRs

* **Estado:** Aceptada
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

Para evitar que la gobernanza se transforme en documentación estática o prosa sin impacto real en el desarrollo diario, las decisiones de arquitectura (ADRs) deben contar con reglas estrictas de ciclo de vida e implementación.

## Decisión

Una ADR solo pasará al estado **Aceptada** si cumple simultáneamente con dos condiciones obligatorias:

1. **Evidencia de uso:** Demostración documentada de que el patrón fue probado previamente con resultados positivos, incluyendo al menos una línea explicativa sobre el entorno y el resultado obtenido.
2. **Mecanismo de control automatizable:** Implementación efectiva de un mecanismo que obligue su cumplimiento sin depender de la revisión humana (CI gates, hooks locales, linters, `CODEOWNERS` o reglas de protección de GitHub).

### Estados del índice

* **Aceptada:** Cumple con la evidencia de uso y el mecanismo de control está activo y verificado en CI/mecanismos del repo.
* **Propuesta:** Automatizable y con evidencia de uso, pero el mecanismo de control técnico aún no está implementado.
* **Idea:** Concepto en evaluación, no automatizable con las herramientas actuales.

### Estructura de archivos
Las ADRs en estado **Aceptada** residen en `docs/adr/`. Las ADRs en estado **Propuesta** u **Idea** residen en `docs/proposals/`.

## Mecanismo de control

1. **CI Check:** El pipeline del repositorio verifica que toda ADR bajo `docs/adr/` incluya obligatoriamente y con contenido válido las secciones `## Evidencia de uso` y `## Mecanismo de control`.
2. **Plantilla obligatoria:** Toda nueva propuesta debe crearse utilizando la plantilla oficial en `templates/ADR.template.md`.

## Evidencia de uso

Aplicado para definir la transición de propuestas a reglas definitivas en este repositorio de gobernanza.

## Consecuencias

### Positivas
* Elimina las falsas garantías: solo lo que está automatizado se considera aceptado.
* Mantiene limpio el directorio `docs/adr/` con reglas efectivamente vigentes.

### Negativas
* Exige construir el script/check de automatización antes de dar por aceptada una regla.