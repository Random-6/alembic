---
title: Resultados
feature_text: |
  Resultados del modelo predictivo
feature_image: "/cajamar_predictive/images/fondo.png"
image: "/cajamar_predictive/images/fondo.png"
---

En este apartado se presenta los resultados obtenidos. 


### Validación de los modelos por cada cluster 

Continuando con lo explicado en el apartado anterior de "Seleccion de Modelos", se ha aplicado un DRF con una optimización usando un Grid Random Search para cada train and test set agrupado por los distintos clusters. A continuación se muestran los resultados de la validación con la curva ROC i la Curva de Precision-Recall (explicadas brevemente anteriormente). 

- ROC: las curvas ROC muestras una performance casi perfecta del modelo. El area bajo las curvas para los distintos cluster varia desde 0.92 a 0.98. Sin embargo, y como se ha explicado brevemente, esta curva puede dar información falsa sobre como es, en realidad, la performance del modelo, ya que nos da información que puede estar bias debido al imbalance dataset. 

- Precision - Recall: en este caso si podemos ver diferencias entre los modelos, siendo el cluster_2grid (cluster 2) el que obtuvo mejores puntuaciones de precision y el que dispone de una mejor precision-recall curve. 

<img src="/cajamar_predictive/images/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />

<img src="/cajamar_predictive/images/unnamed-chunk-2-2.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />


---

### Validación del Model Score 

El Model Score nos da una idea de como de bien recomienda nuestro modelo. En el mejor de los casos el model score debiera ser de 1, siendo que hemos recomenando a cada customer el producto que realmente compró en el primer lugar del ranking. 
En nuestro caso se ha obtenido un Model Score de 0.95, bastante cercano a 1. 
Los siguientes gráficos muestran el histograma de score por customer. Recordemos que para cada customer se calcula el score como la posición en el ranking del producto que realmente compró (siendo 1 el peor score y 94 el mejor). 
El gráfico muestra claramente un pico en la posición 94, es decir, en el mejor resultado. Ese se corresponde con la cantidad de customers por los cuales se ha recomendado el producto correcto a la primera. Sin embargo también se puede observar una cola en los otros valores de score, confirmando que el modelo no tiene una performance perfecta. 

<img src="/cajamar_predictive/images/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />

El siguiente gráfico es igual al anterior pero permite ver la proporción de customers por cada score. Esto nos permite confirmar los sigueintes resultados: 
- 46% de customers se les ha recomendado el producto correcto en el 1r lugar 
- 76% de customers se les ha recomendado el producto correcto entre el 1r i el 4t lugar 


<img src="/cajamar_predictive/images/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />


Finalmente, y como curiosidad, si calculamos el Model Score solo en los customers que anteriormente habian comprado el producto 9991, tenemos un model score de 0.999 (casi 1) y el producto a recomendar és el 9993! 




