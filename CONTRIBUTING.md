# Guía de contribución · CS Level

Convenciones comunes a los repositorios de CS-Level. Si un repositorio tiene su propio `CONTRIBUTING.md`, manda el suyo.

## Commits y título de la PR: Conventional Commits

```
<tipo>: <descripción>
```

Tipos válidos (los mismos que el `.commitlintrc.json` de los repositorios): `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.

Reglas:
- Tipo en minúsculas y obligatorio.
- Descripción entre 10 y 100 caracteres; cabecera completa de 120 como máximo.
- Descripción en infinitivo: "add", no "added".

```bash
git commit -m "fix: handle null amount in refund request

AB#1234"
```

Que commitlint se ejecute o bloquee depende de cada repositorio: consulta sus workflows antes de dar por hecho que hay un check.

## Work items de Azure DevOps

Vincula el work item con `AB#<id>` en la descripción de la PR (o en el commit). La plantilla de PR lo pide; si un repositorio lo valida automáticamente, lo indica en su propia documentación.

## Antes de abrir la PR

- **.NET**: los repositorios restauran paquetes de GitHub Packages (APS-Framework y CS-Level). Define la variable de entorno `APS_NUGET_TOKEN` con un token con `read:packages` y compila la solución indicándola de forma explícita, por ejemplo `dotnet build <Repo>.sln`.
- **Tests**: en los servicios, los unitarios están en `tests/*.UnitTest` y se ejecutan en el build de CI (algunas librerías mantienen aún un único proyecto en `test/`; mira su `README-dev.md`). Los de `tests/*.IntegrationTest` llevan `[TestCategory("Integration")]` y necesitan el App Configuration del entorno; en local, `dotnet test <Repo>.sln --filter "TestCategory!=Integration"`.
- **Documentación**: si cambias contratos públicos, configuración o despliegue, actualiza `README.md`, `README-sdk.md` o `README-dev.md` del repositorio en el mismo PR.
- **Secretos**: nunca en código, commits, PRs ni logs. La configuración vive en Azure App Configuration y Key Vault.

## CI/CD

Cada repositorio define sus workflows en `.github/workflows/`, apoyados en los reutilizables de [APS-Framework/.github](https://github.com/APS-Framework/.github#readme). Los paquetes NuGet se publican con `workflow_dispatch` (`release_type`: `rc` o `stable`); un push solo ejecuta CI.

## Protección de ramas

Las reglas (revisiones obligatorias, checks requeridos) se configuran en GitHub por repositorio. Consúltalas en la configuración del repositorio antes de asumir qué es obligatorio.
