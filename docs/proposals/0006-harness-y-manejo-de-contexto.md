# ADR 0006 Harness y manejo de Contexto

* **Estado:** Propuesta
* **Fecha:** 2026-10-21
* **Autores:** Lucas Trecanao

## Contexto

Tras definir la separación entre `AGENTS.md` y Skills en el ADR 0001, se requiere un mecanismo técnico (harness) que automatice la gestión de este contexto para evitar la saturación de la ventana de tokens y la degradación de la precisión del modelo.

## Decisión

Se implementará un **Harness de Contexto Dinámico** con el siguiente flujo:

1. **Carga Base:** Inyección obligatoria de `AGENTS.md` como instrucción de sistema al inicio de la sesión.
2. **Descubrimiento de Skills:** Indexación del frontmatter (`name`, `description`) de las skills disponibles.
3. **Inyección Just-in-Time (JIT):** Carga del contenido de la skill específica solo cuando la intención del usuario lo requiera.
4. **Purga de Contexto:** Eliminación de la skill del contexto una vez finalizada la tarea asociada, preservando únicamente la base de `AGENTS.md`.

## Mecanismo de control

1. **Orquestador de Contexto:** Capa de software intermediaria encargada de la inserción y remoción de archivos `.md` en el prompt.

## Evidencia de uso

La implementación del harness elimina la necesidad de handoffs manuales y permite la continuidad del flujo de trabajo sin interrupciones por límite de tokens, incrementando la precisión de las respuestas al reducir el ruido en la ventana de contexto.

## Consecuencias

### Positivas
* Eliminación de interrupciones manuales para la gestión de contexto.
* Mayor precisión mediante el aislamiento de instrucciones operativas.
* Continuidad operativa en sesiones de larga duración.

### Negativas
* Latencia mínima adicional durante la fase de descubrimiento y carga de skills.