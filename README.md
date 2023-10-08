# Proyecto Red de Banco de Alimentos de México
Este proyecto es parte del curso "Ingeniería de Características" de la Maestría en Ciencia de Datos de la Universidad de Sonora. Su motivación principal es contribuir a la Red de Bancos de Alimentos de México (red BAMX) mediante el análisis de datos públicos relacionados con la producción y el mercado de alimentos a nivel nacional. El objetivo final es "contar una historia con los datos" que permita a la red BAMX identificar ventanas de oportunidad para optimizar sus procedimientos en la colecta y redistribución de alimentos.

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/8ba0f5ef-dbdc-46b7-9885-734aa5250be1" alt="Descripción de la imagen">
</p>

<p align="center">
  <em>Figura 1: Red del Banco de Alimentos de México.</em>
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

## Primera parte: obtención de los datos

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/5700c3a8-2af7-4959-9fe5-5c077a110d59" alt="Descripción de la imagen">
</p>

<p align="center">
  <em>Figura 2: Fuente de información de producción agroalimentaria SIAP.</em>
</p>

La principal fuente para la obtención de datos relacionados con la producción de alimentos en el campo es el Servicio de Información Agroalimentaria y Pesquera (SIAP). A esta plataforma se puede acceder por medio del siguiente [enlace](https://www.gob.mx/siap). Dentro de los datos de relevancia proporcionados por esta fuente se encuentran las hectareas de cultivo sembrada, cosechada y siniestrada, junto con su respectiva producción y rendimiento. Desde la perspectiva geográfica, la plataforma ofrece al usuario la posibilidad de solicitar estos datos para todos los municipios de cada estado. Por otro lado, la resolución temporal mínima permitida se basa en reportes con los avances mensuales de cada año. 

<p align="center">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/997573d9-8af2-45d0-a214-8fefae6d94e7" alt="Descripción de la imagen">
  <img src="https://github.com/josemal98/Proyecto_Ing_Caract/assets/90294947/80ca30fb-1769-4cb8-b6a0-e5c381c4dbcc" alt="Descripción de la imagen">
</p>

<p align="center">
  <em>Figura 3: Ejemplo de filtros y datos obtenidos directamente en la plataforma SIAP.</em>
</p>


