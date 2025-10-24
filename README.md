# Arquitectura-de-Datos-
1 contactos_empleados 

Origen — se cargó la fuente (archivo/tabla).

Tipo cambiado — Power Query detectó tipos y aplicó cambios (texto, número, fecha).

Encabezados promovidos — la primera fila se convirtió en encabezado de columnas.

Rellenar hacia abajo — se rellenaron celdas vacías hacia abajo en alguna columna para completar valores repetidos.

Dividir columna por delimitador — alguna columna combinada (probablemente con varios datos en una celda) se dividió en varias columnas usando un delimitador (por ejemplo “,” o “;”).

Cambiar nombre de columnas generadas por la división (por ejemplo Combinada.1, Combinada.1.1).

Columna combinada insertada — se combinaron 2 o más columnas en una nueva (p. ej. para formar correo o teléfono).

Columnas quitadas — se eliminaron columnas intermedias no necesarias.

Valor reemplazado (varios pasos) — se reemplazaron ciertos valores problemáticos (por ejemplo 0, "O", celdas vacías, o texto como "N/A") por otro valor o por nulos.

Columnas reordenadas — se organizó el orden final de las columnas (Legajo, Nombre, Correo, Número, País).

Rename final — se renombraron columnas a nombres definitivos (Legajo, Nombre, Correo, Numero, Pais).

Objetivo/por qué: separar información combinada (correo/teléfono/país), limpiar valores inválidos, homogeneizar tipos y dejar la tabla lista para análisis.

2) contactos_clientes 


Tipo cambiado — detección y asignación de tipos.

Encabezados promovidos.

Tipo cambiado1 / 2 — ajustes adicionales de tipo tras operaciones intermedias.

Columna combinada insertada — se combinó o volvieron a combinar columnas (se observa Combinada.1 y Combinada.1.1).

Columnas quitadas — eliminación de columnas auxiliares de la combinación.

Valor reemplazado (varios) — limpieza de registros con valores 0 o O y reemplazo por formato adecuado (p. ej. "0" -> null o viceversa, según se requiera).

Dividir columna por delimitador — alguna columna (posiblemente dirección/telefono) fue dividida en partes.

Columnas reordenadas — ordenar columnas en la vista final (ID, NombreCompleto, correo, numero, pais).

Rename — renombrado final de columnas.

Objetivo: muy parecido al anterior — separar/componer campos de contacto, limpiar ceros/valores no válidos y dejar la tabla normalizada.

3) ventas_mensuales 


Tipo cambiado — números/texto detectados en columnas de meses.

Encabezados promovidos — la fila de meses se usa como encabezado.

Dividir columna por delimitador — se separaron columnas que venían combinadas o con formatos distintos.

Tipo cambiado1 / 2 / 3 — varios ajustes para asegurar que las columnas de mes tengan tipo numérico.

Columnas quitadas — se eliminaron columnas innecesarias (Column15, Column16 según la barra de fórmula).

Reemplazos / Limpieza — se cambiaron valores como N/A, -, textos no numéricos o celdas con formato $12 a un formato uniforme (probablemente eliminando símbolos $ y separadores).

Ajustes de formato numérico — dejar las columnas de cada mes como número entero o decimal para permitir agregaciones.

Objetivo: transformar una tabla en formato ancho (meses como columnas) con valores numéricos limpios listos para sumas/promedios y visualizaciones.

4) contactos_proveedores



Tipo cambiado.

Encabezados promovidos.

Valor reemplazado (varios) — limpieza de campos (por ejemplo reemplazar 0 por vacío o viceversa).

Columna combinada insertada y Dividir columna por delimitador — se combinó/partió datos (correo/telefono/pais) para colocar cada dato en su propia columna.

Columnas quitadas — quitar columnas auxiliares de la transformación.

Tipo cambiado final y Columnas reordenadas (Id, RazonSocial, Correo, Numero, Pais).

Renombrado de columnas (ej. Combinada.1.1 -> correo, Combinada -> numero, Combinada.1 -> pais) — esto aparece en la barra de fórmulas:
Table.RenameColumns(..., {{"Combinada.1.1","correo"},{"Combinada","numero"},{"Combinada.1","pais"}})

Objetivo: normalizar la información de proveedores separando teléfono/correo/país y estandarizando nombres de columnas.

5) ventas_ordenes 



Tipo cambiado.

Encabezados promovidos.

Dividir columna por delimitador — por ejemplo, separar campos combinados o columnas que contenían múltiples datos.

Valor reemplazado1 / 2 / 3 — limpieza de valores en la columna Total. En la barra se ve una fórmula:
Table.ReplaceValue(#"Valor reemplazado2"," ","0",Replacer.ReplaceText,{"Total"})
=> aquí se reemplazaron espacios en blanco por "0" en la columna Total.

Cambio de formato numérico — después de reemplazar se ajustó el tipo de Total a número o moneda.

Encabezados promovidos (posiblemente aplicado antes o después) y Columnas quitadas para eliminar datos intermedios.

Renombrado y reordenado — columnas finales: OrderID, CustomerID, FechaOrden, Total, Estado.

Objetivo: limpiar la columna Total (eliminar espacios, convertir a 0 donde no hay valor) y asegurar que esté en formato numérico para cálculos de ventas.

6) productos_erp


Tipo cambiado — los campos PrecioLista, Costo, SKU, etc. se detectaron y ajustaron.

Dividir columna por delimitador — separar columnas que vinieron concatenadas.

Valor reemplazado (varios pasos) — por ejemplo reemplazo No / no por Activo ó viceversa; en la barra aparece:
Table.ReplaceValue(#"Valor reemplazado6","No","no",Replacer.ReplaceText,{"Activo"}) o similar — indican normalización de valores booleanos/textuales de disponibilidad.

Columnas quitadas — eliminar información auxiliar o columnas intermedias.

Encabezados promovidos — si alguna fila fue promovida a encabezado.

Tipo cambiado final — asegurar PrecioLista, Costo como número; ProductID, Nombre como texto; SKU texto; Activo lógico/texto.

Orden final de columnas — ProductID, Nombre, Categoria, PrecioLista, Costo, SKU, Activo.

Objetivo: limpiar y estandarizar el catálogo de productos, uniformizar valores de estado (activo/inactivo) y preparar precios como numéricos.
