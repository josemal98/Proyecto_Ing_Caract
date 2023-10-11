# Proyecto Red de Banco de Alimentos de México
Este proyecto es parte del curso "Ingeniería de Características" de la Maestría en Ciencia de Datos de la Universidad de Sonora. Su motivación principal es contribuir a la Red de Bancos de Alimentos de México (red BAMX) mediante el análisis de datos públicos relacionados con la producción y el mercado de alimentos a nivel nacional. El objetivo final es realizar el "Storytelling" que permita a la red BAMX identificar ventanas de oportunidad para optimizar sus procedimientos en la colecta y redistribución de alimentos.

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/8ba0f5ef-dbdc-46b7-9885-734aa5250be1" alt="Descripción de la imagen" width="40%" height="40%">
</p>

<p align="center">
  <em>Figura 1: Logo de la red del Banco de Alimentos de México.</em>
</p>

## Integrantes del equipo

- José Carlos Barreras Maldonado
- Luis Ernesto Ortíz Villalón
- Vesna Camile Pivac Alcaraz

## Descripción del proyecto

El proyecto se divide en tres partes fundamentales:

**1. Obtención de los datos**

El objetivo de esta fase es la identificación y descarga de los datos necesarios de fuentes públicas y confiables. Esto se lleva a cabo de manera programática, para que cualquier persona pueda replicar la descarga simplificadamente por medio de líneas de código. El resultado final son los datos sin ningún tipo de procesamiento, pero organizados de manera *tidy*. Esto se refiere a que los datos cumplen con las condiciones de que cada columna sea una variable y cada fila una observación.

**2. Preparación de los datos**

Esta etapa se enfoca en la transformación y acondicionamiento de los datos adquiridos para su posterior análisis. Los datos obtenidos en la etapa anterior pueden presentar inconsistencias, formatos no adecuados, valores faltantes o valores atípicos. Para garantizar la fiabilidad y la utilidad de estos, se realizan las siguientes acciones:

* *Limpieza de datos:* Se identifican y corrigen inconsistencias en los valores, eliminando datos duplicados o erróneos.
  
* *Estandarización de formatos:* Se asegura que los datos sigan un formato coherente y que los tipos de datos sean apropiados para su análisis.
  
* *Manejo de valores faltantes:* Se abordan los valores faltantes de manera adecuada, ya sea rellenándolos con estimadores o eliminando registros incompletos, dependiendo del impacto en el análisis.

* *Manejo de valores atípicos:* Se aplican técnicas estadísticas para identificar y se decidir cómo tratarlos, ya sea corrigiéndolos, transformándolos o manteniéndolos según su relevancia para la historia que se narra con los datos.
  
**3. Visualización de los datos**

En esta parte del proyecto se da vida a los datos a través de gráficos y representaciones visuales. La información recopilada se presenta de manera efectiva en un *dashboard* interactivo que facilita la identificación de patrones, tendencias y áreas de interés. Estas visualizaciones ayudan a contar la historia que se encuentra en los datos, proporcionando una visión clara y accesible para la red BAMX.

Las visualizaciones se diseñan metodológicamente para destacar aspectos relevantes de la producción y el mercado de alimentos a nivel nacional. Este proceso permite identificar oportunidades significativas que podrían beneficiar a la red BAMX en la optimización de sus procedimientos de recolección y redistribución de alimentos.

```mermaid
graph TD;

subgraph 3. Visualización de los datos
  H[Creación de gráficos y visualizaciones] --> I[Dashboard interactivo]
end

subgraph 2. Preparación de los datos
  D[Limpieza de datos] --> E[Estandarización de formatos]
  E --> F[Manejo de valores faltantes]
  F --> G[Manejo de valores atípicos]
end

subgraph 1. Obtención de los datos
  A[Identificación de fuentes públicas y confiables] --> B[Descarga programática de datos]
  B --> C[Organización tidy de datos]
end

```

