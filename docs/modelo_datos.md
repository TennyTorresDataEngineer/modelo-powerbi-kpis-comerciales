# Modelo de datos

## Tipo de modelo
Esquema en estrella (star schema): una tabla de hechos (`ventas`) conectada a tres dimensiones (`clientes`, `productos`, `Calendario`).

## Tablas

### ventas (hechos)
Granularidad: una fila por venta individual.

| Columna | Tipo | Descripcion |
|---|---|---|
| id_venta | Entero | Identificador unico de la venta |
| fecha | Fecha | Fecha en que ocurrio la venta |
| id_cliente | Entero | Llave foranea hacia clientes |
| id_producto | Entero | Llave foranea hacia productos |
| canal | Texto | Marketplace, Web Propia o Redes Sociales |
| cantidad | Entero | Unidades vendidas en esa transaccion |

### clientes (dimension)
| Columna | Tipo | Descripcion |
|---|---|---|
| id_cliente | Entero | Llave primaria |
| nombre | Texto | Nombre del cliente (ficticio) |
| ciudad | Texto | Ciudad de residencia |
| segmento | Texto | Consumidor Final o Pyme |
| fecha_registro | Fecha | Fecha de alta del cliente |

### productos (dimension)
| Columna | Tipo | Descripcion |
|---|---|---|
| id_producto | Entero | Llave primaria |
| nombre | Texto | Nombre del producto |
| categoria | Texto | Tecnologia, Hogar, Moda o Belleza |
| precio_unitario | Decimal | Precio unitario en pesos ficticios |

### Calendario (dimension, generada con DAX)
Se genera directamente en Power BI con la funcion `CALENDAR`/`ADDCOLUMNS` (ver `dax/medidas.dax`) en lugar de importarse como CSV, para asegurar una linea de tiempo continua sin huecos, con columnas de anio, mes, trimestre y dia de la semana.

## Relaciones
- `ventas[id_cliente]` (muchos) -> `clientes[id_cliente]` (uno)
- `ventas[id_producto]` (muchos) -> `productos[id_producto]` (uno)
- `ventas[fecha]` (muchos) -> `Calendario[Date]` (uno)

Todas las relaciones son de una direccion (single direction), desde las dimensiones hacia la tabla de hechos, siguiendo la practica estandar de modelado en Power BI.

## Por que este diseno
Separar hechos de dimensiones permite que las medidas DAX (ver `dax/medidas.dax`) se calculen de forma eficiente y que el modelo escale si se agregan mas tablas de hechos en el futuro (por ejemplo, devoluciones o metas comerciales).
