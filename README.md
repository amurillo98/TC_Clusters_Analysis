# TC_Clusters_Analysis
Análisis del Comportamiento de tarjetahabientes de una institución bancaria "BLUE" en los últimos 6 meses y clasificación de los usuarios para una óptima gestión del negocio


# Introducción
Actualmente, la inteligencia artificial (IA) y el machine learning son herramientas fundamentales para analizar información y predecir comportamientos de manera eficiente. Estas tecnologías permiten a las empresas no solo incrementar sus ganancias, sino también identificar patrones específicos y personalizar productos y servicios para satisfacer las necesidades de sus clientes. En el sector bancario, en particular, la IA se ha convertido en una herramienta esencial para evaluar la solvencia de aquellos usuarios que desean un crédito y poder darles el mejor servicio. Sadok, H., Sakka, F., & El Maknouzi, M. E. H. (2022).

En los últimos años, el segmento de consumo y el número de tarjetahabientes han crecido significativamente. Los consumidores han aumentado el uso de tarjetas de crédito como un mecanismo rápido de acceso a crédito de consumo. Entre enero y julio de 2022, se registraron 97,2 millones de consumos con tarjeta de crédito en Ecuador, un 19% más en comparación con el mismo período del año anterior. La facturación también creció un 25%, alcanzando los USD 6.902 millones en ese mismo periodo (Primicias, 2022).

Dado este crecimiento, es esencial que las instituciones financieras analicen el perfil de los clientes con tarjeta de crédito y ofrezcan límites de crédito que se ajusten a su balance, historial de pagos, hábitos de consumo y otras variables relevantes. La creación de clusters mediante IA permite identificar patrones distintivos entre los usuarios, lo cual facilita el diseño de estrategias personalizadas para cada grupo, asegurando un tratamiento adecuado según sus características y reduciendo el riesgo de crédito de forma más efectiva.

# Metodología

