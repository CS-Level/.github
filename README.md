# CS-Level/.github

Repositorio especial de la organización CS-Level en GitHub.

| Fichero | Uso |
|---|---|
| `CONTRIBUTING.md` | Guía de contribución por defecto. GitHub la muestra en los repositorios de la organización que no tienen la suya. |
| `PULL_REQUEST_TEMPLATE.md` | Plantilla de PR por defecto, con la misma regla: aplica a los repositorios sin `PULL_REQUEST_TEMPLATE.md` propio. |

Un repositorio que necesite convenciones distintas añade su propio fichero, que sustituye al de aquí.

Los workflows reutilizables de CI/CD (build, despliegue de Functions y Web Apps, swap de slots, publicación NuGet) **no** viven aquí, sino en [APS-Framework/.github](https://github.com/APS-Framework/.github#readme), y cada repositorio los invoca desde su `.github/workflows/`.

Este repositorio es público porque GitHub solo aplica los ficheros por defecto desde un `.github` público. El perfil de la organización (catálogo de repositorios y paquetes) es información interna y vive en [CS-Level/.github-private](https://github.com/CS-Level/.github-private/blob/main/profile/README.md), visible solo para los miembros.
