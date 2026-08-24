# spring-boot-webapi

Copia propia del proyecto [pablovillazon/spring-boot-webapi](https://github.com/pablovillazon/spring-boot-webapi), usada como base para el **Laboratorio de integración de JUnit y Code Coverage en CI con GitHub Actions**.

## Objetivo del laboratorio

1. Integrar la ejecución de las pruebas unitarias (JUnit) dentro del pipeline de CI.
2. Integrar el análisis de cobertura de código (JaCoCo) dentro del mismo pipeline.
3. Verificar que ambos pasos se ejecuten correctamente en GitHub Actions.

## Estructura relevante

```
src/main/java/com/cicd/webapi/Calculator.java     # Lógica de negocio de ejemplo
src/test/java/com/cicd/webapi/CalculatorTest.java # Pruebas unitarias (JUnit 5)
pom.xml                                           # Configuración de Maven + plugin JaCoCo
.github/workflows/maven.yml                       # Pipeline de CI (GitHub Actions)
```

## Cobertura de código (JaCoCo)

El `pom.xml` incluye el plugin `jacoco-maven-plugin`, con dos ejecuciones:

- `prepare-agent`: instrumenta las clases antes de correr los tests.
- `report` (fase `verify`): genera el reporte HTML de cobertura una vez finalizados los tests.

## Cómo ejecutar localmente

Correr solo las pruebas:

```bash
mvn -B test --file pom.xml
```

Correr las pruebas y generar el reporte de cobertura:

```bash
mvn clean verify
```

Si el build finaliza con `BUILD SUCCESS`, el reporte de cobertura queda disponible en:

```
target/site/jacoco/index.html
```

## Pipeline de CI (GitHub Actions)

El workflow [`maven.yml`](.github/workflows/maven.yml) se ejecuta en cada `push` a `master`/`feature/**` y en cada `pull_request` a `master`, e incluye entre otros los siguientes pasos:

- **Run tests with Maven** — `mvn -B test --file pom.xml`
- **Run Code Coverage with Maven** — `mvn -B verify --file pom.xml`

## Requisitos

- JDK 21 (el pipeline de CI usa JDK 25 vía `actions/setup-java`)
- Maven 3.9+ (o el wrapper `./mvnw` incluido en el repositorio)
