---
title: Exploración
feature_text: |
  Análisis exploratorio de los datos y comprensión de negocio
feature_image: "https://unsplash.it/1300/400?image=1061"
excerpt: "Análisis exploratorio de los datos y comprensión de negocio"
---
<p align="justify">
En este primer apartado se presenta el análisis exploratorio de los datos del reto Microsoft Predictive Modelling de Cajamar. </p>

<<<<<<< HEAD
## Introducción Cajamar

{% include figure.html image="https://alimentaria.world/wp-content/uploads/2016/02/cajamar_positivo_rgb" position="left" %}

<p align="justify">
Cajamar es una entidad financiera resultante de la fusión de diversas cajas rurales españolas. Sus primeras oficinas abrireron sus puertas en 1966 en Almería. En 1988 iniciaron su expansión integrando otras cajas rurales y cooperativas, actividad que siguieron desarrolando a lo largo de los siguientes años, especialmente a partir de los años 2000. Actualmente tiene más de 1,4 millones de socios y 4 millones clientes.</p> 

<p align="justify">
Las actividades de Cajamar Caja Rural atienden las necesidades y demandas de financiación, ahorro e inversión de sus socios y clientes. Realiza toda clase de operaciones activas, pasivas y de servicios, entre ellas las de banca al por menor en su red de sucursales, banca corporativa, financiación hipotecaria, banca telefónica y banca electrónica, operaciones financieras con no residentes, gestión de fondos y patrimonios, arrendamiento financiero, seguros y otros productos secundarios para captación de recursos o financiación a clientes.</p>

## Primeros pasos
<p align="justify">
Primero se evaluan las dimensiones de los datasets y se hacen comprovaciones senzillas:</p>

<p align="justify">
El dataset train original tiene una dimensión de 3350601 entradas por 8 variables y el dataset test, 1147687 entradas y 8 variables. Antes de empezar se tienen que comprobar si hay entradas duplicadas y/o missing values. En este caso no hay duplicados ni missing values.</p>


## Variables
El significado de las variables es el siguiente:

- ID_Customer = Identificador de cliente
- Cod_Prod = Código de la modalidad de producto contratado
- Cod_Fecha = Fecha de contratación de la modalidad de producto
- Socio_Demo_01 = Edad
- Socio_Demo_02 = Antigüedad
- Socio_Demo_03 = Ingresos
- Socio_Demo_04 = Sexo (1: Hombre, 2: Mujer)
- Socio_Demo_05 = Segmento (00: Particular | 01:Agricultor | 02:Comercio | 03:Autónomo)


<p align="justify">
Así pues, tenemos el identificador del usuario, el codigo del producto comprado, la fecha de la compra y características demográficas del usuario.</p>

### Visualización variables sociodemográficas
<p align="justify">
Para evaluar las variables sociodemográficas de manera dinámica se ha preparado un Desktop con Power BI de Microsoft. De esta manera se pueden visualizar diferentes gráficos dinámicos de estas variables.</p> 

