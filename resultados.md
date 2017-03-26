---
title: Resultados
feature_text: |
  Resultados del modelo predictivo
feature_image: "/cajamar_predictive/images/fondo.png"
image: "/cajamar_predictive/images/fondo.png"
---

<p align="justify">En este apartado se presenta los resultados obtenidos. </p> 


### Validación de los modelos por cada cluster 

<p align="justify">Continuando con lo explicado en el apartado anterior de "Seleccion de Modelos", se ha aplicado un DRF con una optimización usando un Grid Random Search para cada train and test set agrupado por los distintos clusters. A continuación se muestran los resultados de la validación con la curva ROC i la Curva de Precision-Recall (explicadas brevemente anteriormente). </p> 

<p align="justify">- ROC: las curvas ROC muestras una performance casi perfecta del modelo. El area bajo las curvas para los distintos cluster varia desde 0.92 a 0.98. Sin embargo, y como se ha explicado brevemente, esta curva puede dar información falsa sobre como es, en realidad, la performance del modelo, ya que nos da información que puede estar bias debido al imbalance dataset. </p> 

<p align="justify">- Precision - Recall: en este caso si podemos ver diferencias entre los modelos, siendo el cluster_2grid (cluster 2) el que obtuvo mejores puntuaciones de precision y el que dispone de una mejor precision-recall curve. </p> 

<img src="/cajamar_predictive/images/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

<img src="/cajamar_predictive/images/unnamed-chunk-2-2.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />


---

### Validación del Model Score 

<p align="justify">El Model Score nos da una idea de como de bien recomienda nuestro modelo. En el mejor de los casos el model score debiera ser de 94, siendo que hemos recomenando a cada customer el producto que realmente compró en el primer lugar del ranking.</p>  
<p align="justify">En nuestro caso se ha obtenido un Model Score de 0.95, bastante cercano a 1. 
Los siguientes gráficos muestran el histograma de score por customer. Recordemos que para cada customer se calcula el score como la posición en el ranking del producto que realmente compró (siendo 1 el peor score y 94 el mejor). </p> 
<p align="justify">El gráfico muestra claramente un pico en la posición 94, es decir, en el mejor resultado. Ese se corresponde con la cantidad de customers por los cuales se ha recomendado el producto correcto a la primera. Sin embargo también se puede observar una cola en los otros valores de score, confirmando que el modelo no tiene una performance perfecta. </p> 

<img src="/cajamar_predictive/images/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

<p align="justify">El siguiente gráfico es igual al anterior pero permite ver la proporción de customers por cada score. Esto nos permite confirmar los sigueintes resultados:</p>  
<p align="justify">- 46% de customers se les ha recomendado el producto correcto en el 1r lugar.</p>  
<p align="justify">- 76% de customers se les ha recomendado el producto correcto entre el 1r i el 4t lugar.</p>  


<img src="/cajamar_predictive/images/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />


<p align="justify">Finalmente, y como curiosidad, si calculamos el Model Score solo en los customers que anteriormente habian comprado el producto 9991, tenemos un model score de 0.999 (casi 1) y el producto a recomendar és el 9993!</p>  

---

### Conclusiones

<p align="justify">- Los resultados obtenidos son una lista de recomendaciones según la probabilidad de compra. Tratando con un problema de recomendación de productos, nos parece interesante presentar también los 3-4 productos con mayor probabilidad, ya que normalmente en este abordaje las empresas tienen en cuenta más de una opción de recomendación.</p>   

<p align="justify">- Si recomendamos 3-4 productos, en más del 70% de los casos se ofrece el producto comprado a continuación por el cliente.</p> 

<p align="justify">- En nuestra métrica de validación, no se considera solamente acertar o no el primer producto, sino que tiene en cuenta en qué posición de nuestra lista de recomendaciones está el producto que realmente comprará el cliente. Por lo tanto, nos permite valorar también si el producto real está entre las primeras recomendaciones, no solo la primera. Creemos que esta validación se ajusta más a la realidad del mercado estudiado.</p> 

<p align="justify">- Crear un modelo por cluster ha dado mejores resultados que hacer un modelo para todos los clientes. Por lo tanto, buscar características distintivas entre clientes parece ser un buen planteamiento.</p> 

<p align="justify">- La utilización de librerías y plataformas como h2o permite crear, optimizar y evaluar modelos de una manera rápida y sencilla. De esta manera se puede dedicar una parte importante del proceso en estudiar y transformar la base y las variables.</p>   


