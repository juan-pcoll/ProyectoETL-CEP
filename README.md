# ProyectoETL-CEP
Dentro de este repositorio se encontrará todo el proyecto a desarrollar dentro de la clase de ETL

Evaluación del Índice de Pobreza Multidimensional en Colombia – 2023
Autores:
Juan Pablo Coll Muriel
Miguel Ángel Echeverry Fernández
Samuel Peña García

🎯 Objetivo del Proyecto
Este proyecto tiene como finalidad realizar una evaluación estadística y estructurada del Índice de Pobreza Multidimensional (IPM) en Colombia para el año 2023, utilizando datos oficiales del DANE.

Más allá del cumplimiento académico, esta iniciativa busca:
Transformar datos crudos en información estructurada y analítica.
Visualizar indicadores clave que permitan comprender la realidad social del país.
Aportar al análisis relacionado con los Objetivos de Desarrollo Sostenible (ODS), especialmente el ODS 1: Fin de la pobreza.
Facilitar que terceros puedan reutilizar esta información como base para investigaciones, análisis de políticas públicas o generación de conciencia social basada en datos.

Este proyecto demuestra cómo la ingeniería de datos puede convertirse en una herramienta poderosa para la comprensión de problemáticas estructurales.
Fuente de Datos

Los datos utilizados fueron obtenidos del Departamento Administrativo Nacional de Estadística (DANE).
Catálogo del estudio:
https://microdatos.dane.gov.co/index.php/catalog/824/study-description
Descarga de microdatos:
https://microdatos.dane.gov.co/index.php/catalog/824/get-microdata
Diccionario de variables:
https://microdatos.dane.gov.co/index.php/catalog/824/data-dictionary/F45?file_name=Personas%20%20(departamental)

Características del Dataset
Año: 2023
Nivel: Personas (departamental)
Formato original: .csv
Datos públicos y de libre uso
Variables codificadas (cada pregunta representada por un código)
Respuestas numéricas asociadas a categorías específicas
Preguntas mayoritariamente cerradas y de opción múltiple

Arquitectura del Proyecto
Se implementó un modelo Star Schema (Esquema en Estrella) diseñado en dbdiagram.io, compuesto por:

Tabla de hechos:
fact_persona

Tablas de dimensiones:
dim_demografia
dim_educacion
dim_salud
dim_tecnologia
dim_trabajo

Este diseño permite consultas eficientes y análisis optimizados en Power BI.

Tecnologías Utilizadas
Tecnología	Uso
Python	Desarrollo del proceso ETL
🗄 PostgreSQL	Base de datos relacional
🐘 pgAdmin	Administración de la base de datos
Power BI	Visualización y KPIs
Jupyter Notebook	Pruebas y validación
dbdiagram.io	Diseño del modelo dimensional
VS Code	Entorno de desarrollo
Flujo ETL

El pipeline sigue la arquitectura clásica:

1. Extract
Se cargan los datos crudos desde la carpeta data/raw.
Archivo principal:personas(departamental)2023-CEP.csv

2. Transform
Limpieza de datos
Conversión de tipos
Decodificación de variables categóricas
Creación de dimensiones
Normalización según el modelo estrella

3. Load
Conexión a PostgreSQL mediante SQLAlchemy
Creación de tablas
Inserción de datos transformados

Todo el flujo se ejecuta desde:
python - src/main.py

Estructura del Proyecto
PROJECT_1
│
├── .etl
├── .vscode
├── data
│   ├── processed
│   │   ├── dim_demografia.csv
│   │   ├── dim_educacion.csv
│   │   ├── dim_salud.csv
│   │   ├── dim_tecnologia.csv
│   │   ├── dim_trabajo.csv
│   │   └── fact_persona.csv
│   └── raw
│       └── personas(departamental)2023-CEP.csv
│
├── diagrams
├── sql
├── src
│   ├── analysis.py
│   ├── extract.py
│   ├── transform.py
│   ├── load.py
│   ├── log.py
│   └── main.py
│
├── visualizations
└── README.md

En la carpeta visualizations se almacenan las imágenes exportadas desde Power BI.

Guía de Ejecución
- Requisitos Previos

Asegúrese de tener instalado:
Python 3.10 o más recientes
PostgreSQL
pgAdmin
Power BI Desktop
VS Code (opcional pero recomendado)

- Paso 1: Clonar o descargar el proyecto
git clone <url-del-repositorio>

- Paso 2: Crear Base de Datos en PostgreSQL
Iniciar el servicio de PostgreSQL.
Abrir pgAdmin.
Crear una base de datos llamada: ods_pobreza

- Paso 3: Configurar conexión en main.py
Modificar la cadena de conexión:
engine = create_engine(
    "postgresql+psycopg2://usuario:contraseña@localhost:5432/ods_pobreza",
    connect_args={"client_encoding": "utf8"}
)

Reemplazar:
usuario
contraseña
puerto (si es diferente)
*recuerde que si también creó el database con otro nombre diferente a ods_pobreza, debe modificarlo.

- Paso 4: Ejecutar el ETL
Desde la raíz del proyecto:
python src/main.py
Si todo funciona correctamente, se generarán las tablas en PostgreSQL.

- Paso 5: Conectar Power BI
Abrir Power BI
Obtener datos → PostgreSQL
Servidor: localhost
Base de datos: ods_pobreza
Seleccionar tablas
Crear modelo relacional
Generar visualizaciones

Visualizaciones

En Power BI se desarrollaron:
KPIs comparativos

Las imágenes exportadas se encuentran en la carpeta:
/visualizations
