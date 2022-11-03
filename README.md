# RN-A-Normalizacion
Redes Neuronales - Adicional - Normalizacion
### Introduccion ###

Un tema que suele ser muy confuso para los principiantes cuando usan redes neuronales es la normalización y codificación de datos. Debido a que las redes neuronales funcionan internamente con datos numéricos, los datos binarios (como el sexo, que puede ser masculino o femenino) y los datos categóricos (como una comunidad, que puede ser suburbana, urbana o rural) deben codificarse en forma numérica. Además, la experiencia ha demostrado que, en la mayoría de los casos, los datos numéricos, como la edad de una persona, deben normalizarse. Hay muchas referencias que analizan la teoría de la normalización y la codificación, pero pocas brindan orientación práctica y aún menos brindan ejemplos de implementación de código. El proceso es conceptualmente simple pero sorprendentemente difícil de implementar.  

Cuando se utilizan redes neuronales, los datos sin procesar suelen ser binarios (dos valores posibles), categóricos (tres o más valores posibles) o numéricos. En la demostración, el sexo se identifica como binario, los ingresos como numéricos, la comunidad como categórica y la edad como numérica. La variable dependiente, afiliación política, se etiqueta como categórica.  

### Codificación de datos binarios y categóricos ###

Al codificar datos binarios y categóricos, hay cuatro casos que debe tratar: datos binarios independientes (x), datos binarios dependientes (y), datos categóricos independientes (x) y datos categóricos dependientes (y). Un ejemplo de datos binarios independientes es una variable predictora, sexo, que puede tomar uno de dos valores: "masculino" o "femenino". Para tales datos, recomiendo codificar los dos valores posibles como -1.0 y +1.0:

* male   = -1.0  
* female = +1.0  

Hay investigaciones convincentes que indican que un esquema de -1.0, +1.0 es superior a un esquema simple de 0.0, 1.0 para variables binarias independientes.  

Un ejemplo de datos categóricos independientes es una comunidad variable predictora, que puede tomar valores "suburbano", "rural" o "ciudad". Para tales datos, recomiendo usar lo que a menudo se denomina codificación de efectos 1 de (C-1). La codificación de efectos no es obvia y se explica mejor con un ejemplo  

* suburban = [ 0.0,  0.0,  1.0]  
* rural    = [ 0.0,  1.0,  0.0]  
* city     = [-1.0, -1.0, -1.0]  

En otras palabras, la codificación de efectos configura una matriz de valores numéricos. El tamaño de la matriz es el número de valores posibles, c. El primer valor categórico tiene valores 0.0 en todas las posiciones excepto un solo valor 1.0 en la última posición. El segundo valor categórico tiene el único 1.0 en la penúltima posición, y así sucesivamente. El último valor categórico, en lugar de tener un 1,0 en la primera posición y valores de 0,0 en las posiciones c-1 restantes como cabría esperar, tiene valores de -1,0 en todas las posiciones c.  

En la demostración, la variable dependiente, afiliación política, es categórica y tiene cuatro valores posibles: "republicano", "demócrata", "libertario" y "otro". Para codificar datos categóricos dependientes, recomiendo usar lo que a menudo se denomina codificación ficticia 1 de C:

* republican  = [0.0, 0.0,  0.0,  1.0]  
* democrat    = [0.0, 0.0,  1.0,  0.0]  
* libertarian = [0.0, 1.0,  0.0,  0.0]  
* other       = [1.0, 0.0,  0.0,  0.0]  

En otras palabras, la codificación 1 de C es lo mismo que la codificación de efectos, excepto que el último valor categórico tiene un 1,0 en la primera posición de la matriz y 0,0 valores en todas las demás posiciones c-1.

En lugar de tener cuatro valores posibles, supongamos que la variable dependiente, la afiliación política, tuviera solo dos valores, "conservador" o "liberal". Este sería un ejemplo de datos binarios dependientes. En tales situaciones, recomiendo usar un esquema simple 0.0, 1.0:

* conservative  = 0.0
* liberal       = 1.0 

No es del todo obvio por qué recomiendo cuatro esquemas de codificación diferentes para los cuatro casos de datos diferentes. Y hay varias alternativas. Puede encontrar muchas referencias en línea que abordan una discusión dolorosamente detallada de este tema si está interesado en la teoría detrás de estas recomendaciones de codificación.

### Normalización de datos numéricos ###

Hay dos casos de datos numéricos de redes neuronales: datos numéricos independientes (x) y datos numéricos dependientes (y). Un ejemplo de valores de datos numéricos independientes son las edades (54, 28, 31, 48, 22, 39) en el programa de demostración. Recomiendo normalizar los datos numéricos independientes calculando las medias y la desviación estándar de los datos numéricos x y luego aplicando la transformación (x - media) / stddev.

Por ejemplo, en el programa de demostración, la media de los seis valores de edad es 37,0 y la desviación estándar de los seis valores de edad es 11,22. Entonces, la edad normalizada para la primera persona es (54.0 - 37.0) / 11.22 = 1.51.

En la mayoría de los casos, los datos numéricos normalizados tendrán valores que oscilan entre -6,0 y +6,0. La idea detrás de la normalización de datos es escalar todos los datos numéricos para que tengan magnitudes más o menos similares. En la demostración, un valor de ingreso anual típico es 30,000.0, pero un valor de edad típico es 31.0. Sin la normalización, las grandes magnitudes de los datos de ingresos en relación con los datos de edad harían que el proceso de entrenamiento de la red neuronal fuera más difícil que con los datos normalizados, porque los cambios en las ponderaciones de ingresos tendrían un efecto mucho mayor que los cambios en las ponderaciones de edad.

Para datos numéricos dependientes, excepto en situaciones muy inusuales, recomiendo no normalizar ni transformar los datos.
