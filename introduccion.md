---
title: Exploración
feature_text: |
  Análisis exploratorio de los datos y comprensión de negocio
feature_image: "/cajamar_predictive/images/fondo.png"
image: "/cajamar_predictive/images/fondo.png"
---
<p align="justify">En este primer apartado se presenta el análisis exploratorio de los datos del reto.</p>

## Introducción Cajamar

{% include figure.html image="https://alimentaria.world/wp-content/uploads/2016/02/cajamar_positivo_rgb" position="left" %}

<p align="justify">
Cajamar es una entidad financiera resultante de la fusión de diversas cajas rurales españolas. Sus primeras oficinas abrireron sus puertas en 1966 en Almería. En 1988 iniciaron su expansión integrando otras cajas rurales y cooperativas, actividad que siguieron desarrolando a lo largo de los siguientes años, especialmente a partir de los años 2000. Actualmente tiene más de 1,4 millones de socios y 4 millones clientes.</p> 

<p align="justify">
Las actividades de Cajamar Caja Rural atienden las necesidades y demandas de financiación, ahorro e inversión de sus socios y clientes. Realiza toda clase de operaciones activas, pasivas y de servicios, entre ellas las de banca al por menor en su red de sucursales, banca corporativa, financiación hipotecaria, banca telefónica y banca electrónica, operaciones financieras con no residentes, gestión de fondos y patrimonios, arrendamiento financiero, seguros y otros productos secundarios para captación de recursos o financiación a clientes.</p>

## Primeros pasos

<p align="justify">El dataset <i>train</i> original tiene una dimensión de 3.350.601 entradas por 8 variables y el dataset <i>test</i>, 1.147.687 entradas y 8 variables.</p>


## Variables

<p align="justify">Las variables sociodemográficas disponibles son las siguientes:
Identificador de cliente (ID_Customer), código de la modalidad de producto contratado (Cod_Prod), fecha de contratación (Cod_Fecha), edad (Socio_Demo_01), Antigüedad (Socio_Demo_02), ingresos (Socio_Demo_03), sexo (Socio_Demo_04) y segmento (Socio_Demo_05). </p>

Para más información de las variables, consultar la web de [University Hack 2017](http://www.cajamardatalab.com/datathon-cajamar-universityhack-2017/) 


### Análisis exploratorio de las variables sociodemográficas

<p align="justify">
Para evaluar las variables de manera dinámica se ha preparado un Desktop con Power BI de Microsoft.</p> 

[CajamarPowerBI](https://app.powerbi.com/view?r=eyJrIjoiN2I5MzM5MTUtZWZhMi00MmNlLWI0NmEtMjEwOTY1NWMzOTZjIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9)


<iframe width="800" height="600" src="https://app.powerbi.com/view?r=eyJrIjoiN2I5MzM5MTUtZWZhMi00MmNlLWI0NmEtMjEwOTY1NWMzOTZjIiwidCI6ImEyMzEzY2FiLWIxYzMtNGYzYS1iYjExLTIxNTc0NDdkZGJiNCIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>

<p align="justify">A nivel temporal los dos datasets presentan distribuciones similares tanto a nivel de productos por año como por mes. Se puede observar un incremento de venta de productos a partir del año 2000, que coincide con la expansión y fusión de la entidad. </p>


<p align="justify">Comparando las variables sociodemográficas entre ambos datasets, se puede observar que el rango de edad predominante es entre 45-65 años. Esto encaja con que la antigüedad predominante sea entre 10-20 años (que también encaja con el incremento alrededor del año 2000.En relación a los ingresos, el train set muestra customers con unos valores menores que los valores presentados en el test. En tema de género, el train presenta más proporción de hombres que el test. Finalmente, respecto al segmento de los customers, ambos datasets tienen mayoritariamente a particulares.</p> 

<p align="justify">Así pues, con esta exploración hemos podido hacernos una idea general de los dos datasets, sus parecidos y diferencias.</p> 


## Conclusiones 

<p align="justify">Después de esta primera exploración de los datos, podemos concluir que los datasets de train y test estan hechos de manera muy similar, sobretodo en la distribución temporal. Hay diferencies por lo que respecta a customers en género y segmento. </p>
<p align="justify">En este reto parece clave la información que se puede obtener a partir de la fecha de compra, así que puede ser útil para el modelo predictivo añadir más variables con información temporal. </p>
<p align="justify">El orden de compra es importante, ya que hay productes que se compran o tienden a comprarse juntos. Por lo tanto, también puede ser de utilidad añadir variables de compras previas. El orden de compra es importante, ya que hay productes que se compran o tienden a comprarse Esta información primaria se usará para la creación de nuevas variables y de modelos. </p>




