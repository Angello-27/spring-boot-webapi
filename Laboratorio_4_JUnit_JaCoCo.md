# Laboratorio 3 — Integración de JUnit y Code Coverage en CI

## Repositorio base

https://github.com/pablovillazon/spring-boot-webapi.git

## 1.- Integración de las pruebas unitarias en el CI

1. Clonar el repositorio y crear una copia en su propia cuenta de GitHub.

2. Revisar las pruebas unitarias existentes en:

```text
src/test/
```

3. Verificar en `pom.xml` la dependencia de testing utilizada por Spring Boot.

4. Ejecutar las pruebas localmente:

```bash
mvn test
```

5. Verificar que las pruebas finalicen correctamente:

```text
BUILD SUCCESS
```

6. Revisar los reportes generados por Maven en:

```text
target/surefire-reports/
```

7. Abrir el archivo del pipeline:

```text
.github/workflows/maven.yml
```

8. Incorporar la ejecución de las pruebas unitarias mediante Maven.

Utilizar la estructura:

```yaml
- name: Run tests with Maven
  run: mvn -B test --file pom.xml
```

9. Realizar `commit` y `push` de los cambios.

10. Ingresar a **GitHub → Actions** y verificar la ejecución del pipeline.

11. Comprobar que el paso **Run tests with Maven** finalice correctamente.

## 2.- Integración del Code Coverage (JaCoCo) en el CI

1. Agregar el plugin **JaCoCo** en el archivo:

```text
pom.xml
```

2. Ejecutar localmente:

```bash
mvn clean verify
```

3. Verificar que la ejecución finalice con:

```text
BUILD SUCCESS
```

4. Revisar la carpeta generada:

```text
target/site/jacoco/
```

5. Abrir el reporte:

```text
target/site/jacoco/index.html
```

6. Revisar la información de cobertura generada por JaCoCo.

7. Modificar nuevamente:

```text
.github/workflows/maven.yml
```

para ejecutar el proceso que genera el reporte de cobertura.

Utilizar la estructura:

```yaml
- name: Run Code Coverage with Maven
  run: mvn -B verify --file pom.xml
```

8. Realizar `commit` y `push` de los cambios.

9. Verificar en **GitHub → Actions** que el paso **Run Code Coverage with Maven** finalice correctamente.

## 3.- Modificación y verificación final del pipeline

El pipeline debe ejecutar como mínimo:

```text
Build
  ↓
Run tests with Maven
  ↓
Run Code Coverage with Maven
```

Verificar que ambos procesos se ejecuten correctamente en GitHub Actions.

### Tarea

Elaborar un **PDF** que contenga:

1. Captura de GitHub Actions mostrando la ejecución exitosa de:

   - `Run tests with Maven`

2. Captura de GitHub Actions mostrando la ejecución exitosa de:

   - `Run Code Coverage with Maven`

3. Captura del reporte de JaCoCo generado localmente en:

```text
target/site/jacoco/index.html
```

4. Incluir en la entrega el enlace al repositorio GitHub utilizado para realizar la actividad.
