Desafío Práctico 2: Cubo OLAP y Data Warehouse (AdventureWorksDW2022)

Proyecto: Implementación y Explotación de un Cubo Multidimensional en SQL Server Analysis Services (SSAS)

Descripción del Proyecto

El objetivo principal es diseñar, implementar, procesar y explotar un modelo dimensional multidimensional (Cubo OLAP) a partir de la base de datos relacional de ejemplo AdventureWorksDW2022. El proyecto abarca desde la restauración de la base de datos en SQL Server hasta el consumo de métricas de negocio en tiempo real mediante una conexión en directo (Live Connection) desde Power BI Desktop.

Stack Tecnológico

Motor de Base de Datos Relacional: Microsoft SQL Server 2022

Entorno de Administración Relacional: SQL Server Management Studio (SSMS) v22.0.0

Base de Datos Origen: AdventureWorksDW2022 (Esquema en estrella)

Motor OLAP: SQL Server Analysis Services (SSAS) Multidimensional

Entorno de Desarrollo: Visual Studio 2026 (SQL Server Data Tools / SSAS Extension)

Visualización e Inteligencia de Negocios: Power BI Desktop

Arquitectura y Diseño Multidimensional

1. Esquema del Data Warehouse

El modelo se basa en un esquema en estrella compuesto por:

Tabla de Hechos: FactInternetSales (núcleo transaccional).

Dimensiones: DimDate, DimCustomer, DimProduct, DimSalesTerritory.

2. Estructuración de la Dimensión de Tiempo (DimDate)

Jerarquía Personalizada (Calendar Hierarchy): Calendar Year ➡️ Calendar Semester ➡️ English Month Name ➡️ Full Date Alternate Key.

Relaciones de Atributos: Ajustadas como rígidas (Rigid) para mantener la consistencia cronológica y la agregación jerárquica.

Roles Múltiples de Dimensión (Role-Playing Dimensions): Reutilización de DimDate para tres funciones independientes dentro de la tabla de hechos:

Order Date (OrderDateKey)

Due Date (DueDateKey)

Ship Date (ShipDateKey)

3. Medidas Cuantitativas Configuradas

Order Quantity (Cantidad de unidades vendidas)

Sales Amount (Importe total de ventas)

Unit Price (Precio unitario)

Total Product Cost (Costo total del producto)

Pasos para Replicar el Proyecto

Paso 1: Restauración de la Base de Datos

Descargar el archivo de respaldo AdventureWorksDW2022.bak.

Conectarse a la instancia de SQL Server mediante SSMS (localhost).

Ejecutar la restauración seleccionando la opción WITH REPLACE.

Paso 2: Configuración e Implementación en SSAS

Abrir la solución CuboAdventure.sln en Visual Studio.

Comprobar la conexión del Data Source apuntando al servidor de SQL Server.

Verificar la Data Source View (DSV) con la tabla de hechos y dimensiones.

Hacer clic derecho sobre el proyecto CuboAdventure y seleccionar Deploy (Implementar).

Procesar la base de datos multidimensional (Process Full).

Paso 3: Explotación y Visualización en Power BI

Abrir Power BI Desktop.

Seleccionar Obtener datos ➡️ Base de datos de SQL Server Analysis Services.

Ingresar la dirección del servidor (PCLAP\SQLEXPRESS) y marcar Conectar en directo (Live Connection).

Seleccionar el cubo CuboVentasInternet.

Arrastrar las medidas (Sales Amount, Order Quantity) y la jerarquía de calendario para generar tableros analíticos.

Visualización de Indicadores en Power BI

La integración directa permite la consulta analítica al vuelo de los indicadores clave de rendimiento:

Distribución de Pedidos por Año (Order Quantity): Análisis porcentual de transacciones, destacando la concentración en el período 2013 (87.42%).

Tendencia Histórica de Ventas (Sales Amount): Evolución financiera interanual que refleja picos de demanda y comportamiento comercial.

Estructura del Repositorio

├── CuboAdventure/                  # Proyecto Multidimensional de Analysis Services (Visual Studio)
│   ├── CuboAdventure.dwproj
│   ├── Dim Date.dim
│   ├── Dim Customer.dim
│   ├── Dim Product.dim
│   ├── Dim Sales Territory.dim
│   ├── CuboVentasInternet.cube
│   └── AdventureWorksDW2022.dsv
├── Reportes/                       # Tableros e imágenes de prueba en Power BI
└── README.md                       # Documentación principal del proyecto

