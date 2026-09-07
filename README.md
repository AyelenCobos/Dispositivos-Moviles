# ParkRide — Backend (FastAPI)

Configuración inicial del backend del proyecto **ParkRide**, basada en la
ficha técnica (Actividad Fundamental 1, Ingeniería de Dispositivos Móviles).

## Estructura

```
parkride_backend/
├── app/
│   ├── main.py            # Punto de entrada de FastAPI
│   ├── database.py         # Conexión a la base de datos (SQLite por defecto)
│   ├── models.py            # Tablas SQLAlchemy: Usuarios, Vehiculos, Nodos_Ubicacion, Viajes, Transacciones
│   ├── schemas.py           # Esquemas Pydantic (request/response)
│   ├── matching.py          # Algoritmo de emparejamiento (sección 5 de la ficha técnica)
│   └── routers/
│       ├── usuarios.py
│       ├── vehiculos.py
│       ├── nodos.py
│       ├── viajes.py
│       └── transacciones.py
└── requirements.txt
```

## Instalación

```bash
python -m venv venv
source venv/bin/activate      # En Windows: venv\Scripts\activate
pip install -r requirements.txt
```

## Ejecución

```bash
uvicorn app.main:app --reload
```

La API queda disponible en `http://127.0.0.1:8000` y la documentación
interactiva (Swagger) en `http://127.0.0.1:8000/docs`.

Por defecto usa una base de datos SQLite local (`parkride.db`) para que
corra sin configuración adicional. Para usar PostgreSQL o MySQL (como
indica la ficha técnica), define la variable de entorno `DATABASE_URL`
antes de levantar el servidor, por ejemplo:

```bash
export DATABASE_URL="postgresql://usuario:password@localhost:5432/parkride"
```

y descomenta el driver correspondiente en `requirements.txt`.

## Endpoints incluidos (MVP)

- `POST /usuarios/` · `GET /usuarios/` · `GET /usuarios/{id}`
- `POST /vehiculos/` · `GET /vehiculos/`
- `POST /nodos/` · `GET /nodos/`
- `POST /viajes/` (ejecuta el algoritmo de emparejamiento) · `GET /viajes/` · `GET /viajes/{id}` · `PATCH /viajes/{id}/finalizar`
- `POST /transacciones/` · `GET /transacciones/`

## Pendiente para siguientes entregas

- Autenticación contra la base de datos de RH (número de nómina).
- Mapeo real de distancias entre nodos para el ETA y la "cercanía de nodos".
- Cálculo dinámico del costo en créditos por ruta (actualmente es un valor fijo).
- Módulo ESG (cálculo de CO₂ ahorrado y recompensas verdes).
- Migraciones con Alembic en vez de `create_all`.
