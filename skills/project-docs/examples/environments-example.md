# Variables de Entorno — api-core

Las variables marcadas como **Required: `true`** deben estar presentes al iniciar la aplicación. Si faltan, la aplicación lanza un error y no arranca.

---

### APLICACIÓN

* **NODE_ENV**: Entorno de ejecución.
  - Default: ninguno
  - Required: `true`
  - Valores: `development`, `production`, `test`
* **DATABASE_URL**: URL de conexión a la base de datos PostgreSQL.
  - Default: ninguno
  - Required: `true`
  - Ejemplo: `postgresql://user:password@localhost:5432/restaurants`
* **PORT**: Puerto en que escucha la API.
  - Default: ninguno
  - Required: `true`
  - Rango válido: `1–65535`
* **API_BASE_URL**: URL pública de la API (usada en presigned URLs).
  - Default: `http://localhost:3000`
  - Required: `false`
* **FRONTEND_URL**: URL del frontend (usada en CORS y redirecciones).
  - Default: `http://localhost:4321`
  - Required: `false`

---

### AUTH / JWT

* **JWT_SECRET**: Clave secreta para firmar tokens JWT.
  - Default: ninguno
  - Required: `true`
  - **Producción**: mínimo 32 caracteres, generado aleatoriamente. Usar `openssl rand -base64 48`.
  - No reutilizar el mismo valor entre entornos.
