# Agents Governance

Repositorio de **definiciones de arquitectura y gobernanza** para proyectos asistidos por agentes de inteligencia artificial.

Este repositorio contiene exclusivamente estándares, reglas y plantillas de diseño. No almacena código de producto ni implementaciones específicas. La fuente de las reglas ejecutables y skills base se referencia de manera externa para evitar duplicación.

## Principios Rectores

1. **Contexto acotado:** El agente solo debe cargar permanentemente lo estrictamente necesario en `AGENTS.md`. Los procedimientos específicos se desacoplan en skills a demanda.
2. **Cero confianza ciega:** Ninguna decisión de arquitectura (ADR) se considera "Aceptada" basándose únicamente en buena voluntad o revisión humana; requiere evidencia de uso y un mecanismo de control automatizable.
3. **Trazabilidad y atomicidad:** Todo cambio se rige por Conventional Commits, un cambio por commit, prohibición absoluta de trabajar o commitear en estado rojo, y hooks locales obligatorios (`pre-push`).
4. **Seguridad por diseño:** Prohibición estricta de incluir secretos en los artefactos de gobernanza, con validaciones automatizadas en CI y protección de ramas y artefactos críticos mediante `CODEOWNERS`.
5. **Verificación previa (Preflight):** El agente verifica de forma automatizada las precondiciones de seguridad del entorno antes de iniciar cualquier tarea de desarrollo.

## Índice de Decisiones de Arquitectura (ADR)

### Aceptadas
*(Requieren evidencia de uso y mecanismo de control implementado)*
* [ADR 0000: Criterios de aceptación de ADRs](./docs/adr/0000-criterios-de-aceptacion.md)

### Propuestas
*(Automatizables, con diseño o evidencia parcial, pendiente de implementación del mecanismo)*
* [ADR 0001: Roles de AGENTS.md y skills](./docs/proposals/0001-roles-agents-md-y-skills.md)
* [ADR 0002: Commits, push y trazabilidad](./docs/proposals/0002-commits-push-y-trazabilidad.md)
* [ADR 0003: Precondiciones del repositorio (Preflight)](./docs/proposals/0003-precondiciones-del-repositorio.md)
* [ADR 0004: Límites, formato y seguridad en contexto](./docs/proposals/0004-limites-formato-y-seguridad.md)
* [ADR 0005: Testing y verificación automatizada](./docs/proposals/0005-testing-y-verificacion.md)

## Estructura del Repositorio

```text
agents-governance/
├── README.md
├── docs/
│   ├── adr/               # ADRs Aceptadas (mecanismo implementado)
│   └── proposals/         # ADRs Propuestas e Ideas
└── templates/             # Plantillas reutilizables (ADR, AGENTS.md, SKILL.md)