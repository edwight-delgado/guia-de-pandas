# Manipulación y análisis de datos con pandas

Estas son mi notas del curso manipulación y análisis de datos con pandas de Platzi. 

## Modulo 1: ¿ Comenzando con pandas ?

### Clase 1: Que es pandas
El termino **Pandas** viene de Panel Datas,inventado por West McKinney.
Es una librería de python para manipular y análisis de grande volúmenes de datos

### Clase 2: Primeros pasos con Google Colab: configuracion del entorno de trabajo
**Que es google colab**: google colab es una herramienta poderosa donde puedes ejecutar código en python de manera interactiva usando el navegador sin necesidad de instalar nada en tu computador . solo necesitas abrir y escribir . puedes encontrar la documentación oficial [https://colab.research.google.com/](https://colab.research.google.com/)

También te comparto [notebook](https://colab.research.google.com/drive/10aWN9XYtUnhUZal-UWDhNUR8m0X3sE_C)  de google colab en blanco 

### Clase 3: Series e Indexación y selección de datos
Creando una serie. para mas información
https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.html

    import pandas as pd
    pd.Series([2,3,1,12,34,5])

**métodos que podemos usar en una Series:**

**sr = pd.Series(<list>)**  ⇒ crear una serie

    pd.Series([2,3,1,12,34,5])
    

**sr = pd.Series(dic)**  ⇒ crea una Serie con índices específicos.

    my_dic={
	    'venezuela':23,
	    'argentina':12,
	    'colombia':38
	    }
    pd.Series(my_dic)

**sr.values**  ⇒ obtener los valores de la serie

    sr = pd.Series(my_dic,index=my_dict.keys())
	sr.values
	#-> array([23, 12, 38])
**sr.index**  ⇒ obtener los índices de la serie

    sr = pd.Series(my_dic,index=my_dict.keys())
    sr.index
    #-> Index(['venezuela', 'argentina', 'colombia'], dtype='object')

**sr.shape**  ⇒ obtener la dimensión
	
    sr = pd.Series(my_dic,index=my_dict.keys())
    sr.shape
    #-> (3,)

**sr[< index >]**  ⇒ obtener un elemento de la serie a través de un índice

    sr =pd.Series(my_dic,index=my_dict.keys())
    #En caso de indice numérico
    sr[3]
    #En caso de incice de tipo string
    sr['colombia']
	#-> 38
**sr[<list_of_indexes>]**  ⇒ obtener valores a través de una lista índices.

    #En caso de indice numérico
    sr[1:10]
    #en caso de indice de tipo string
    sr['argentina':'colombia']
    # -> argentina 12 colombia 38

**sr.isnull()**  ⇒ Lista con True cuando el valor es nulo

    import numpy as np
    my_dic={
    'venezuela':23,
    'argentina':12,
    'colombia':38,
    'chile':np.nan,
    'ecuador':np.nan
    }
    sr =pd.Series(my_dic)
    sr.isnull()
    #-> venezuela False argentina False colombia False chile True ecuador True
    

**sr.notnull()**  ⇒ Lista con True cuando el valor es no nulo

    sr.notnull()
    #-> venezuela True argentina True colombia True chile False ecuador False
  
  **sr.isnull().any()**  ⇒  Esta función adicionalmente nos regresa un booleano indicándonos si existe (TRUE) o no existe (FALSE) algún nan
  

    sr.isnull().any()
    #-> True

  **sr[sr.notnull()]**  ⇒ Nos regresa los valores de la serie que “NO” son nulos
  

    sr[sr.notnull()]
    #venezuela 23.0 argentina 12.0 colombia 38.0
    
**sr[sr.isnull()]**  ⇒ Nos regresa los valores de la serie que “SI” son nulos

    sr[sr.isnull()]
    #->chile NaN ecuador NaN

### Clase 3: De paneles de datos al DataFrame
¿que es un dataframe ?
https://pandas.pydata.org/pandas-docs/stable/reference/frame.html
