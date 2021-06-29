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

### Clase 4: De paneles de datos al DataFrame
**¿Que es un DataFrame ?**
Es una estructura bidireccional donde las columnas  contiene varias categorías de datos que pueden se de tipo texto, fecha, números flotante o decimales etc.
Para mas información te dejo la documentación del [DataFrame](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html)

**Creando un DataFrame**
```
import pandas as pd
import numpy as np

dict_data = {
    'edad': [10,9,13,14,12,11,12],
    'cm': [115,110,130,155,125,120,125],
    'pais':['co','mx','co','mx','mx','ch','ch'],
    'genero':['M','F','F','M','M','M','F'],
    'Q1':[5,10,8,np.nan,7,8,3],
    'Q2':[7,9,9,8,8,8,9]
}

```
Creamos un diccionario donde las llaves se convierte en las columnas y los valores ahora son los valores de la columnas

    pd.DataFrame(dict_data)

 
(img pandas2)

**Cambiar los indices del DataFrame**
Para cambiar los indices se tiene que usar el argumento “index” y el indice tiene que tener la misma cantidad de elemento que el indice de defecto.

    inx=['benito','ana','erika','daniel','camilo','fabian','gabriela']
    df=pd.DataFrame(dict_data,index=inx)

(img pandas3)

**Métodos  que puedes usar en un dataFrame:**
Muchos de los métodos usado en una Series también se aplican para un dataFrame

**df.index** :permiten visualizar los indices de del dataframe

    df=pd.DataFrame(dict_data,index=inx)
    df.index
    #-> Index(['benito', 'ana', 'erika', 'daniel', 'camilo', 'fabian', 'gabriela'], dtype='object')

**df.columns**: permite visualizar todas las columnas del dataFrame

    df.columns
    #-> Index(['edad', 'cm', 'pais', 'genero', 'Q1', 'Q2'], dtype='object')

**df.values**: muestra solo los valores que contiene el DataFrame

    df.values

**df.shape**:muestra la dimensión del dataframe

    df.shape
    #-> (7, 6) 7 filas y 6 columnas

Recuerda que en la [documentación](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html) puedes encontrar mas métodos que se pueden usar en un DataFrame. yo solo te muestro algunos. 

**Sub Conjunto [columnas]**
Imagina que necesitamos trabajar solo con un sub conjunto de datos ejemplo un sub conjunto de la edad, centímetros, país y genero.

    df_new = df[['edad','cm','pais','genero']]

En caso de necesitar una solo elemento 

    df_new = df['edad']

(img pandas4)

**sub conjunto [filas][columnas]**
Para seleccionar un sub conjunto de las filas hay solo dos opciones **loc** y **iloc** 

**df.loc[<nombre_indice>,<nombre_columna>]**:muestra las filas por su nombre de indices y/o columnas. Ejemplo.

df.loc['ana']:muestra la información de ana

    df.loc['ana']

(img pandas5)
En caso de necesitar seleccionar de esa fila con indice  'ana' solo columnas edad y país  

    df_new.loc['ana',['edad','pais']]

(img pandas6)

Ahora si yo quiero traer varios estudiantes que se muestre solo su edad, país y genero. Lo hago así. 

    df_new.loc[['ana','gabriela','camilo'],['edad','pais','genero']]

(img pandas7)

df.iloc[<posision_indice>,<posicion_columna>]:muestra las filas por su posición de los indices y/o columnas. Ejemplo.
supongamos que queremos de gabriela su país

    df_new.iloc[6,2]
    #-> ch
    #gabriela esta en la posición 6
    # y el país esta en la posición 2 
	
Ahora si queremos ademas del país traer el genero 

    df_new.iloc[6,[2,3]]

(img pandas8)
Finalmente si quiero mostrar varios estudiante con su país y genero lo hago de la siguiente manera.

    df_new.iloc[[2,3,6],[2,3]]
(img pandas9)
	

Filtros Basado en Condiciones 
Supongamos que queremos todos los estudiantes que su edad sea mayor e igual  a 12 años.

 1. Lo primero que are es crear una condición 
		 
		 df['edad']>=12

(img pandas10)
		
 2. luego esa condición se anida dentro del corchetes con nombre de columna indicado en este caso edad

    	df.edad[df['edad']>=12]
    	#solo muestra los registro cuya edades son mayor a 12 años 
    
   También es equivalente 
	
  	df.edad[df.edad>=12]

**Condiciones Múltiples**
También podemos filtrar con condiciones múltiples de la siguiente manera 

    df[(df.edad>=12) & (df.pais=='mx')]
	
otra forma mas elegante de filtrar es usando query

    df.query( 'edad >= 12 and pais == "mx" ')

Se obtiene el mismo resultado que anidando las condiciones y se ve mucho mejor 
