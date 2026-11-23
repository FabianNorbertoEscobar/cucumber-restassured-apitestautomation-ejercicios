# Automatización de pruebas de API

Repositorio de prácticas para automatizar y documentar pruebas de servicios REST con Java, Cucumber y REST Assured.

## Stack y tecnologías

- **Java 8** como lenguaje y versión de compatibilidad.
- **Gradle** para la gestión de dependencias y ejecución de pruebas.
- **Cucumber 6.10.3** y **Gherkin** para describir escenarios en lenguaje natural.
- **REST Assured** para construir solicitudes HTTP y validar respuestas JSON.
- **JUnit** como integración de ejecución de Cucumber (`cucumber-junit`); también está incluida la dependencia de JUnit Jupiter.
- **ExtentReports Cucumber Adapter** para generar reportes legibles de Cucumber.
- **JSON-java** para el manejo de datos JSON.

Las dependencias están declaradas en `build.gradle`. REST Assured figura allí en dos versiones (4.3.3 y 3.3.0); Gradle resuelve el conflicto de versiones durante la resolución de dependencias.

## Funcionalidades y ejercicios

### Pruebas API con Cucumber

En `src/test/resources/features/APITest.feature` se describen ejercicios para:

- realizar una solicitud `GET` a la API de GitHub y validar el código HTTP;
- comprobar la cantidad de elementos de una respuesta;
- buscar un valor en una lista de usuarios;
- validar un campo anidado de la respuesta.

Los step definitions correspondientes están en `src/test/java/Steps/APISteps.java`. El runner (`src/test/java/Runner/Runner.java`) configura la ejecución de escenarios etiquetados con `@API` y genera un reporte JSON en `target/cucumber-reports.json`, además del reporte de ExtentReports.

**Estado actual:** en el feature, `@API` está aplicado únicamente al primer escenario. Por eso, el runner configurado selecciona ese escenario; los otros tres están escritos, pero no se ejecutan con ese filtro.

### Ejemplos y prácticas adicionales

- `src/test/java/Steps/ejemplosAPI.java` reúne ejemplos de solicitudes `GET`, `POST`, `PUT` y `DELETE`, una solicitud SOAP, autenticación básica y por formulario, y un flujo OAuth. Son métodos de práctica, no escenarios conectados al runner.
- `src/test/resources/features/BraveNewCoin.feature` contiene escenarios planteados para obtener un token y validar respuestas de error de BraveNewCoin. Aún no están implementados por completo: faltan step definitions para esos pasos, por lo que no se consideran pruebas ejecutables.
- `src/test/resources/Payloads/ejemplo.json` contiene un payload JSON de ejemplo.

## Estructura del proyecto

```text
src/test/java/Runner/       Runner de Cucumber
src/test/java/Steps/        Step definitions y ejemplos REST Assured
src/test/resources/features/ Escenarios Gherkin
src/test/resources/Payloads/ Payloads JSON de práctica
```

## Ejecución

Con Java 8 o compatible y Gradle instalado, ejecutar desde la raíz:

```bash
gradle test
```

Para ejecutar otros escenarios de `APITest.feature`, etiquetarlos con `@API` o ajustar el filtro `tags` en `Runner.java`. Las pruebas que llamen servicios externos requieren conectividad y que los endpoints estén disponibles.
