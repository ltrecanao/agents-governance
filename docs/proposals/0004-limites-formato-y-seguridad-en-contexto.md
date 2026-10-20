# ADR 0004: Límites, formato y seguridad en contexto

* **Estado:** Propuesta
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

Si `AGENTS.md` crece sin control, satura la ventana de contexto y diluye la atención del modelo. Además, los archivos de contexto e instrucciones son un vector común de fuga de información sensible si se incluyen secretos o credenciales por descuido.

## Decisión

1. **Límite de tamaño en `AGENTS.md`:** `AGENTS.md` no debe superar un tamaño máximo razonable (ej. 150 líneas / 5 KB). Debe contener únicamente principios, arquitectura general y reglas no negociables.
2. **Formato obligatorio de Skills:** Toda skill debe incluir un frontmatter con `name` y `description` concisos que especifiquen con precisión **cuándo sí y cuándo no** debe cargarse.
3. **Prohibición de secretos:** Queda estrictamente prohibido incluir tokens, contraseñas, claves privadas, URLs internas sensibles o variables de entorno con credenciales en cualquier archivo de gobernanza, `AGENTS.md` o skill.

## Mecanismo de control

1. Linter en CI que falle si `AGENTS.md` supera el límite de líneas/caracteres.
2. Linter que valide la presencia y estructura del frontmatter en todas las skills.
3. Chequeo de seguridad (`gitleaks` o similar) en CI para prevenir el commit de secretos en el repositorio.

## Evidencia de uso

* Probado acotando el tamaño de `AGENTS.md` y definiendo descripciones claras en el frontmatter de skills, logrando que el agente active herramientas solo cuando corresponde y reduciendo el consumo inútil de memoria.

## Consecuencias

### Positivas
* Mantiene el prompt limpio, enfocado y económicamente eficiente.
* Evita filtraciones accidentales de credenciales en repositorios.

### Negativas
* Exige condensar y redactar con brevedad en lugar de pegar bloques largos de texto.