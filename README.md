# Módulo 6: Integración Continua con GitHub Actions (`lab-cicd`)

Este repositorio implementa un flujo de **CI/CD** automatizado mediante **GitHub Actions**, diseñado para validar la integridad y la sintaxis de los archivos de infraestructura (`docker-compose.yml`) antes de permitir cualquier cambio en la rama principal.

---

## Arquitectura del Workflow

```text
  ┌───────────────┐         git push         ┌───────────────────┐
  │  Desarrollador│ ───────────────────────> │   GitHub Remote   │
  │  (Local Host) │                          │   (Repositorio)   │
  └───────────────┘                          └────────┬──────────┘
                                                      │
                                                      │ Trigger (push / PR)
                                                      │
                                             ┌────────▼──────────┐
                                             │  GitHub Actions   │
                                             │  (Runner Ubuntu)  │
                                             └────────┬──────────┘
                                                      │
                                                      │ docker compose config
                                                      │
                                             ┌────────▼──────────┐
                                             │ Validacion Exitosa│
                                             │    (Check Verde)  │
                                             └───────────────────┘
                                             
 Tecnologías Utilizadas:

GitHub Actions: Motor de automatización y ejecución de pipelines CI/CD.
Docker & Docker Compose: Orquestación validada de contenedores.
YAML: Sintaxis de configuración para los workflows.

Estructura del Workflow (.github/workflows/ci.yml)

El pipeline se ejecuta automáticamente ante cada evento de push o pull_request hacia la rama main, realizando las siguientes acciones:
Clona el repositorio en un entorno limpio (ubuntu-latest).
Configura las herramientas de Docker Compose.
Ejecuta la validación de sintaxis para prevenir errores de despliegue en producción.

Instrucciones de uso
Clona el repositorio y ejecuta validaciones locales:

git clone [https://github.com/flyfresh9/lab-cicd.git](https://github.com/flyfresh9/lab-cicd.git)
cd lab-cicd
docker compose config