---
title: Feature Engineering
feature_text: |
  Creación de nuevas variables
feature_image: "/cajamar_predictive/images/fondo.png"
image: "/cajamar_predictive/images/fondo.png"
---

<p align="justify">En este apartado se explican qué variables se introducen en los modelos predictivos.</p> 

### Son todas las variables necesarias?

Recordemos que variables tienen estos datasets:

* ID_Customer = Identificador de cliente
* Cod_Prod = Código de la modalidad de producto contratado
* Cod_Fecha = Fecha de contratación de la modalidad de producto
* Socio_Demo_01 = Edad
* Socio_Demo_02 = Antigüedad
* Socio_Demo_03 = Ingresos
* Socio_Demo_04 = Sexo (1: Hombre, 2: Mujer)
* Socio_Demo_05 = Segmento (00: Particular, 01:Agricultor, 02:Comercio, 03:Autónomo)

<p align="justify">Es importante tener en cuenta para quien se esta haciendo este modelo predictivo. En este caso, el banco Cajamar tiene que decidir la interpretabilidad y viabilidad del modelo. Así pues, una variable que hemos decidido <b>no utilizar para esta predicción es el género del cliente</b>, ya que no es adecuado que el banco utilize un modelo que introduzca diferencias de compra en función del género del cliente.</p> 

## Enriquecer la base

<p align="justify">A partir de las variables dadas también se pueden crear de otras para enriquecer la base.</p> 

<p align="justify">Primero de todo, tal y como se vio en el análisis exploratorio de los datos, hay mucha información temporal que nos puede ser útil. Así pues, podemos utilizar las variables creadas en el apartado anterior, como <b>mes</b> y <b>año</b>, <b>tiempo desde primera compra</b>,<b>tiempo desde última compra</b> y <b>tiempo medio entre compras</b>. Otro concepto interesante es saber cuantos productos ha comprado cada customer por mes, ya que así se intenta modelizar el hecho que hay productos que se compran mas en épocas determinadas y usuarios que tienden a compran más en determinados meses.</p> 

<p align="justify">A parte de las variables temporales, también se puede introducir información de los productos comprados anteriormente, ya que se ha visto que hay productos que se tienden a comprar juntos o de manera consecutiva, así que tener en cuenta los productos comprados previamente es también importante.</p> 


#### Cluster de productos

<p align="justify">Una primera aproximación es hacer un clustering para ver si se agrupan los productos y podemos hacer una variable <b>cluster por producto</b>. Para hacer el clustering se utiliza el paqueta h2o, ya que tiene funciones optimizadas para trabajar con algoritmos de machine learning.</p> 

*IMATGE REPARTICIO CLUSTER DOLENT*

<p align="justify">Como se puede observar, el clustering de productos según el número de productos por mes de compra no genera resultados muy aprovechables, ya que separa los productos en un cluster muy grande y otros de pequeños. Esta información no nos es muy útiles para complementar el modelo.</p> 


#### Cluster de customers

<p align="justify">Vamos a hacer otra aproximación de clustering, esta vez de los usuarios dadas sus características sociodemográficas y la información de compra. Las variables que se añaden en el clustering son:</p> 

* Socio_Demo01-05, todas excepto el género. 
* Variables de tiempo de compra.
* Total productos comprados

<p align="justify">De esta manera se han caracterizado los customers segun sus características demograficas y sus características de compras.</p> 

*AFEGIR LINK!*

*AFEGIR COMENTARIS*

<p align="justify">En este caso, el clustering ha dado unos grupos con porcentages de customers razonables. Para intentar caracterizar los distintos clusters, se ha utilizado l'herramienta de *Power BI*.</p>

### GRID de productos

<p align="justify">El historial de compras también se tiene que tener en cuenta, ya que esto tiene un efecto en la próxima compra. Por lo tanto, se ha hecho un grid para indicar, para cada compra, que productos ya se han adquirido anteriormente. Así pues, se añaden 94 variables (tantas como productos únicos), que indican con un valor de 1 si se ha comprado anteriormente cada producto.</p> 


## Base con variables finales

<p align="justify">Finalmente, se han añadido variables para enriquecer la base que se utiliza para los modelos. Las variables de la nueva base son: </p>

* Socio_Demo01-05, todas excepto el género. 
* Total productos
* Variables de tiempo de compra
  + Mes
  + Año
  + Tiempo desde la 1a compra
  + Tiempo desde última compra
  + Lag entre compras
  + Compras por mes
* Total productos comprados
* 94 columnas, una por producto, indicando si se ha adquirido previamente.



