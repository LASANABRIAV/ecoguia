# 🌱 Ecoguía

Sitio web educativo sobre reciclaje, hecho con Flask y SQLite. Explica qué materiales se pueden reciclar y cómo separarlos, y permite que los visitantes dejen sugerencias que un administrador revisa en un panel protegido.

## Funciones

- Página pública con contenido educativo sobre reciclaje.
- Formulario para enviar sugerencias (nombre, correo y mensaje).
- Acceso de administrador con usuario y contraseña.
- Panel protegido para ver las sugerencias recibidas.
- Base de datos SQLite: no necesita instalar ningún servidor.

## Requisitos

- Python 3.10 o superior
- pip
- Git

## Instalación

### 1. Clonar el repositorio

```
git clone https://github.com/LASANABRIAV/ecoguia.git
cd ecoguia
```

### 2. Crear y activar el entorno virtual

En Windows (PowerShell):

```
python -m venv venv
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
venv\Scripts\activate
```

En Linux o macOS:

```
python3 -m venv venv
source venv/bin/activate
```

### 3. Instalar las dependencias

```
pip install -r requirements.txt
```

### 4. Crear el administrador

La base de datos (`instance/app.db`) se crea sola la primera vez que arranca la aplicación. Para crear el usuario administrador, ejecuta:

```
python crear_admin.py
```

El script te pedirá un usuario y una contraseña. La contraseña no se ve mientras la escribes y se guarda cifrada (hash), nunca en texto plano. Si el usuario ya existe, el script lo avisa y no crea un duplicado.

### 5. Iniciar la aplicación

```
python main.py
```

Abre en el navegador: <http://127.0.0.1:5000>

Si el puerto 5000 está ocupado, cambia el valor de `port` en `main.py`.

## Uso

- **Visitantes:** leen la guía y envían sugerencias desde el formulario al final de la página de inicio.
- **Administrador:** pulsa "Acceso administrador" en la barra superior, inicia sesión y entra al "Panel" para ver las sugerencias.

## Estructura del proyecto

```
ecoguia
├── app
│   ├── static/style.css     # estilos en verde
│   ├── templates            # páginas HTML (base, index, login, panel)
│   ├── routes.py            # rutas: inicio, sugerencias, login, logout, panel
│   ├── tables.py            # tablas: sugerencias y administradores
│   └── db.py                # conexión con SQLite
├── config.py                # configuración (base de datos y SECRET_KEY)
├── crear_admin.py           # script para crear el administrador
├── main.py                  # punto de entrada
└── requirements.txt
```

## Configuración

La configuración se lee de variables de entorno, con valores por defecto para desarrollo:

| Variable     | Valor por defecto   | Descripción                          |
|--------------|---------------------|--------------------------------------|
| `DATABASE`   | `instance/app.db`   | Ruta del archivo de base de datos    |
| `SECRET_KEY` | `dev`               | Clave para firmar las sesiones       |

> ⚠️ Es un proyecto académico con datos ficticios. Si algún día se publica en internet, hay que definir un `SECRET_KEY` propio como variable de entorno y usar una contraseña de administrador segura.

## Docker

Pendiente. Como la base de datos es un archivo SQLite, al usar contenedores habrá que guardar la carpeta `instance/` en un volumen para no perder los datos.

## Créditos y licencia

Proyecto basado en la plantilla [flask-sqlite-app-factory-template](https://github.com/theneurocoder/flask-sqlite-app-factory-template) de TheNeuroCoder. Se distribuye bajo la licencia MIT incluida en el archivo `LICENSE`.