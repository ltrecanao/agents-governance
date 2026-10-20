# AGENTS.md

> **Ubicación obligatoria en el repositorio:** `/AGENTS.md` (Raíz del proyecto)

## Propósito del repositorio
[Breve descripción de qué hace este proyecto, su stack tecnológico principal y su arquitectura general.]

## Reglas no negociables
1. **Commits y trazabilidad:** Un cambio por commit, Conventional Commits, prohibido el push automático sin orden y nunca commitear en estado rojo.
    * **Formato:** `<tipo>: <descripción>`.
    * **Tipos:** `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `ci`.
    * **Límite:** Máximo **50 caracteres** en una sola línea (atómico y sin cuerpo).

2. **Seguridad:** Prohibido incluir credenciales, secretos o tokens en ningún archivo de código o documentación.
3. **Testing:** Todo código nuevo o modificado debe incluir sus pruebas. No se permite deshabilitar tests existentes para pasar el build.

## Estructura de contexto y skills disponibles
* El contexto permanente se mantiene acotado en este archivo (`/AGENTS.md`).
* Los procedimientos específicos se cargan a demanda desde la carpeta `.agent/skills/<nombre-skill>/SKILL.md` cuando la tarea lo requiere.