<p align="center">
  <em>Figura 2: Descripción de las 3 etapas que conforman el proyecto.</em>
</p>

## 1. Obtención de los datos

### SIAP

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/5700c3a8-2af7-4959-9fe5-5c077a110d59" alt="Descripción de la imagen" width="50%" height="50%">
</p>

<p align="center">
  <em>Figura 3: Fuente de información de producción agroalimentaria SIAP.</em>
</p>

La principal fuente para la obtención de datos relacionados con la producción de alimentos en el campo es el Servicio de Información Agroalimentaria y Pesquera (SIAP). A esta plataforma se puede acceder por medio del siguiente [enlace](https://www.gob.mx/siap). Dentro de los datos de relevancia proporcionados por esta fuente se encuentran las hectareas de cultivo sembrada, cosechada y siniestrada, junto con su respectiva producción y rendimiento. Desde la perspectiva geográfica, la plataforma ofrece al usuario la posibilidad de solicitar estos datos para todos los municipios de cada estado. Por otro lado, la resolución temporal mínima permitida se basa en reportes con los avances mensuales de cada año. 

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/997573d9-8af2-45d0-a214-8fefae6d94e7" alt="Descripción de la imagen" width="60%" height="60%">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/80ca30fb-1769-4cb8-b6a0-e5c381c4dbcc" alt="Descripción de la imagen" width="60%" height="60%">
</p>

<p align="center">
  <em>Figura 4: Ejemplo de filtros y datos obtenidos directamente en la plataforma SIAP.</em>
</p>

Para la adquisición programática de los datos, es necesario realizar un *request* al *endpoint* [https://nube.siap.gob.mx/avance_agricola/](https://nube.siap.gob.mx/avance_agricola/). Como resultado, se obtiene una cadena de texto en formato XML que contiene una tabla equivalente a la mostrada en la figura, pero cuyo contenido depende de los identificadores (ID's) proporcionados en el *request*. Es importante mencionar que estos ID no están disponibles directamente en la plataforma, por lo que fue necesario manipular los filtros para su obtención. Una vez adquiridos, los ID's fueron almacenados en un JSON, el cual fue añadido al presente repositorio (Victor-dict.json). Para la obtención de los datos de las cadenas de texto con formato XML es necesario aplicar un *parsing* utilizando BeautifulSoup, de modo que se facilite la identificación y extracción del contenido de cada una de las celdas. 

Dado que el interés principal es obtener datos mensuales de cada cultivo desde 2018 hasta el presente año, el siguiente paso consistió en repetir este proceso anidadamente para los ID de años, meses y cultivos de interés. En cada iteración, el contenido de la tabla correspondiente a un mes de un año en particular se almacenó en un archivo CSV en la carpeta "raw" del presente repositorio, siguiendo el formato: "Avance_Agricola_año_mes.csv". A estos datos se la añade una columna "Cultivo", cuyo valor indica el cultivo al que se refieren los datos. En total, al tratarse de 6 años y 12 meses, se obtuvo un apróximado de 72 archivos (en realidad son menos porque el 2023 está incompleto). Posteriormente, estos archivos locales se volvieron a cargar en el entorno de programación para organizarlos de manera *tidy*. Esto implicó combinarlos en un único dataframe al que se le agregaron columnas para "año" y "mes". Debido a su tamaño (992213 filas con 10 columnas), este DataFrame se almacena en un archivo parquet, el cual fue añadido al repositorio. 

Como nota, es necesario mencionar que no se iteró sobre las categorías de los filtros de Riego y Modalidad. En su lugar, en ambos casos se empleó la categoría que abarca a todas las otras.  


#### Dataframe tidy

A continuación se muestra una descripción del DataFrame *SIAP* que resultó de la descarga y organización de los datos, el cual fue almacenado en formato parquet.

##### Información general

- **Nombre del DataFrame:** SIAP.parquet
- **Número de filas:** 992213
- **Número de columnas:** 10

##### Columnas

A continuación, se muestra una lista de las columnas en el DataFrame *tidy*, junto con una breve descripción de cada una:

| **Columna**          | **Descripción**                                    | **Unidad** |
|----------------------|----------------------------------------------------|------------|
| Entidad              | Entidad a la que pertenece el dato                 |            |
| Municipio            | Nombre del municipio al que pertenece el dato     |            |
| Superficie Sembrada  | Superficie destinada a la siembra (hectareas)      | Hectarea  |
| Superficie Cosechada | Superficie cosechada                 | Hectarea |
| Superficie Siniestrada| Superficie siniestrada                 | Hectarea |
| Produccion           | Cantidad de producción         | Unidad de medida |
| Rendimiento          | Rendimiento del cultivo | Unidad de medida / hectarea |
| Anio                 | Año en el que se registraron los datos            |            |
| Mes                  | Mes en el que se registraron los datos            |            |
| Cultivo              | Tipo de cultivo                                    |            |



Aquí hay una muestra de cinco filas seleccionadas aleatoriamente del DataFrame para que se tenga una idea de cómo se ven los datos:

| Index | Entidad   | Municipio       | Superficie Sembrada | Superficie Cosechada | Superficie Siniestrada | Produccion | Rendimiento | Anio | Mes       | Cultivo                |
|-------|-----------|-----------------|----------------------|------------------------|-------------------------|------------|------------|------|-----------|------------------------|
| 949223  | Zacatecas | Pinos                | 10.50                | 8.00                   | 2.5                    | 169.60     | 21.20      | 2018 | Septiembre | Cebolla                |
| 512503  | Yucatán   | Temozón              | 1.50                 | 1.50                   | 0.0                    | 28.00      | 18.67      | 2020 | Marzo      | Chile verde            |
| 659064  | Veracruz  | Tlalixcoyan          | 416.00               | 200.00                 | 0.0                    | 1,300.00   | 6.50       | 2019 | Enero     | Limón                  |
| 672054  | Puebla    | Atzitzihuacán        | 20.00                | 10.00                  | 0.0                    | 41.00      | 4.10       | 2019 | Febrero   | Maíz grano            |
| 130789  | Coahuila  | Lamadrid             | 55.00                | 0.00                   | 0.0                    | 0.00       | 0          | 2022 | Enero     | Avena forrajera en verde|

### SNIIM

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/b75332c5-bf56-4094-a018-8dd07a9201fd" alt="Descripción de la imagen" width="40%" height="40%">
</p>

<p align="center">
  <em>Figura 5: Fuente de información de mercado SNIIM</em>
</p>

Para la obtención de datos de mercado de los distinto producto agrícolas a lo largo del territorio nacional recurrimos al Sistema Nacional de Información e Integración de Mercados o SNIIM. El SNIIM es un servicio proporcionado por la Secretaría de Economía que se enfoca en brindar información sobre el comportamiento de los precios al por mayor de productos agrícolas, pecuarios y pesqueros en los mercados nacionales e internacionales. Se puede acceder a esta plataforma por medio del siguiente [enlace](http://www.economia-sniim.gob.mx/nuevo/Home.aspx). 

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/7195da21-4b0c-4f63-9fce-a643efacd8d8" alt="Descripción de la imagen" width="70%" height="70%">
</p>

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/cb618216-c380-4480-ab30-047d552fe268" alt="Descripción de la imagen" width="70%" height="70%">
</p>

<p align="center">
  <em>Figura 6: Ejemplo de filtros y datos obtenidos directamente en la plataforma SNIIM</em>
</p>

La obtención de datos del  SNIIM se realiza mediante una clase "ScrapperMarketAgriculture" especializada en *web scraping* que automatiza el proceso. Esta clase gestiona las bibliotecas necesarias, como requests y BeautifulSoup, para realizar solicitudes web y analizar los resultados de estas solicitudes. En este caso, la solicitud a [http://www.economia-sniim.gob.mx/NUEVO/Consultas/MercadosNacionales/PreciosDeMercado/Agricolas](http://www.economia-sniim.gob.mx/NUEVO/Consultas/MercadosNacionales/PreciosDeMercado/Agricolas) arroja un HTML que contiene una tabla equivalente a la mostrada en la figura para un cultivo particular. Esta tabla contiene la información histórica de precios del cultivo en los distintas parejas de mercado de origen-destino de todo México. Tal como en los datos del SIAP, estamos interesados en el periodo que va del 2018 al presente. Aunque el periodo de tiempo entre dos instancias subsecuentes es variable, por lo general este es de varios días.

Cada producto de interés se trata como una instancia de esta clase, lo que permite una gestión controlada del proceso. En cada una de estas instancias se realiza un *parsing* con BeautifulSoup, a partir del cual se puede extraer el contenido de cada una de las celdas de la tabla. Este contenido se almacena en un DataFrame temporal. A su vez, este DataFrame se guarda en un archivo CSV cuyo nombre sigue el formato: "sniim_product_cultivo_calidad.csv". Estos archivos fueron añadidos la carpeta "raw" del presente repositorio. 

Por último, la transformación de estos datos a un formato *tidy* implicó cargar y concatenar todos los archivos CSV. Tal como con los datos del SIAP, este nuevo DataFrame *tidy* se guardó en formato parquet, y se añadió al presente repositorio. 

#### DataFrame tidy

A continuación se muestra una descripción del DataFrame *SNIIM* que resultó de la descarga y organización de los datos, el cual fue almacenado en formato parquet.

##### Información general

- **Nombre del DataFrame:** SNIIM.parquet
- **Número de columnas:** 9

##### Columnas

A continuación, se muestra una lista de las columnas en el DataFrame *tidy*, junto con una breve descripción de cada una:
| **Columna**    | **Descripción**                                  |
|--------------  |--------------------------------------------------|
| Fecha         | Fecha de los registros de precios                |
| Presentacion  | Tipo de presentación del producto                |
| Origen        | Origen del producto                              |
| Destino       | Destino del producto                             |
| Precio_min    | Precio mínimo del producto                       |
| Precio_max    | Precio máximo del producto                       |
| precio_frec   | Precio frecuente del producto                    |
| Observacion   | Observación sobre los registros                  |
| Cultivo       | Nombre del cultivo                               |

Aquí hay una muestra de cinco filas seleccionadas aleatoriamente del DataFrame para que se tenga una idea de cómo se ven los datos:

| Index |   Fecha   | Presentacion          | Origen                    | Destino         | Precio_min | Precio_max | precio_frec | Observacion      | Cultivo            |
|-------|------------|-----------------------|-------------------------- |-----------------|------------|------------|------------ |----------------- |------------------- |
| 123232 | 11/11/2020 | Manojo                | Baja California           | Baja California Sur: Unión de Comerciantes de ...  | 3.0       | 7.00       | 7.00         | nan             | cilantro_primera   |
| 92619   | 19/11/2019 | Rollo de 20 pzas.      | Jalisco                   | Nuevo León: Mercado de Abasto "Estrella" de Sa... | 6.5       | 7.50       | 6.50         | nan             | caña_primera       |
| 136301 | 11/05/2018 | Caja de 10 kg.         | Importación               | Durango: Central de Abasto "Francisco Villa"   | 62.0      | 62.00      | 62.00         | Origen U.S.A.    | ciruela pasa_primera |
| 124224 | 24/05/2021 | Manojo                | Baja California           | Baja California Sur: Unión de Comerciantes de ...  | 3.0       | 7.00       | 5.00         | nan             | cilantro_primera   |
| 15799   | 09/11/2018 | Caja de 20 kg.         | Aguascalientes            | Nayarit: Mercado de abasto 'Adolfo López Mateo...  | 32.0      | 33.25      | 32.25         | nan             | aguacate pagua_primera |

