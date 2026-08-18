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

Deploy manual con imagenes publicadas:

```bash
mkdir -p /opt/testweb
cd /opt/testweb
curl -fsSLO https://raw.githubusercontent.com/nsampini/TestWeb/main/docker-compose.yml
mkdir -p deploy
curl -fsSLo deploy/edge.conf https://raw.githubusercontent.com/nsampini/TestWeb/main/deploy/edge.conf
docker compose up -d --scale api=2 --scale web=2
```

El reverse proxy externo de la VM debe apuntar al puerto `8080` del host.

Deploy automatico:

Configurar estos secretos en GitHub Actions del repo `TestWeb`:

- `VM_HOST`: IP o dominio de la VM.
- `VM_USER`: usuario SSH.
- `VM_SSH_KEY`: clave privada SSH con acceso a la VM.
- `VM_PORT`: puerto SSH, opcional; default `22`.
- `VM_APP_DIR`: carpeta de deploy, opcional; default `/opt/testweb`.

El workflow publica la imagen del Web y ejecuta `docker compose pull` + `docker compose up -d` en la VM.
