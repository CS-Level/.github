# CS Level

Servicios y librerías de la solución CS Level (Rambla): reservas, disponibilidad, pagos y portal web, integrados con los PSS Resiber y Ecommerce.

Los repositorios son .NET 10 (Azure Functions isolated worker) y Next.js, y se apoyan en la infraestructura compartida de [APS-Framework](https://github.com/APS-Framework): paquetes `APS.*`, workflows reutilizables de CI/CD en [APS-Framework/.github](https://github.com/APS-Framework/.github#readme) y el servidor MCP [sdk-mcp-server](https://github.com/APS-Framework/sdk-mcp-server#readme).

---

## Servicios

| Repositorio | Descripción | Paquete cliente |
|---|---|---|
| [CS.Level.Booking](https://github.com/CS-Level/CS.Level.Booking#readme) | Orquestación de reservas: operaciones sobre pasajeros, contactos, segmentos, servicios auxiliares y billetes, sincronizadas con el PSS mediante una máquina de estados. | `CS.Level.Booking.Client` |
| [CS.Level.Booking.Data](https://github.com/CS-Level/CS.Level.Booking.Data#readme) | Consulta de solo lectura del histórico de una reserva. | — |
| [CS.Level.Availability](https://github.com/CS-Level/CS.Level.Availability#readme) | Disponibilidad, cotización, calendarios, cambios de tarifa y cargos por operaciones post-venta. | `CS.Level.Availability.Client` |
| [CS.Level.Payment](https://github.com/CS-Level/CS.Level.Payment#readme) | Links de pago y reembolsos sobre Adyen. | `CS.Level.Payment.Client` |
| [CS.Level.Webhooks](https://github.com/CS-Level/CS.Level.Webhooks#readme) | Recepción de notificaciones de Adyen: valida la firma HMAC y propaga la confirmación de pago o reembolso a Booking. | — |
| [CS.Level.Foundry](https://github.com/CS-Level/CS.Level.Foundry#readme) | API que genera informes de reserva con Azure AI Foundry. | — |
| [CS.Level.FrontEnd](https://github.com/CS-Level/CS.Level.FrontEnd#readme) | Portal web (Next.js) de la solución. | — |

## Dominio y conectores

| Repositorio | Paquete | Descripción |
|---|---|---|
| [CS.Level.Domain](https://github.com/CS-Level/CS.Level.Domain#readme) | `CS.Level.Domain` | Modelo de dominio, contratos `IRambla*` que implementa cada conector y `ConnectorResolver`. |
| [CS.Level.Connector.Resiber](https://github.com/CS-Level/CS.Level.Connector.Resiber#readme) | `CS.Level.Connector.Resiber` | Implementación de los contratos de dominio sobre el PSS Resiber. |
| [CS.Level.Connector.Ecommerce](https://github.com/CS-Level/CS.Level.Connector.Ecommerce#readme) | `CS.Level.Connector.Ecommerce` | Implementación de los contratos de dominio sobre Ecommerce. |

## Clientes de servicios externos

| Repositorio | Paquete | Descripción |
|---|---|---|
| [CS.Resiber.Client](https://github.com/CS-Level/CS.Resiber.Client#readme) | `Resiber.Native.Client` | Cliente SOAP de Resiber: RES, TKT, InfoVuelos y Tarificación. |
| [CS.Ecommerce.Client](https://github.com/CS-Level/CS.Ecommerce.Client#readme) | `CS.Ecommerce.Client` | Cliente REST de Ecommerce: reservas, bonos y bundles. |
| [CS.Airpricing.Client](https://github.com/CS-Level/CS.Airpricing.Client#readme) | `CS.Airpricing.Client` | Cliente REST de Air Pricing: precios, horarios, calendarios y estado de vuelos. |
| [CS.Adyen.Client](https://github.com/CS-Level/CS.Adyen.Client#readme) | `CS.Adyen.Client` | Cliente REST de Adyen Checkout y validación HMAC de webhooks. |

---

## Paquetes NuGet

Los paquetes se publican en GitHub Packages. Para consumirlos hacen falta los feeds de CS-Level y de APS-Framework (los paquetes de CS Level dependen de paquetes `APS.*`), con un token con `read:packages` en la variable de entorno `APS_NUGET_TOKEN`:

```xml
<packageSources>
  <clear />
  <add key="NugetOrg" value="https://api.nuget.org/v3/index.json" />
  <add key="APS-Framework" value="https://nuget.pkg.github.com/APS-Framework/index.json" />
  <add key="CS-Level" value="https://nuget.pkg.github.com/CS-Level/index.json" />
</packageSources>
<packageSourceCredentials>
  <APS-Framework>
    <add key="Username" value="x" />
    <add key="ClearTextPassword" value="%APS_NUGET_TOKEN%" />
  </APS-Framework>
  <CS-Level>
    <add key="Username" value="x" />
    <add key="ClearTextPassword" value="%APS_NUGET_TOKEN%" />
  </CS-Level>
</packageSourceCredentials>
```

Los repositorios que publican paquete documentan su instalación y configuración en `README-sdk.md`; las librerías y los servicios principales describen además su arquitectura interna, build y publicación en `README-dev.md`.
