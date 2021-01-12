---
title: Feature Engineering
feature_text: |
  Creación de nuevas variables
feature_image: "/cajamar_predictive/images/fondo.png"
image: "/cajamar_predictive/images/fondo.png"
---

<p align="justify">En este apartado se explican qué variables se introducen en los modelos predictivos y como se han deducido.</p>


### Son todas las variables necesarias?

<p align="justify">Se ha decidido no usar la variable género, ya que no se considera adecuada la recomendación de productos basada en diferencias en esta característica. Aunque esta variable pueda dar lugar a resultados mejores, no es ético que se usen modelos basados en diferencias de género entre clientes, ya que va contra las política de igualdad de género actuales.  
</p>


### Obtener información con la fecha de compra

#### Se pueden eliminar productos antiguos?

<p align="justify">Una primera hipótesis fue utilizar solo información de compras más recientes. Se comprobó por tanto, los rangos de fecha de los distintos productos en ambos datasets. El gráfico de continuación presenta la diferencia entre el año inicial de los productos entre ambos datasets, dandonos visión de dicha diferencia.</p>

{% include figure.html image="/cajamar_predictive/images/p2.png" position="left" %}

<p align="justify">Se pudo observar que los productos no aparecen en los dos datasets exactamente en el mismo rango de años. Hay un producto en concreto, el 1002, que aparece en el test 29 años antes que en el train, y dos mas, el 704 y el 2503, que aprecen 12 y 11 años antes en el train que en el test, respectivamente. Por eso se decidio no filtrar muestras basandonos en esta propiedad.</p>

#### Hay productos que se venden más en determinadas epocas del año?

<p align="justify">Una posible característica a añadir es el mes de compra del producto. Por tanto, se estudió la distribución a lo largo de los meses para todos los productos. El siguiente gráfico presenta el caso particular del producto 9993, el cual presenta un pico en marzo y abril. En consecuencia se podría deducir que es un producto estacional y que dicha característica debería introducirse en el dataset.</p>

{% include figure.html image="/cajamar_predictive/images/p3.png" position="left" %}


#### Hay productos que se vendan juntos?

<p align="justify">
Otra idea interesante a explorar la correlación entre productos. Aplicando técnicas senzillas de correlación se ha podido detectar que efectivamente hay productos que se venden juntos. Como por ejemplo los codigos 9993 y el 9991 que tienen cada año el mismo número de compras (ver imagen siguiente). Sería acertado, por tanto, recomendar a los clientes que tengan un producto que compren su pareja.</p>

{% include figure.html image="/cajamar_predictive/images/p4a.png" position="left" %}

#### Y de los productos que se compran juntos, que parejas predominan?

<p align="justify">
Como se ha comentado anteriormente, el dataset presenta parejas de productos. Si se observa la distribución de compra por las distintas parejas y trios, se pueden observar distintos conjuntos altamente demandados como el de 201-601, seguido de 601-2302, 301-601 y 201-601-2302. Tal como se ha visto anteriormente, los productos 601, 201, 301 deben pertenecer a productos primarios. Por tanto no es de estrañar encontrarlos en las secuencias.  </p>

{% include figure.html image="/cajamar_predictive/images/p7.png" position="left" %}


----

### Relación entre último y penúltimo producto

<p align="justify">
Otra idea interesante es mirar la relación entre un producto y el anterior comprado. Para mirar esta idea se cogen los últimos y penúltimos productos de cada customer y se crea el siguiente gráfico. Dicho gráfico es un heatmap, en el cual cada recuadro representa el log(N), siendo N el número de veces que 2 productos se compran seguidos.
</p>
{% include figure.html image="/cajamar_predictive/images/p10.png" position="left" %}


<p align="justify">
Hay algunos productos que se compran bastante seguidos, como por ejemplo el <b>9991</b> y el <b>9993</b>, como ya hemos comentado anteriormente, el <b>601</b> y el <b>301</b>, y también el <b>601</b> y el <b>2302</b>, entre otros. Además, esta matriz nos puede dar una idea de relaciones entre productos, y también nos plantea la posiblidad de hacer cluster de productos para detectar este tipo de relaciones.
</p>



----

### Variables relacionadas con el customer

<p align="justify">
A continuación se pretende caracterizar a los distintos customers según sus características de compra, como por ejemplo, si es un customer que compra mucho, cuando es su primera compra, y la última, cada cuanto realiza una compra, etc.</p>

#### Cuantos productos han comprado los customers?

<p align="justify">
Podemos ver que la gran mayoria de customers compran entre 1-4 productos. </p>

{% include figure.html image="/cajamar_predictive/images/p4.png" position="left" %}