[CajamarPowerBI](https://app.powerbi.com/view?r=eyJrIjoiN2I5MzM5MTUtZWZhMi00MmNlLWI0NmEtMjEwOTY1NWMzOTZjIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9)


<iframe width="800" height="600" src="https://app.powerbi.com/view?r=eyJrIjoiN2I5MzM5MTUtZWZhMi00MmNlLWI0NmEtMjEwOTY1NWMzOTZjIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>

*CONCLUSIONS!!!!*


### Obtener información con la fecha de compra
<p align="justify">
Una comprovación importante es saber si el dataset de test tiene una distribución de año de compras similar al dataset de train. Vamos a mirarlo.</p> 

{% include figure.html image="/images/p1.png"%}

<p align="justify">
Podemos ver que los años de compra se distribuyen de manera muy parecida en los dos datasets. Es interesante observar que tenemos tanto entradas antiguas como entradas mas recientes, aunque predominan las mas nuevas. Si tenemos en cuenta la evolución de Cajamar, tiene sentido que en los años recientes haya un mayor número de entradas, ya que coincide con la expansión y fusión de la entidad. </p> 

<p align="justify">
También es útil saber si los productos se venden aproximadamente en los mismos periodos de tiempo entre el dataset train y test, ya que nos puede servir para establecer etiquetas de productos viejos y nuevos. 
Primero de todo se calcula los años que hay entre la primera compra y la última de cada producto, para establecer su rango de compra en cada dataset. Posteriormente se comparan los dos datasets para saber si los productos de los dos datasets se ofrecen en el mismo periodo. </p>

{% include figure.html image="/images/p2.png"%}

<p align="justify">
Se puede observar que los productos no aparecen en los dos datasets exactamente en el mismo rango de años. Hay un producto en concreto, el 1002, que aparece en el test 29 años antes que en el train, y dos mas, el 704 y el 2503, que aprecen 12 y 11 años antes en el train que en el test, respectivamente. Así pues, aunque mayormente el periodo en que aparecen los productos en el test y el train es parecido, no es muy apropiado basarnos en las fechas de inicio y final de aparición de productos en el train para definir este rango en el test, ya que puede variar. </p>

#### Hay productos que se venden mas en determinadas epocas del año?

<p align="justify">
Mirando el efecto temporal, tambien es importante visualizar si hay productos que se tienden a comprar más en algunas épocas del año en concreto. </p>

{% include figure.html image="/images/p3.png"%}

<p align="justify">
Se puede observar que sí que hay productos que se venden en épocas determinadas. Puede ser interesante añadir esta información en los modelos. </p>

#### Hay productos que se vendan juntos?

<p align="justify">
Otra idea interesante a explorar es identificar si hay algunos productos que se vendan juntos. Hemos podido detectar que hay dos productos, el 9993 y el 9991, que tienen cada año el mismo número de compras. Así pues, es indicado suponer que se deben vender juntos o de manera consecutiva. Así pues, si en el test hay usuarios que han comprado uno de los dos productos y no tienen el otro, se les puede recomendar. </p> 

{% include figure.html image="/images/p4a.png"%}



### Variables relacionadas con el customer 

<p align="justify">
Ahora queremos ver como actua cada customer, por ejemplo, es un customer que compra mucho? Cuando es su primera compra, y la última? Y el tiempo medio entre compras? De esta manera podemos provar de caracterizar los customers. </p>

#### Cuantos productos han comprado los customers?

{% include figure.html image="/images/p4.png"%}

<p align="justify">
Podemos ver que la gran mayoria de customers compran entre 1-4 productos. </p>

#### Y de los que solo han comprado un producto, que productos predominan?

{% include figure.html image="/images/p5.png"%}

<p align="justify">
Se puede ver pues que el *601* destaca en esos usuarios que solo han comprado uno, y ya con menos productos, el *301*, el *201* y el *2302*. </p>

<p align="justify">
Tambien se pueden evaluar los productos comprados por customers que compran mucho (> 10 productos).</p>

{% include figure.html image="/images/p6.png"%}

<p align="justify">
El producto *601* sigue siendo muy alto, pero a él se unen también otros productos como el *201* y el *301*, el *2302* y la pareja formada por el *9991* y *9993*.</p> 

#### Y de los productos que se compran juntos (lag=0), que parejas predominan?*

{% include figure.html image="/images/p7.png"%}


<p align="justify">
El conjunto predomina más es el de 201-601, seguido de 601-2302, 301-601 y 201-601-2302. Como se ha ido viendo, estos 3 productos son muy recurrentes. </p>

<p align="justify">
Por otra parte, es de esperar que haya customers que tiendan a comprar más en unos meses que en otros, así que también es interesante mirar si hay este efecto. </p>

{% include figure.html image="/images/p8.png"%}

<p align="justify">
Por otro lado, fijandonos en el tiempo de compras, podemos generar los siguientes gráficos:</p> 

{% include figure.html image="/images/p9.png"%}

<p align="justify">
La mayoria de customers tienen aproximadamente un tiempo medio desde la primera compra de 5000 dias (14 años), un tiempo medio desde la última compra de 2222 (7 años) y un lag entre compras de 1200 (3 años). 
</p>

### Relación entre último y penúltimo producto

<p align="justify">
Otra idea interesante es mirar la relación entre un producto y el anterior comprado, es decir, si después de comprar uno se tiende a comprar otro en concreto. Para mirar esta idea se cogen los últimos y penúltimos productos de cada customer, para ver que parejas de productos se compran más seguidas.  
</p>
{% include figure.html image="/images/p10.png"%}


<p align="justify">
Hay algunos productos que se compran bastante seguidos, como por ejemplo el *9991* y el *9993*, como ya hemos comentado anteriormente, el *601* y el *301*, y también el *601* y el *2302*, entre otros. Estos productos han estado apareciendo en todos los análisis hechos hasta ahora, lo que indica que deben ser productos que compran todo tipo de clientes y deben ser bastante básicos. 
Además, esta matriz nos puede dar una idea de relaciones entre productos, y también nos plantea la posiblidad de hacer cluster de productos para detectar este tipo de relaciones. 
</p>


*CONCLUSIONES FINALES*





=======
<p align="justify">En este primer apartado se presenta el análisis exploratorio de los datos del reto Microsoft Predictive Modelling de Cajamar.</p>  

**Introducción Cajamar**

{% include figure.html image="https://alimentaria.world/wp-content/uploads/2016/02/cajamar_positivo_rgb" position="left" %}


<p align="justify">Cajamar es una entidad financiera resultante de la fusión de diversas cajas rurales españolas. Sus primeras oficinas abrireron sus puertas en 1966 en Almería. En 1988 iniciaron su expansión integrando otras cajas rurales y cooperativas, actividad que siguieron desarrolando a lo largo de los siguientes años, especialmente a partir de los años 2000. Actualmente tiene más de 1,4 millones de socios y 4 millones clientes.</p> 

<p align="justify">Las actividades de Cajamar Caja Rural atienden las necesidades y demandas de financiación, ahorro e inversión de sus socios y clientes. Realiza toda clase de operaciones activas, pasivas y de servicios, entre ellas las de banca al por menor en su red de sucursales, banca corporativa, financiación hipotecaria, banca telefónica y banca electrónica, operaciones financieras con no residentes, gestión de fondos y patrimonios, arrendamiento financiero, seguros y otros productos secundarios para captación de recursos o financiación a clientes.</p>
>>>>>>> origin/gh-pages



