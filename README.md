# Café Origen: motor de analítica v0.1

Proyecto de análisis de una muestra de 12 ventas de Café Origen. El motor calcula indicadores, agrupa resultados y presenta un informe legible en la consola con Node.js, sin dependencias externas.

## Requisitos

- Node.js LTS

## Ejecutar el reporte

Desde la raíz del proyecto, ejecuta:

```sh
node src/reporte.js
```

El informe muestra el resumen general, las ventas por ciudad, las unidades por producto y los tres productos con mayor valor vendido. También compara un día con ventas con uno sin ventas.

## Verificar los cálculos

```sh
node src/verificar.js
```

El proceso termina con código distinto de cero si alguna comprobación falla.

## Explorar los datos

```sh
node src/explorar.js
```

El script muestra el número de registros, el primero y el último, el producto del registro en la posición 4 y la tabla completa. La estructura de los datos, los casos borde y la bitácora de depuración están en [bitacora.md](./bitacora.md).

## Medir operaciones

```sh
node src/medir.js
```

El script genera historiales de 100, 1.000, 10.000 y 100.000 ventas y muestra en una tabla las operaciones contadas para cada función. Las predicciones, los resultados y su análisis Big O están en [bitacora.md](./bitacora.md).

## Medir tiempos de clientes recurrentes

```sh
node src/tiempos.js           # n = 1.000, 2.000, 4.000, 8.000 y 16.000, y estimaciones
node src/tiempos.js 100000    # además ejecuta 100.000 si la estimación es menor a 2 minutos
node src/costoOculto.js       # cuenta comparaciones y el trabajo oculto de includes
```

`tiempos.js` mide `clientesRecurrentes` con `console.time` / `console.timeEnd` y estima su tiempo para 100.000 y 1.000.000 de ventas. `costoOculto.js` compara datos típicos con un peor caso construido. La tabla de tiempos, las estimaciones y el diagnóstico están en [bitacora.md](./bitacora.md).

## Comparar memoria: cadena de métodos frente a una pasada

```sh
node src/espacio.js
```

Compara `totalCiudadCadena` (map, filter, map y reduce) con `totalCiudadUnaPasada` (un solo `for...of`). Verifica que dan el mismo valor con 10.000 ventas, cuenta los recorridos y los arreglos intermedios, mide tiempos y ejecuta las dos con 1.000.000 de ventas bajo distintos límites de memoria. La clasificación espacial del motor y la decisión final están en [bitacora.md](./bitacora.md).

## Preguntas que responde

- ¿Cuánto se vendió en total y cuál fue el ticket promedio?
- ¿Cuántas unidades se vendieron por producto?
- ¿Cuánto vendió cada ciudad, agrupando variantes de mayúsculas y espacios?
- ¿Qué tres productos generaron más valor?
- ¿Cuáles fueron las ventas, unidades y ticket promedio de una fecha determinada?