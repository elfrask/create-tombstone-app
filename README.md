# create-tombstone-app

Plantilla base de Tombstone.

## Estructura

```
app/
  core/         bootstrap y contexto
  routes/       registro de rutas
  controllers/  controladores HTTP
  requests/     entrada/validacion de casos de uso
  services/     servicios de aplicacion
  models/       modelos ORM
  resources/    presentacion JSON
  views/        paginas CMX
  components/   componentes CMX
database/
  migrations/   migraciones versionadas
  seeds/        seeders idempotentes
  database/     archivos SQLite
config/
  environment.clsx carga .env (modulo estandar `env`)
  app.clsx      configuracion de la app
  database.clsx configuracion de la base
public/         assets estaticos
```

## Desarrollo

```bash
cp .env.example .env
tombstone migrate
clx run app/main.clsx -- 3000
clx run app/main.clsx -- test
```

`app/views/Layout.clsx` centraliza el documento HTML de todas las paginas; las
rutas usan `Page(...)`. `app.not_found(...)` devuelve la vista 404 con el mismo
layout.

La plantilla usa `pathModules` para resolver el repo CLS durante el desarrollo.
En una app instalada, ajusta esas rutas a los modulos globales.

## .env

`config/environment.clsx` usa el modulo estandar `env`:

```clx
import "env" as env;
var values = env.load(".env");
values.get("APP_NAME");
```

Las variables del sistema (`system_env`) siguen teniendo prioridad si tu
config las consulta explicitamente.
