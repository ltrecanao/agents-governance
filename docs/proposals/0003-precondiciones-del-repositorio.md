# ADR 0003: Precondiciones del repositorio (Preflight)

* **Estado:** Propuesta
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

Un agente no debe asumir que el entorno de trabajo está configurado correctamente antes de empezar a escribir código o modificar el sistema.

## Decisión

Antes de ejecutar cualquier modificación, el agente debe verificar las precondiciones del entorno mediante `gh api` y herramientas locales:

* Protección activa de la rama `main`.
* Pipelines de CI configurados y bloqueantes.
* Deploy condicionado estrictamente al CI en verde.
* Existencia de `CODEOWNERS`.
* Presencia de `AGENTS.md` vigente y hooks locales activos.

Si alguna condición falla, el agente **se detiene e informa al usuario**; no intenta corregir la configuración del repositorio por su cuenta.

## Mecanismo de control

Script de preflight automatizado que el agente ejecuta obligatoriamente al iniciar cada sesión de trabajo y reporta el estado antes de procesar tareas.

## Evidencia de uso

Probado en verificaciones manuales con `gh api` comprobando la protección de la rama y configuraciones de merge antes de iniciar iteraciones.

## Consecuencias

### Positivas
* Previene operaciones destructivas en repositorios mal configurados.
* Establece una línea de base de seguridad obligatoria antes de trabajar.

### Negativas
* Depende de la disponibilidad de la API de GitHub y los permisos del token utilizado.