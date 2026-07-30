# Modelo Power BI de KPIs Comerciales

## Problema
Los equipos comerciales necesitan un dashboard confiable para monitorear ventas, ticket promedio y crecimiento por categoria y canal, con un modelo de datos bien disenado (no una hoja de calculo con formulas sueltas) que sea facil de mantener y de escalar.

## Solucion
Este repositorio documenta un modelo de datos en esquema estrella y un conjunto de medidas DAX para construir ese dashboard en Power BI, usando datos ficticios de un e-commerce (clientes, productos y ventas). Incluye los CSV de origen, las medidas DAX documentadas y la explicacion completa del modelo, para que el dashboard pueda reconstruirse de forma identica en Power BI Desktop.

**Nota importante:** Power BI Desktop es una aplicacion de escritorio y no puede operarse ni generarse un archivo .pbix desde el navegador. Por eso este repositorio no incluye un .pbix; en su lugar documenta todo lo necesario (datos, modelo y medidas) para que cualquiera pueda reconstruir el dashboard localmente siguiendo la guia de abajo.

Los datos utilizados son completamente ficticios y fueron creados unicamente con fines demostrativos.

## Tecnologias
- Power BI Desktop
- DAX (Data Analysis Expressions)
- Power Query (para la carga e importacion de los CSV)

## Estructura del repositorio
```
modelo-powerbi-kpis-comerciales/
├── README.md
├── data/
│   ├── clientes.csv
│   ├── productos.csv
│   └── ventas.csv
├── dax/
│   └── medidas.dax
└── docs/
    └── modelo_datos.md
```

## Como reconstruir el dashboard (paso a paso)
1. Abrir Power BI Desktop y seleccionar **Obtener datos > Texto/CSV**.
2. Importar los tres archivos de `data/`: `clientes.csv`, `productos.csv` y `ventas.csv`.
3. En la vista de **Modelado**, crear las relaciones:
   - `ventas[id_cliente]` -> `clientes[id_cliente]`
   - `ventas[id_producto]` -> `productos[id_producto]`
4. Crear la tabla `Calendario` con la formula DAX incluida en `dax/medidas.dax` (Modelado > Nueva tabla) y relacionarla con `ventas[fecha]`.
5. Copiar cada medida de `dax/medidas.dax` en una tabla de medidas dentro del modelo (Modelado > Nueva medida).
6. Construir las visualizaciones: tarjetas para Ventas Totales, Ticket Promedio y Clientes Activos; un grafico de lineas de Ventas Totales por mes; un grafico de barras de Participacion por Categoria; y una tabla de Clientes con Mas de una Compra.
7. Aplicar segmentadores (slicers) por canal, categoria y rango de fechas.

Para el detalle completo del modelo de datos (tablas, columnas y relaciones) ver [docs/modelo_datos.md](docs/modelo_datos.md).

## Resultado
Un dashboard de KPIs comerciales con visibilidad de ventas totales, ticket promedio, crecimiento interanual y participacion por categoria, construido sobre un modelo de datos limpio y documentado.

_(Espacio para captura de pantalla del dashboard una vez construido en Power BI Desktop)_
