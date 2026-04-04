# ESP32-WEB

Servidor web en Python para visualizar datos enviados desde un ESP32.

## Descripción

Este proyecto monta un dashboard web con Flask que recibe datos de sensores (`AX`, `AY`, `AZ` y `EMG`) y los muestra en una tabla y en gráficas dinámicas. También permite generar un PDF con el historial de lecturas y borrar los datos almacenados en memoria.

## Tecnologías

- Python 3.11+
- Flask
- Flask-CORS
- ReportLab
- Chart.js (desde CDN)

## Características

- Panel web en `templates/index.html`
- Actualiza datos en tabla y gráficas (`AX`, `AY`, `AZ`)
- Descarga un reporte en PDF con el historial
- Borra los datos en memoria
- Endpoints REST para envío y consulta de datos

## Instalación

1. Crear y activar entorno virtual:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

2. Instalar dependencias:

```powershell
pip install -r requirements.txt
```

## Ejecución

Configura la variable de entorno para Flask y ejecuta el servidor:

```powershell
$env:FLASK_APP = "app.py"
python -m flask run --host=0.0.0.0 --port=5000
```

Luego abre en el navegador:

```text
http://127.0.0.1:5000/
```

> Nota: los datos se almacenan en memoria mientras el servidor está activo. Al reiniciar el servidor, el historial se pierde.

## Endpoints

- `GET /` - Dashboard principal
- `POST /update` - Añade un nuevo registro de datos en formato JSON
- `GET /data` - Devuelve el historial completo en JSON
- `POST /clear-data` - Elimina todos los datos almacenados
- `GET /download-pdf` - Genera y descarga un PDF con el historial

### Formato esperado para `/update`

```json
{
  "ax": 0.0,
  "ay": 0.0,
  "az": 0.0,
  "emg": 0.0
}
```

## Estructura de archivos

- `app.py` - Aplicación Flask y lógica de endpoints
- `requirements.txt` - Dependencias del proyecto
- `pyproject.toml` - Metadatos del proyecto
- `templates/index.html` - Interfaz web principal
- `static/script.js` - Lógica del panel y actualización de datos

## Uso esperado

1. El ESP32 o cualquier cliente envía datos a `POST /update`.
2. La web consulta `GET /data` para mostrar la información.
3. El usuario puede descargar el reporte en PDF o borrar los datos actuales.
