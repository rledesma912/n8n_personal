# n8n - Configuración con Docker

Este proyecto despliega **n8n**, una plataforma de automatización de flujos de trabajo de código abierto, usando Docker Compose.

## 🚀 Despliegue Rápido

1.  **Clona el repositorio:**
    ```bash
    git clone <url-de-tu-repositorio>
    cd <nombre-del-repositorio>
    ```

2.  **Configura las variables de entorno:**
    ```bash
    cp .env.example .env
    ```
    Edita el archivo `.env` y establece un **nombre de usuario** y una **contraseña segura**.

3.  **Inicia n8n:**
    ```bash
    docker-compose up -d
    ```

4.  **Accede a la interfaz:**
    Abre tu navegador en [http://localhost:5678](http://localhost:5678) e inicia sesión con las credenciales de tu archivo `.env`.

## 📦 Estructura del Proyecto
*   `docker-compose.yml` - Define el servicio de n8n con volumen personalizado.
*   `.env.example` - Plantilla para las variables de entorno.
*   `.gitignore` - Excluye archivos sensibles.
*   `/media/rick/Cosas/my_n8n_flows/` - **Ubicación personalizada** que contiene todos los datos persistentes (workflows, configuraciones, credenciales).

## 🔒 Gestión de Permisos
El directorio de datos personalizado requiere permisos adecuados. Si n8n no puede escribir:
```bash
# Solución rápida (entorno de desarrollo)
sudo chmod -R 777 /media/rick/Cosas/my_n8n_flows

# Solución específica (producción)
sudo chown -R 1000:1000 /media/rick/Cosas/my_n8n_flows

## ⚙️ Comandos Útiles
| Comando | Descripción |
|---------|-------------|
| `docker-compose logs -f n8n` | Muestra los logs en tiempo real. |
| `docker-compose down` | Detiene y elimina el contenedor. |
| `docker-compose pull && docker-compose up -d` | Actualiza n8n a la última versión. |

## 🔒 Consideraciones de Seguridad para Producción
*   **Nunca** expongas el puerto `5678` directamente a Internet sin un proxy inverso (como Nginx o Caddy) con HTTPS[citation:8].
*   Para mayor robustez, considera cambiar la base de datos de SQLite (por defecto) a **PostgreSQL**[citation:1][citation:7].
*   Realiza **copias de seguridad periódicas** de la carpeta `n8n_data`.

## ⁉️ Solución de Problemas Comunes
*   **Error de permisos (EACCES):** Si al iniciar ves errores de permiso denegado, ejecuta:
    ```bash
    sudo chown -R 1000:1000 ./n8n_data
    ```[citation:3]
*   **Error de "cookies seguras":** Si accedes por HTTP (sin HTTPS) y la página no carga, para desarrollo puedes añadir `- N8N_SECURE_COOKIE=false` en el `docker-compose.yml`. **No uses esto en producción**[citation:8].