#### Y de los que solo han comprado un producto, que productos predominan?

<p align="justify">
Se puede ver pues que el <b>601</b> destaca en esos usuarios que solo han comprado uno, seguido del <b>301</b>, el <b>201</b> y el <b>2302</b>. Se puede deducir que estos productos deben ser básicos para todo usuario bancario. </p>

{% include figure.html image="/cajamar_predictive/images/p5.png" position="left" %}

<p align="justify">
Tambien se pueden evaluar los productos comprados por customers con mayor historial de compra (> 10 productos).</p>
<p align="justify">
El producto <b>601</b> sigue teniendo mucha demanda, pero a él se unen también otros productos como el <b>201</b> y el <b>301</b>, el <b>2302</b> y la pareja formada por el <b>9991</b> y <b>9993</b>.</p>

{% include figure.html image="/cajamar_predictive/images/p6.png" position="left" %}


#### Es importante el mes de compra?

<p align="justify">
Entendiendo el negocio se puede deducir que los customers tendrán tendencia a comprar en determinados periodos del año. Así pues es interesante mirar si hay este efecto. En la imágen siguiente se puede observar las compras de estos customers se centran en meses determinados. </p>

{% include figure.html image="/cajamar_predictive/images/fig11.png" position="left" %}

<p align="justify">Otra variable a deducir es el tiempo de compras, que se puede visualizar en los siguientes gráficos:</p>

{% include figure.html image="/cajamar_predictive/images/fig12.png" position="left" %}

<p align="justify">
La mayoria de customers tienen aproximadamente un tiempo medio desde la primera compra de 5000 dias (14 años), un tiempo medio desde la última compra de 2222 (7 años) y un lag entre compras de 1200 (3 años).
</p>


## Enriquecer la base

<p align="justify">Usando la información anterior se han creado variables nuevas para ayudar al modelo.</p>

<p align="justify">Primero de todo, tal y como se vio en el análisis exploratorio de los datos, hay mucha información temporal que puede ser útil.</p>
<p align="justify">Otro punto es introducir el histórico de productos.Así pues, se añaden 94 variables (tantas como productos únicos), que indican si un producto se ha comprado anteriormente.</p>


#### Cluster de productos

<p align="justify">Una primera aproximación fue hacer un clustering para ver si se agrupan los productos y se puede añadir una variable <b>cluster por producto</b>. Para hacer el clustering se utiliza la plataforma h2o, ya que tiene funciones optimizadas para trabajar con algoritmos de machine learning.</p>
<p align="justify">Sin embargo, se descarto esta idea porque los grupos obtenidos se repartían de manera muy inhomogénea.</p>


#### Cluster de customers

<p align="justify">Por otro lado, se presenta otra aproximación de clustering, esta vez de los usuarios dadas sus características sociodemográficas y la información de compra. </p>

<p align="justify">En este caso, el clustering ha dado unos grupos con porcentages de customers más razonables, como se puede apreciar en la siguiente figura. </p>
{% include figure.html image="/cajamar_predictive/images/fig20.png" position="left" %}

<p align="justify">El análisis exploratorio se hizo con Power BI de Microsoft.</p>

[CajamarPowerBI](https://app.powerbi.com/view?r=eyJrIjoiN2VjYmFhNDktZjUzMy00MjBkLTgxMmItMmRlZWYyZjI2YzBmIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9)

<!--
<iframe width="800" height="600" src="https://app.powerbi.com/view?r=eyJrIjoiN2VjYmFhNDktZjUzMy00MjBkLTgxMmItMmRlZWYyZjI2YzBmIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>
--> 

<p align="justify">En los clusters se puede apreciar: </p>

<p align="justify">* Grupo de clientes mayores con ingresos medios (cluster 0).</p>
<p align="justify">* Grupo de clientes más jóvenes y de mediana edad con ingresos medios-bajos (cluster 1).</p>
<p align="justify">* Grupo de clientes de mediana edad con ingresos medios-altos (cluster 2).</p>
<p align="justify">* Grupo de clientes  de mediana-alta edad con ingresos altos (cluster 3).</p>
<p align="justify">* El cluster 3 es el que tiene más clientes autónomos.</p>
<p align="justify">* Mayormente, los grupos de edad más alta tienen también más antigüedad.</p>

## Conclusiones

<p align="justify">Los análisis llevados a cabo en este apartado permiten definir las variables nuevas que se van a introducir en el modelo predictivo. Destacar la importancia de las variables temporales, así como la información del historial de compra. El hecho que los customers tengan características sociodemográficas y comportamientos de compra distintos permiten también agruparlos en clusters. </p>