![imagen](https://github.com/user-attachments/assets/454121f4-c000-4fea-830c-5f69f455be47)


Se verifica que existen 313 valores nulos, se entiende que los campos están vacios porque el cliente no ha realizado pagos mínimos; por eso se decide poner en '0'. La otra variable "credit limit" solo contiene 1 campo vacío por lo que se decide reemplazar con'0' en ambos casos.


Los histogramas previamente graficados muestran una distribución sesgada a la izquierda en las variables de "Balance", "Purchases", "Credit_limit", "Payments" y "Cash Advance", lo cual puede interpretarse como que la mayoría de usuarios realizan compras de pequeños valores por tanto su límite de crédito se concentra en valores pequeños, así mismo el pago de sus tarjetas.

Por otro lado la antiguedad de la tc "Tenure" es de un año, es decir, se entiende que el comportamiento de estos usuarios se puede interpretar de mejor forma porque tienen una antiguedad suficiente con la tarjeta de crédito para ser analizados.

Existe otro tipo de variables como "Purchase_Frequency" que se concentran en los extremos, es decir o no tienen casi frecuencia de compra o si compran frecuentemente (es de extremos - uno de los dos).

![imagen](https://github.com/user-attachments/assets/c6d076dd-baa9-4093-b6ef-61b63ca43370)



Se procedió a realizar un análisis de correlación entre las variables que contiene el dataset; sin embargo por la cantidad de variables existentes se hizo un filtro para seleccionar aquellas que pueden tener una mayor importancia en el análisis.

De esta forma resulta interesante destacar que la variable "Balance" tiene una correlación positiva con el "Cash_advance", asimismo con el "Credit_limit", lo cual puede deberse a que las personas que tienen un balance mayor tienen un bajo nivel de liquidez a nivel de efectivo y una necesidad mayor de tener este flujo de liquidez; por otro lado, se puede interpretar que aquellos usuarios que tienen un nivel de límite de crédito superior poseen un perfil que les permite retirar una cantidad mayor de efectivo.

Existen también otro tipo de relaciones que se entienden por la misma naturaleza de las variables como aquella entre los pagos y las compras, es decir, a mayor monto de compras con las tarjetas más es el monto de pagos que realizan los usuarios. De igual forma, mientras mayor es el monto de cash advance también hay una relación positiva con la frecuencia con que se realiza el cash advance.

![imagen](https://github.com/user-attachments/assets/854f9950-a1a9-4659-981d-60c9e7fb9010)




Creacion de variables

Dos categóricas:

- 'Antiguedad TC': Con el propósito de agrupar aquellos clientes con una TC de 1 año, es decir que tienen experiencia de crédito (que representa la mayoría), con 6 meses hasta menos de 12 meses distinguiéndolos como usuarios con poca experiencia y aquellos sin experiencia que son clientes nuevos con TC con una antiguedad menor a 6 meses. 

- 'Límite de Crédito': Se creó esta agrupación para establecer una segmnentación de crédito en función al perfil del usuario, es decir, se entiende que los que tienen mayor límite de crédito tienen mayores ingresos o una mayor capacidad de pago que permiten justificar el cupo que se les otorga, de la misma forma funciona de manera inversa. 

Dos continuas por su relevancia e interés en el análisis:

- 'CREDIT_UTILIZATION_RATIO': Variable que permite identificar el ratio de crédito que está utilizando el cliente sobre el cupo disponible, ya que generalmente se considera en riesgos que si se tiene un cupo de utilización muy alto y cerca del límite se entiende como un mayor riesgo de crédito.

- 'PAYMENT_RATIO': Variable que permite calcular la proporción de pagos que están haciendo los usuarios frente a su balance. Así se entiende que mientras mayor es el ratio de signfica que los usuarios están siendo resposables con los pagos que les correponden y visceversa.

#Procesamiento de Datos

Se procedió a quitar la columna de identificación del cliente, ya que no contribuye al poder de predicción del modelo.


![imagen](https://github.com/user-attachments/assets/9f606504-e0c5-4416-8a2a-d6608c947f4a)

![imagen](https://github.com/user-attachments/assets/d7d0cd10-3292-40b9-8467-ed5c5eeff3c7)

Se puede ver a través de los gráficos que existe un sesgo hacia la izquierda para las tres variables que se graficaron en función a las variables categóricas creadas: Antiguedad_TC y Límite_Crédito. Si bien se observa que para Antiguedad_TC predominan los clientes determinados con experiencia, mientras que en Límite_Crédito la segmentación se encuentra mejor distribuida, si bien predominan aquellos clasificados en el segmento de límite de crédito medio.

#El diagrama de cajas

Muestra la distribución de Balance en las diferentes categorías de Límite_crédito, existe una relación evidente en donde mientras mayor es el límite de crédito del usuario de TC, mayor balance tendrá. Resulta interesante ver que para los rangos de "Alto" y "Muy Alto", el rango intercuartil es más amplio, lo que implica mayor variabilidad en el balance de los usuarios de aquellos grupos. De esta forma, los clientes con límites de crédito más altos (especialmente en "Muy Alto" y "Alto") podrían estar utilizando más de su crédito, lo que conlleva a que tengan balances más altos. Esto puede ser indicativo de un mayor nivel de gasto o una tendencia a mantener un balance alto en lugar de pagarlo por completo cada mes.

![imagen](https://github.com/user-attachments/assets/6976e3cc-6a95-4a06-9c5d-bffd172289e3)


#Entrenamiento y Tuneo de Hiperparámetros


#Interpretación de los Clusters

Se puede concluir a partir de la segmentación realizada que:

El cluster 3 destaca como el grupo con los clientes de mayor estabilidad financiera, pues tienen tanto altos balances como límites de crédito elevados. Este grupo podría incluir clientes de alto valor para la institución.

Mientras que el cluster 0 parece representar clientes con límites de crédito bajos y balances negativos, posiblemente indicando un perfil de riesgo más alto o clientes nuevos, por lo que se podría tomar en cuenta para mayor observación ya que podrían caer en default y ser representar una pérdida para la institución.

Cluster 1 y Cluster 4 tienen una dispersión significativa en BALANCE y CREDIT_LIMIT, sugiriendo perfiles variados, lo cual podría indicar una combinación de clientes con diferentes perfiles de riesgo y necesidades de crédito; dando a entender que pueden ser buenos o clientes asimismo clientes más riesgosos.

Cluster 2 muestra balances y límites de crédito moderados, con poca variabilidad, lo que sugiere un grupo de clientes estables pero con menor capacidad de gasto y crédito en comparación con el cluster 3, debido a los bajos balances.

![imagen](https://github.com/user-attachments/assets/3b0d9859-fc94-4ac9-8d92-a3a5bfb77427)


#Expliquen cómo implementarían el modelo en el negocio y justifíquenlo

En el sector financiero la clusterización se utiliza para identificar patrones sospechosos de actividad fraudulentas, pudiendo agrupar las transacciones en base a criterios como la ubicación geográfica, la frecuencia y el monto para detectar actividades anómalas en el uso de tarjetas de crédito. De igual manera, al segmentarlos en grupos homogéneos les facilita la creación de estrategias marketing específicas y dirigidas a cada segmento de clientes. Al aplicar estas tácticas, las empresas pueden aumentar su lealtad y retención de clientes.

#Limitaciones
Falta de variables contextuales o demográficas que determinen el perfil del consumidor y su comportamiento de consumo. 
El registro de datos de tenure no puede ser suficiente para aquellos clientes nuevos puesto que no cuentan con un comportamiento histórico.






