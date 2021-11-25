# PANDAS

## Importación
  > import pandas as pd

  > import numpy as np

## Cheat sheet

### SERIE
_Una serie es un arreglo de una dimension_

```python
serieP = pd.Series([10, 20, 30, 40, 50],dtype=np.float32)
serieP = pd.Series([10, 20, 30, 40, 50],dtype=np.int32, index=['a','b','c','d','e'])
serieP = pd.Series({'a':10,'b':200,'c':300}) # Diccionario
serieP = pd.Series(np.arange(4))

# Modificacion
serieP.name = 'Numeros'
serieP.index
serieP.index.values
serieP.index.tolist()
serieP.index.name = 'indices'

# NULOS
# np.NaN
# pd.isnull(serieP)
# pd.notnull(serieP)
serieP.isnull()
serieP.dropna() # Elimina los valores nulos
serieP.fillna(99) # Reemplaza nulo por 99
serieP[serieP.notnull()] # Serie de datos no nulos

```
### DATAFRAME

```python

------------------------------------
usuarios = {
    'nombre':["mayu","shirley","ines","karina"],
    'calificaciones':[9,10,4,9.5],
    'edad':[23,17,20,34],
    'aprobado':[True, False, True, True]
}

------------------------------------

users = pd.DataFrame(usuarios,index=['a','b','c','d'],columns=['nombre','calificaciones'])

# Ver la cantidad de NULOS por variable
data.isna().sum().sort_values(ascending=False)

users.columns = ['nombre1','calificaciones1']
users.index = '1a','2b','3c','4d'
users.rename(columns={'nombre1':'nameHM'})

# Aplicar una funcion a una columna en especifico
users['calificaciones1'] = users.apply(lambda row: row['calificaciones1'] + 1 , axis=1) #axis = 1 <> filas

# EXTRAER DATOS DESDE UN ARCHIVO CSV
# ------------------------
userdf = pd.read_csv('./datasets/users.csv', delimiter=",", header=5, index_col=0 )
userdf = pd.read_csv('./datasets/users.csv', delimiter=",")
paisesdf = pd.read_csv('./datasets/paises.csv', 
                       usecols=['pais','poblacion','long','lat'],
                      na_values=['N/S'],index_col='id')
paisesdf.head(3)
paisesdf.tail(3)
# ------------------------

# Filtros de Dataframes
paises = paisesdf[paisesdf.poblacion.notnull()] # Solo filas sin nulos
paises.poblacion = paises.apply(lambda row: int(str(row['poblacion']).replace('.','')), axis=1)

# ORDENAR Dataframes
paises.sort_index(ascending=False) #Ordenar por INDEX
paises.sort_values('poblacion',ascending=False) #Ordenar por valores de una COLUMNA
paises.sort_values('poblacion',ascending=False).head(3)

# CRUD DATAFRAME
df = pd.DataFrame(np.arange(16).reshape(4,4), 
             columns=list('ABCD'),
            index=list('abcd'))
# Crear una columna
df.insert(1,'Z',[100,200,300,400]) # SI MODIFICA al Dataframe
df.assign(Z2 =[100,200,300,400])  # NO MODIFICA al Dataframe

# Eliminar
df.drop('D', axis=1) # axis=1 <> Columnas
df.drop('b', axis=0) # axis=0 <> Fila

# Actualizar
df['B']=10,20,30,40 # Columnas
df.B['b'] = 50 # Valor especifico

```

DATAFRAME FILTRO CON QUERY

```python

# data[data['age']>40]['name']
data.query('age > 40')

# data[(data['age']>40) & (data['gender'] == 'female')]
data.query('age > 40 and gender == "female"')

# data[~data['email'].str.endswith('@example.com')]
data.query('~email.str.contains("@example.com")')

# data[(data['country'].isin(["Germany","Finland","Canada"]))].count()
data.query('country in ("Germany","Finland","Canada")')

# data[(data['gender'] == 'female') & (data['country']== "Germany")]
data.query('gender == "female" and country == "Germany" ')
```

GUARDAR ARCHIVOS .CSV

```python
paises.to_csv('./datasets/paisesNew.csv')
paises.to_csv('./datasets/paisesNew.csv', 
              columns=['pais','poblacion'],
              index=False
             )  # columnas especificas y sin indice
```

LOC - && -  ILOC

```python
------------------------------------
usuarios = {
    'nombre':["mayu","shirley","ines","karina",'marilu'],
    'calificaciones':np.random.randint(5,10,5),
    'edad':np.random.randint(15,30,5),
    'email':["mayu@aa","shirley@aa","ines@bb","karina@bb",'marilu@aa'],
    'aprobado':[True, False, True, True, False]
}
pd.DataFrame(usuarios)
df = pd.DataFrame(usuarios, index=list('abcde'))
------------------------------------

# ------- LOC

df.loc['a':'c','nombre']
df.loc['a':'c',['nombre','edad']]
df.loc[df.calificaciones > 5, ['nombre','edad']]
df.loc[df.calificaciones > 5, ['nombre','edad','calificaciones']
      ].sort_values('calificaciones', ascending=False).head(2)

userdf.loc[(userdf['edad'] > 70) & (userdf.genero == 'female') ,'nombre']
userdf.loc[~userdf['email'].str.endswith('@gmail.com'),'nombre']

(userdf.loc[userdf['pais'].isin(['Germany','Finland','Canada']),['nombre','pais']]).head(3)

userdf.loc[(userdf['edad'] > 20) & (
    userdf.genero == 'female') & (
    userdf['pais'].isin(['Germany','Finland','Canada'])
),['nombre','email','pais']]
# ------- ILOC
df.iloc[0:4,1:3]
df.iloc[0:4,[0,2]]
```

AGRUPAMIENTO

```python
------------------------------------
frutas = {
    'nombre':['Naranja','Manzana','Manzana','Pera','Naranja','Manzana','Sandia'],
    'color':['Naranja','Rojo','Verde','Verde','Naranja','Rojo','Rojo'],
    'cantidad': np.random.randint(5,10,7),
    'precio': np.random.randint(1,5,7),
}
fruitdf = pd.DataFrame(frutas)
------------------------------------

fruitdf.groupby('nombre')
fruitdf.groupby('nombre').cantidad.sum()

# to_frame <> Crear un new dataframe
fruitdf.groupby('nombre').cantidad.sum().to_frame('cantidad')

# Agrupar + agregar un filtro
fruitdf.groupby('nombre').filter(lambda fruta: fruta.cantidad.sum() > 10)

# Agrupar +  filtro + agrupacion
fruitdf.groupby('nombre').filter(lambda fruta: fruta.cantidad.sum() > 10
                                ).groupby('nombre').cantidad.sum()

# Filtro + agrupacion
fruitdf[fruitdf.nombre == 'Manzana'].groupby('color').cantidad.sum() 

# Agrupar por columna y sacar conteo
data.groupby('gender')['gender'].count()
data.value_counts(data['gender']) 
data.groupby('gender').agg({'gender':'count'}) 
data.groupby('gender')['gender'].agg('count')

# Filtros + agrupar + ordenar
data[data['gender']=='female'].groupby('country')['country'].count(
).sort_values(ascending=False).head(3)
```
