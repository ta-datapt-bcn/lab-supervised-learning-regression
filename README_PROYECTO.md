PR-06-ML-Credit-Card-approval

Integrantes del equipo:
  - Gloria Camps
  - Xavier Estevan
  - Marcos Palacios
  - Joan Uruén

Fecha de entrega:
  - 10/07/2021

Objetivo del proyecto:

  Realización de predicciones de datos mediante la utilización de algoritmos de Machine Learning, el dataset ha sido asignado por los profesores del centro.
  Los data sets estan compuestos por información personal de clientes (renta,activos, estado familiar,etc) de un banco y su historial crediticio (estado de pago de los créditos), 
  nuestro objetivo como data analysts es realizar una predicción acerca de cual va a ser la distribución de los clientes según su estado crediticio (variable dependiente), 
  enfocando nuestro target sobre todos aquellos clientes que han solicitado alguna vez algún crédito al banco y no lo han pagado a tiempo.
  


Flujo de Trabajo:

  1. Descarga de los datasets:
    - application_record.csv --> BD que contiene datos personales de los clientes del banco.
    - credit_record.csv --> BD que contiene información referente al historial crediticio de los clientes (es de carácter mensual).
    
    fuente: https://www.kaggle.com/rikdifos/credit-card-approval-prediction
    
  2. Importación de librerías y carga de los datos
  
  3. Exploración de los datos:
      - Identificación del significado de las variables de los datasets.
      - Características generales (Número de registros, tipo de datos, existencia de nulos,etc).
      - Identificación de existencia de colinealidad entre variables independientes.
      
  4. Creación de la variable dependiente (NEW STATUS)
      - EL DATA SET NO DISPONÍA DE UNA VARIABLE DEPENDIENTE, por lo que nos hemos visto obligados a crear una. Nuestra variable endogena ha sido creada a partir de
        la variable STATUS*.
        
        Criterios utilizados para crear la variable objetivo:
        
        - Filtramos la lista de aquellos clientes que son clientes actualmente.
        - Selección de el estado más repetido del cliente a lo largo del tiempo mediante la medida de centralización, moda.
        - Todos aquellos clientes que hayan tenido en alguna ocasión el estado 5 (morosidad), serán catalogados con ese estado. 
        - Clasificamos la variable objetivo en 3 principales categorías:
            1. Clientes que pagan a tiempo (agruapación de status X y C)
            2. Clientes que pagan con retraso (agrupación de status 0,1,2,3,4)
            3. Clientes morosos (todos aquellos clientes que han tenido alguna vez un status 5)
         
        *Nota: Esta variables nos especifica cual es el estado del crédito de nuestro cliente de forma mensual.
        Status:
        0: 1-29 days past due 
        1: 30-59 days past due 
        2: 60-89 days overdue 
        3: 90-119 days overdue 
        4: 120-149 days overdue 
        5: Overdue or bad debts, write-offs for more than 150 days 
        C: paid off that month 
        X: No loan for the month
        
  5. Limpieza de datos
    - Calculamos la edad de los clientes.
    - Calculamos el número de años trabajados y asignamos a una clasificación númerica según el volumen de estos.
    - Transformación de variables categóricas a númericas (carácter binario: 0 y 1).
    - Eliminación de los datos de aquellas variables que contienen un alto % de valores nulos y de aquellas que no nos aportan insights.

  6. Anexión de los dos datasets, creando así la base de datos final 
  
  7. Análisis de correlaciones
    - Realización de matriz de correlación, observamos que existe muy poca correlación entre nuestras variables exógenas y la variable objetivo (NEW STATUS)
    
  8. Análisis de PCA
    - Estandarizamos los valores (ajustar los valores medidos en diferentes escalas respecto a una escala común)
    - Visualización de datos (scatter plot)
    - Observamos que existe una muy baja separabilidad de las observaciones correspondientes a la variable objetivo.
    - Esto puede ser consecuencia de la poca influencia que ejercen las variables independientes sobre la variable dependiente.

  9. Evaluación de Modelos de ML
    - Asignación de variables X e y
    - Realización de un train_test_split (siendo el test_size= 0.2, un 20% de los datos)
    - Creación de la Pipeline:
        - Estandarización de las variables mediante un MinMaxScaler()
        - Balanceamiento de datos, mediante un oversample (añadimos observaciones en el grupo menos voluminoso)
        - Aplicación de modelo de ML:
            - Logistic Regression
            - KNN
            - SVC
            - Decision Tree
            - Random Forest
            - XGBoost
            
       - Visualización de los datos mediante una Matriz de Confusión
       - Evaluación de los resultados de los modelos, centramos nuestro foco sobre los aciertos del grupo 2, Clientes que pagan con retraso.
       - Selección de los dos mejores modelos:
         
                          
            - KNN: 
                - Score del modelo:  0,75    
                - Recall grupo 2: 0,8
                -
            - XGBoost:     
                - Score del modelo:  0,84 
                - Recall grupo 2: 0,93
          
  10. Optimización de los modelos seleccionados (KNN & XGBoost)
    - Optimización en la selección de  parametros de cada uno de los modelos seleccionados mediante un GridSearch()
    - Entrenamiento de los datos y predicción de los datos testeados.
    - Comparación de Modelo Original con Modelo Optimizado
    - Observamos una ligera mejora en la predicción de los modelos



  
  


