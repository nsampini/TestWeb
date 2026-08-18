# TestWebKubernetes.Web

Front Blazor WebAssembly independiente que consume la API de pruebas.

## Ejecutar localmente

Primero iniciar la API en `http://localhost:5190`.

```powershell
dotnet restore
dotnet run
```

Por defecto corre en `http://localhost:5222` y consume `GET /api/products`.
