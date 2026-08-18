# TestWebKubernetes.Web

Front Blazor WebAssembly independiente que consume la API de pruebas.

## Ejecutar localmente

Primero iniciar la API en `http://localhost:5190`.

```powershell
dotnet restore
dotnet run
```

Por defecto corre en `http://localhost:5222` y consume `GET /api/products`.

## Docker

```powershell
docker build -t testweb:local .
docker run --rm -p 5222:8080 testweb:local
```

En Docker, el Web usa `/api` en el mismo host y Nginx proxya la llamada al contenedor `api`.

## Deploy en VM

Clonar los dos repos como carpetas hermanas:

```bash
git clone https://github.com/nsampini/TestApi.git
git clone https://github.com/nsampini/TestWeb.git
cd TestWeb
docker compose up -d --build
```

El reverse proxy externo de la VM debe apuntar al puerto `8080` del host.
