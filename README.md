# Finanzas en Orden

Aplicación web para registrar ingresos y gastos, organizar cuentas y categorías, y consultar resúmenes y gráficos. La app utiliza PostgreSQL en la nube; no guarda usuarios ni finanzas en archivos locales.

## Archivos que subir a GitHub

Sube solo estos archivos y carpetas:

- `app.py`
- `requirements.txt`
- `README.md`
- `.gitignore`
- `.streamlit/config.toml`
- `.streamlit/secrets.toml.example`

No subas `venv/`, `__pycache__/`, `data/`, bases `.db` o un `.streamlit/secrets.toml` real.

## Publicación

Necesitas una cuenta de GitHub, una cuenta de Streamlit Community Cloud y un proyecto PostgreSQL en Supabase.

1. Crea el proyecto de base de datos en Supabase. En **Connect**, copia la cadena **Session pooler** y usa SSL (`sslmode=require`).
2. Crea un repositorio GitHub para **Finanzas en Orden** y sube únicamente los archivos enumerados arriba.
3. En [share.streamlit.io](https://share.streamlit.io/), conecta ese repositorio y selecciona la rama `main` y `app.py`.
4. Antes de desplegar, abre **Advanced settings / Secrets** y añade la conexión privada en formato TOML:

   ```toml
   FINANZAS_DATABASE_URL = "postgresql://USUARIO:CONTRASEÑA@HOST:PUERTO/postgres?sslmode=require"
   ```

   Reemplaza todo el ejemplo por la cadena proporcionada por Supabase. No guardes la cadena en GitHub ni la compartas en el chat.
5. Despliega la app. Al iniciar, creará las tablas vacías en PostgreSQL. Luego crea tu usuario desde la pestaña **Crear mi usuario**.

## Privacidad y almacenamiento

- GitHub contiene el código fuente. La base y su contraseña se guardan separadas: la base en Supabase y la conexión en Streamlit Secrets.
- Las contraseñas de las personas que se registren se guardan como hash con sal individual.
- La base remota empieza vacía; no importa ni sube cuentas, usuarios o datos locales de prueba.
- No existe modo SQLite local en esta versión.
- Para que solo tú puedas acceder a la web, configura el acceso de la app como privado en Streamlit. Si la dejas pública, cualquier persona podrá visitar y registrarse, aunque sus registros se mantengan asociados a su propio usuario.

## Desarrollo local

Esta versión está diseñada para conectarse a PostgreSQL mediante `FINANZAS_DATABASE_URL`. No incluye almacenamiento local. Para pruebas locales también tendrías que proporcionar una URL de PostgreSQL por variable de entorno o en `.streamlit/secrets.toml` (ese archivo está excluido de Git).