# Análisis de tiempos de entrega en entornos de E-Commerce

## Descripción general
Olist es una tienda departamental en línea de Brasil, esta se conecta con vendedores y pequeños negocios para lograr sus ventas. 

Entre los detalles que se encuentran al realizar los envíos, es que no todos llegan a la misma rapidez, no es el mismo tiempo que se hace en una ciudad más grande que en un pueblo en la amazonas, además de podría influir en las reseñas de los usuarios, las principales categorías más vendidas, y qué metodos de pago son populares.

## Archivos

En el archivo se cuentan con 9 datasets que cuentan con la información de cada acción, clientela, reseñas, entre otras.

| Dataset | Descripción |
|---|---|
| `olist_customers_dataset` | Información sobre los clientes y su ubicación |
| `olist_geolocation_dataset` | Códigos postales de Brasil y coordenadas |
| `olist_order_items_dataset` | Datos de los artículos comprados de cada orden |
| `olist_order_payments_dataset` | Información sobre las opciones de pago |
| `olist_order_reviews_dataset` | Reseñas hechas por los clientes, se realizan una vez que se compra el producto |
| `olist_orders_dataset` | El dataset principal con toda la información |
| `olist_products_dataset` | Información sobre los productos vendidos |
| `olist_sellers_dataset` | Datos sobre los vendedores que realizaron las ordenes, en la cual se encuentra su ubicación e identificación del producto vendido |
| `product_category_name_translation` | Dataset con los datos de `product_category_name` pero en inglés |

## Metodologías y herramientas

Para el desarrollo del proyecto, se requirió de las librerías de `pandas`, `matplotlib`, y `SQLite` para la ejecucipon de entornos.

Las metodologías usadas son el análisis exploratorio, para identificar las diferencias de cada venta, limpieza y manipulación de datos para una mejor comprensión y evitar malinterpretaciones, y consultas con SQL para el estudio de pruebas.

## Hallazgos y recomendaciones

Durante el desarrollo, se han encontrado algunos rasgos interesantes:

### Tiempos de entrega
- Roraima `RR` es el estado con **entregas más lentas (29.4 días)**, le siguen Amapá `AP` (27.2 días), Amazonas `AM` (26.4 días), Alagoas `AL` (24.5 días) y Paraíba `PA` (23.8 días). Sao Paulo `SP` es el más rápido con 8.8 días.
- Roraima `RR`, Amapá `AP` y Amazonas `AM` tienen estimaciones de más de 45 días y márgenes de 17 a 19 días: son lentos, pero la promesa es muy holgada, y el margen varía mucho. Por ende, **Todos los estados llegan en promedio antes de lo estimado**
- **Donde se rompe la promesa es en Alagoas `AL` (21.4% de pedidos tarde), Maranhão `MA` (17.4%) y Sergipe `SE` (15.2%).** Tienen tiempos medianos y estimaciones ajustadas, con márgenes de apenas 8 a 9 días. Son los estados que más se benefician de una mejora logística.
- **Río de Janeiro `RJ`** tiene 12.1% de pedidos tarde, alto para un estado con entregas relativamente rápidas y mucho volumen.
- **Limitación:** Roraima `RR` (41 pedidos), Amapá `AP` (67) y Acre `AC` (80) tienen muestras pequeñas; sus promedios son poco estables.

### Categorías 
- `health_beauty` (1.23 M), `watches_gifts` (1.17 M) y `bed_bath_table` (1.02 M) encabezan el ranking como las **Categorías con más ingresos:** .
- `bed_bath_table` (9,272 pedidos) es la primera, seguida de health_beauty (8,647) y sports_leisure (7,530). en cuanto a volúmen
- `watches_gifts` es 2.ª en ingresos pero 7.ª en volumen (5,495 pedidos), por su ticket alto. `bed_bath_table` es 1.ª en volumen pero 3.ª en ingresos, en la que se ve un **Contraste de ticket:**
- **Limitación:** 1,537 ítems (1,392 pedidos) no tienen categoría; suman 170,727 en ingresos y quedan agrupados como `sin_categoria`.

### Reseñas
- Los pedidos a tiempo tienen un score promedio de **4.29** (9.2% de reseñas de 1 o 2 estrellas); los tardíos, **2.27** (62.4%).
- La caída **crece con el retraso**: 3.29 con 1 a 3 días, 2.11 con 4 a 7 días y 1.70 con más de 7 días.
- Solo el 6.8% de los pedidos llega tarde, así que el problema es concentrado y atacable.
- Es una **asociación, no prueba causalidad**: otros factores (calidad del producto, por ejemplo) también pueden influir.

### Métodos de pago
- **Tarjeta de crédito** es la más populas, domina con 76,505 pedidos (76.9%) y es el único método con cuotas (3.5 en promedio).
- **Boleto** es el segundo (19.9%), seguido por voucher (3.9%) y tarjeta de débito (1.5%).
- Los porcentajes suman más de 100% porque un pedido puede combinar métodos (por ejemplo, tarjeta más voucher).
- `not_defined` (3 registros) se trata como anomalía y se excluye de la gráfica.

Las recomendaciones paraEnfocar en mejorar la logística en los estados en que se entrega lento, así como incentivar los diversos métodos de pago, sin descuidar los pagos con tarjeta de crédito y enfocar en los productos que más se venden, y los que no se venden tanto, realizar temporada de ofertas para aumentar las ventas.