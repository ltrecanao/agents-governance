# ADR 0003 Testing y verificación automatizada

* **Estado:** Propuesta
* **Fecha:** 2026-10-19
* **Autores:** Lucas Trecanao

## Contexto

Confiar únicamente en la revisión humana para validar el código generado por un agente es inviable a largo plazo. Sin barreras automatizadas estrictas, los agentes tienden a introducir regresiones, omitir pruebas para código nuevo o incluso eliminar tests existentes para lograr que la ejecución pase en verde.

## Decisión

1. **Gates de CI obligatorios:** Todo cambio debe superar el conjunto de pruebas unitarias, umbrales de cobertura de código y pruebas de mutación (mutation testing) configurados en la integración continua.
2. **Invariante de tests:** Un cambio que elimine pruebas, deshabilite suites existentes o reduzca los umbrales de cobertura requeridos será rechazado automáticamente.
3. **Protección de tests (`CODEOWNERS`):** El directorio de pruebas y la configuración de cobertura quedan bajo el archivo `CODEOWNERS`, impidiendo que el agente debilite la suite de verificación sin revisión del propietario.
4. **Flujo de desarrollo:** Exigir "escribir el test antes del código" se mantiene únicamente como una recomendación de buena práctica en `AGENTS.md`, no como una regla bloqueante de Git, priorizando la atomicidad y la validez de los commits.

## Mecanismo de control

1. Pipeline de CI con gates bloqueantes de cobertura y mutation testing.
2. Script o check de CI que compare la cantidad de tests y umbrales contra la rama base (`main`) para evitar retrocesos.
3. Asignación de revisión obligatoria vía `CODEOWNERS` sobre la carpeta de tests.

## Evidencia de uso

* Probado ejecutando suites de prueba de CI localmente antes de integrar cambios a la rama principal, verificando que los gates detengan la progresión si no se cumplen los estándares.

## Consecuencias

### Positivas
* Garantiza la calidad e integridad del código sin depender de la revisión manual línea por línea.
* Evita que el agente "trampee" los tests deshabilitándolos o bajando la cobertura.

### Negativas
* Exige mantener una suite de tests rápida y confiable en el repositorio para no demorar las iteraciones.