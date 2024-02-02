# Deteccion_phishing_RF

**Introducción**

El phishing es una técnica de ciberseguridad que consiste en enviar mensajes fraudulentos, generalmente por correo electrónico, con el objetivo de obtener información confidencial de las víctimas. Estos mensajes pueden ser enlaces a sitios web falsos o archivos adjuntos que contienen malware. Para combatir este tipo de ataques, se propone un sistema de gestión de SOC (Security Operation Center) basado en Inteligencia Artificial (IA) para el reconocimiento de vulnerabilidades Phishing.

El  proyecto consiste en el entrenamiento de un modelo de aprendizaje automático y redes neuronales como árbol de decisiones o random Forest en el conjunto de datos creado para predecir sitios web de phishing . 

Se opto por el uso de este modelo Esos debido a su reputación de ser altamente efectivos para tareas de clasificación, como determinar si un sitio web es de phishing o no. y también son capaces de manejar datos categóricos y numéricos.
Estos modelos pueden capturar interacciones complejas en los datos, identificando automáticamente qué características basadas en URL y contenido web son más predictivas para detectar phishing.

Se utilizo  datos de  URL de sitios web de phishing y sitios benignos para formar un conjunto de datos y de ellos se extraen las características necesarias basadas en URL y contenido de sitios web para entrenamiento del sistema y que al final el sistema pueda determinar la  detección de sitios de Phishing con la mayor precisión posible . 

**Metodología**


1. Recopilación de datos: Se recolectarán datos de correos electrónicos de ejemplo, tanto legítimos como fraudulentos.

2. Preprocesamiento de datos: Se realizará el preprocesamiento de los datos, eliminando ruido y normalizando las características.

3. Selección de características: Se seleccionarán las características más relevantes para el reconocimiento de vulnerabilidades Phishing.

4. Modelado de aprendizaje automático: Se entrenará un modelo de aprendizaje automático utilizando los datos preprocesados y las características seleccionadas.

5. Evaluación del modelo: Se evaluará el rendimiento del modelo en un conjunto de datos de prueba.

**Resultados**

Se procede a la recolección de datos  como el conjunto de URL de phishing a partir de un servicio de acceso libre llamado PhishTank. Este servicio proporciona un conjunto de URL de phishing en varios formatos, como csv, json, etc., que se actualiza cada hora. 
A partir de este conjunto de datos, se recopilan 5000 URL de phishing aleatorias para entrenar el modelo Random Forest ML.

Las URL legítimas se obtienen de los conjuntos de datos de acceso libre de la Universidad de New Brunswick, https://www.unb.ca/cic/datasets/url-2016.html. Se obtuvo un conjunto  de 5000 datos que contiene una colección de URL benignas 


Los datos de entrada :  direcciones URL y estructuras HTML de sitios web
sospechosos. El sistema recibía estas URL a través de solicitudes y, tras el procesamiento interno, devolvía una respuesta que indicaba si la URL se consideraba segura o sospechosa de phishing. 


Las salidas del sistema se presentaron en formato binario, donde "1" representaba una URL sospechosa y "0" indicaba que se consideraba segura. 

La importancia de las caracteristicas en el modelo estan distribuidas de la siguiente manera 








# Implementacion

Para mejorar la precisión del modelo se opto por modificar 2 parámetros :


    • Aumentar el numero de arboles (n_stimators)  a 500 esto con el fin de reducir la varianza y mejorar el performance. 
    • Optimizar la profundidad máxima de los árboles (max_depth):  con valor de 13 para permitir que los árboles crezcan más y capten mejores interacciones entre las variables que nos interesan para la deteccion de phishing sobretodo las extensiones (Prefix/Sufix) y las características de la URL  .

    







Al realizar el contraste con el resultado de la primera implementación , en esta segunda implementación se mejoro la precisión de el modelo dando como resultado  de 0,814 en el entrenamiento y 0,834 en las pruebas 


A diferencia de el resultado inicial de  0,810 en precisión obtenida en el entrenamiento y 0,826 en las pruebas . 


De este modo el aumento de la profundidad máxima del árbol permitió que el modelo se adaptara mejor a las características repercutiendo en la precisión del mismo , no se uso un valor mas alto dado que existía el riesgo de pasar a un sobre ajuste  

El aumento en la precisión de test ing indica que el modelo generalizó mejor con los nuevos parámetros. Más árboles y mayor profundidad redujeron la varianza del modelo sin incrementar mucho el sesgo.
En cuanto a la  precisión de entrenamiento no tuvo un incremento tan significativo porque el modelo ya estaba sobre ajustado previamente con 100 árboles. Pero al permitir mayor profundidad, los árboles pudieron encontrar mejores patrones en los datos de entrenamiento.1

La diferencia de precisión en las pruebas de 0.008 puntos mayor nos indicaría que se logró un mejor balance entre sesgo y varianza ademas que también mejoraría la detección de muestras positivas y negativas, reduciendo los falsos positivos y falsos negativos.


**Conclusiones**

Se puede constatar que el aumentar el numero de arboles del random forest ayuda a mejorar la precisión , a costa de un ligero aumento de tiempo de entrenamiento , debido al rendimiento requerido por el computador.

la precisión suele estabilizarse rápido a medida que crece el bosque , indicaría que se podría obtener un buen modelo sin necesidad de cientos de árboles.
Tambien se observo que  hay una ventaja al usar el modelo de random forest y es que se reduce la correlación entre arboles al tener aleatoriedad en las muestras y variables 
Para mejorar el rendimiento computacional que encontramos al aumentar el numero de arboles ,  se recomienda balancear clases desbalanceadas de las muestras de sitios legítimos y phishing.
