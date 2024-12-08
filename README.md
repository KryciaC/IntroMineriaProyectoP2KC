# IntroMineriaProyectoP2KC
Introducción a la minería de datos - Proyecto Parte 2 - Árboles de decisión, Random Fores y Redes Neuronales

# Minería de datos - Krycia Castillo 

## 

# Proyecto Parte 2
## Análisis de datos - Servicios hospitalarios consulta interna

## Datos generales
En este proyecto se están utilizando los datos disponibles en la página del INE (Instituto Nacional de Estadística de Guatemala), se muestra los datos sobre los servicios internos de los distintos hospitales, sanatorios y casas de salud del sector privado. Los datos disponibles corresponden a los años del 2009 a 2022. Link: `https://www.ine.gob.gt/estadisticas-hospitalarias/`

## Información del código 

Para usar este código se puede correr un chunk tras otro ya que estan colocados en orden. 

Para iniciar se debe instalar y llamar a las librerías necesarias para realizar este proyecto, conforme se avanza en el proyecto se agregarán las liberías correspondientes. En caso no tenerlas se deben instalar. Se utilizarán las siguientes librerias:

**Librerias** 

library(haven)

library(arules)

library(fim4r)

library(dplyr)

library(ggplot2)

library(rpart)

library(rpart.plot)

library(randomForest)

**Carga de datos**

#Los datos están disponibles en un archivo por año. Los archivos se encuentran en formato SPSS (.sav), se procede a leer los archivos utilizando read_sav para lo cual se debe instalar previamente la librería "haven". En este caso el notebook de R se ha guardado en la misma carpeta donde están los archivos por lo cual no se especifica la ubicación del archivo, unicamente el nombre, en caso que el archivo esté en otra carpeta se debe especificar la ubicación correspondiente:

Ej. 

```
data2009 <- read_sav("Datos 2009.sav")
```

**Revisión de datos**

Se puede utilizar str (NOMBRE_DEL_DATASET) para revisar la estructura como se muestra acontinuación:

```
str(data2009)
```

En este caso se ha creado un dataset por cada año y se ha revisado cada uno, se identificaron diferentes diferencias y se modificaron utilizando rename, attr( ), mutate. Tomar en cuenta que al cargar los archivos .sav se genera un dataset que incluye las etiquetas de las clasificaciones incluidas en el data set, si se modifica el código de alguna categoría se debe modificar la etiqueta correspondiente también. 

Se puede revisar la información disponible en los datasets utilizando:
```
summary(dataset)

table(dataset$variable a revisar)
```

Posterior a la revisión se identifico algunas variables que que contenían valores sin categoría por lo cual se procedió a eliminarlas. 

Luego de realizar la limpieza correspondiente de los datos se unió los todos años en un único dataset - usando la librería dplyr y bind_rows:

```
data <- bind_rows(data2009, data2010, data2011, data2012, data2013, data2014, data2015, data2016, data2017, data2018, data2019, data2020, data2021, data2022)
```

En este caso posterior a la union de los datasets se realizó un última modificación a los datos Debido a que la edad se muestra en 2 columnas, EDAD donde se muestra el valor numérico de la edad y PERIODOEDA donde se indica si son días, meses o años. Para facilidad en el análisis posterior se procederá agregar una nueva columna donde todas las edades se muestren en años. 


Se puede leer el archivo de data guardado luego de unir los datasets de cada año, esto será de utilidad en caso no se desee correr todas las líneas previas donde se limpiaron los datos, para este notebook se utilizó para realizar la aplicación del algoritmo random forest. Notar que se vuelve a guardar como "data". Esto se realizó debido a que este notebook se trabajó en diferentes sesiones, si es la primera vez que se utiliza si se deben correr todas las líneas de revisión y limplieza de los datos. 


**Aplicación del algoritmo Árbol de decisión**

para este algoritmo necesitamos la librería rpart, Se procede a crear el árbol para predecir la variable objetivo para lo cual se utiliza rpart, se indica la variable a predecir, las variables a utilizar para la predicción, el dataset y el método a utilizar. Se grafica el árbol utilizando rpart.plot


Para el árbol 3 de PPERTENENCIA se debe tomar en cuenta que se considerarán unicamente los años entre 2009 y 2017 debido a los cambios de categorías a partir de 2018, de igual forma para tener solamente 2 valores vamos a eliminar los valores PPERTENENCIA = 9= ignorado.

**Aplicación del algoritmo Random Forest**
Para aplicar el algoritmo random forest se utiliza la librería random forest.  


** Redes neuronales**

Para redes neuronales se utilizará el notebook de google colab, se debe considerar que en el notebook de R se generó el archivo de datos dataNA2 para poder usarlo en google colab, se debe especificar la ruta donde se guardará y el nombre que se le asignará al archivo (para este caso fue dataRN.sav). Este es el archivo a usar para redes neuronales. 
