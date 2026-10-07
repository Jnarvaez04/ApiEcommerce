# API Ecommerce

API REST para gestionar productos, categorías y usuarios de un ecommerce, construida con **ASP.NET Core** y **SQL Server**. Proyecto de práctica desarrollado durante el curso de .NET Backend de DevTalles, con el objetivo de aplicar autenticación, arquitectura por capas y buenas prácticas de diseño de APIs.

## Tecnologías

- **ASP.NET Core Web API** (C#)
- **Entity Framework Core** con **SQL Server** (migraciones incluidas)
- **ASP.NET Core Identity** para la gestión de usuarios
- **Autenticación JWT (Bearer)**
- **Mapster** para el mapeo entre entidades y DTOs
- **Swagger / OpenAPI** con soporte para enviar el token JWT desde la interfaz
- **Versionado de API** (v1 y v2)
- **Docker Compose** (`docker-compose.yaml` incluido en el repositorio)

## Características

- **Autenticación y autorización con JWT:** el usuario inicia sesión, recibe un token y lo usa en el header `Authorization: Bearer <token>`.
- **Gestión de productos, categorías y usuarios**, cada uno con su propio repositorio.
- **Patrón Repository:** la lógica de acceso a datos está separada de los controladores mediante interfaces (`ICategoryRepository`, `IProductRepository`, `IUserRepository`) registradas con inyección de dependencias.
- **Versionado de la API:** dos versiones documentadas (v1 y v2) y versión por defecto v1 cuando no se especifica.
- **Caché de respuestas:** perfiles de caché configurables (10 y 20 segundos) aplicados a los endpoints.
- **Datos iniciales:** un `DataSeeder` carga información de ejemplo en la base de datos.
- **Archivos estáticos:** imágenes de productos servidas desde `wwwroot/ProductsImages`.
- **CORS configurado** mediante una política con nombre.
- **Colección de Postman** (`API-Ecommerce.postman_collection.json`) y archivo `ApiEcommerce.http` para probar los endpoints.

## Estructura del proyecto

```
ApiEcommerce/
├── Constants/      # Nombres de políticas CORS y perfiles de caché
├── Controllers/    # Endpoints de la API
├── Data/           # DbContext y datos iniciales (seeder)
├── Mapping/        # Configuración de Mapster
├── Migrations/     # Migraciones de Entity Framework Core
├── Models/         # Entidades y DTOs
├── Repository/     # Repositorios e interfaces (IRepository/)
└── wwwroot/        # Imágenes de productos
```

## Cómo ejecutarlo

**Requisitos:** .NET SDK y una instancia de SQL Server.

1. Clona el repositorio.
2. Configura en `appsettings.Development.json`:
   - `ConnectionStrings:ConexionSql`: cadena de conexión a tu SQL Server.
   - `ApiSettings:SecretKey`: clave secreta usada para firmar los tokens JWT (la API no inicia sin ella).
3. Aplica las migraciones:
   ```bash
   dotnet ef database update
   ```
4. Ejecuta la API:
   ```bash
   dotnet run
   ```
5. En desarrollo, abre Swagger en `/swagger` para explorar y probar los endpoints.

## Autenticación en Swagger

1. Inicia sesión desde el endpoint de login y copia el token que devuelve.
2. Pulsa el botón **Authorize** en Swagger.
3. Pega el token y confirma. Los endpoints protegidos quedarán habilitados.

## Autor

**Jhoan Narváez Torres**, Full-Stack Developer (React y .NET Core)
[LinkedIn](https://www.linkedin.com/in/jhoannarvaez/) · j.narvaez564@gmail.com