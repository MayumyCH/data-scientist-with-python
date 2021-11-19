# NUMPY

## Importacion
  > import numpy as np

## Cheat sheet

```python
lista = [1.73, 1.68, 1.71, 1.89, 1.79] # Lista
lista.shape # Fila,Columna

type(lista) # Saber el TIPO de mi VARIABLE

# -- ARREGLO es una LISTA en PYTHON
# -----------
nArray = np.array(lista) # Convertir lista => Arreglo
nArray.ndim # dimension del arreglo
nArray.size # nro elementos del arreglo
nArray.itemsize # tamanio en byte del arreglo
nArray.shape # Fila,Columna

# COPIAR un ARREGLO
e=a.copy

# SUBARRAY
nArray[1:3]
nArray[1:5:2]
nArray[::-1] # ARRAY INVERSO

lista = [0,3,6]
np_array[lista] # valores de un array de ciertos indices

# CRUD arreglo
nArray[0:3]=20
nArray[[4,6,8]]=16
nArray = np.append(nArray,88) # Agregar
nArray = np.delete(nArray,5) # Eliminar (array, posicion)

# DEFINIR TIPO DE DATO ARRAY
# np.array([0,3,6],dtype='f') 
np.array([0,3,6],dtype=np.float32) # Mas recomendable
# np.array([0,3,6],dtype='i')
np.array([0,3,6],dtype=np.int32) # Mas recomendable
# np.array([0,1,0],dtype='?')
np.array([0,1,0],dtype=np.bool) # Mas recomendable

# CREAR ARREGLO
np.arange(0,10) # RANGO (Nro INICIO, Nro FIN)
np.arange(3, 10, 5) # RANGO (Nro INICIO, Nro FIN, SALTO)
np.linspace(3, 10, 5) # (Nro INICIO, Nro FIN, PARTICION)

np.zeros(5) # Arreglo unidimensional - 5 ceros
np.ones((4, 5),dtype=np.int32) # Arreglo bidimensional de 1's (fila, columna)
np.full((3,5), 10) # [(fila, columna), nro] := Crear un Arreglo bidimensional de 10's
np.diag([1,7,3]) # Matriz diagonal con valores 1,7,3

# OPERACIONES
nArray.sum()
nArray.min()
nArray.max()
nArray.std() # Desviacion estandar de nuestro arreglo
nArray.mean() # Media de nuestro arreglo
nArray.sort() # Ascendente

np.median(nArray) # Mediana
np.corrcoef(nArray1,nArray2) # Correlación
np.std(nArray) # Desviación estandar
np.column_stack((nArray1,nArray2)) # Juntar como 2 columnas
np.transpose(...) # Tranpuesta de la matriz
np.sort(nArray, order = 'llave') # Ordenar el array

# Creando MUESTRAS ALEATORIAS con DISTRIBUCION NORMAL
# np.random.normal(loc:Media, scale:Standard desviation ,size:# muestras)
arr_example = np.round(np.random.normal(1.75, 0.20, 5000),2)

# ALEATORIOS
np.random.rand() # Un numero pseudoaleatorio entre (0;1)
np.random.random(6) # Arreglo de tamanio 6 en el rango de [0,1]
np.random.randint(0,7) # Un numero entero entre (0;7)
np.random.randint(0,7,3) # Arreglo de tamanio 3 en el rango de [0,7]
# VALOR SEMILLA aleatoria, resultados reproducibles entre simulaciones.
np.random.seed(123) 

# OPERADORES LOGICOS
newArray= nArray[nArray < 20]
newArray= nArray[(nArray < 20) & (nArray>5)]
newArray= nArray[(nArray < 20) | (nArray== 30)]

#  OPERADORES LOGICOS NUMPY
var_cond = np.logical_and(nArray >1.70,nArray <1.74)
np.logical_or()
np.logical_not()
nArray[var_cond]

np_array.shape = (3,5)   # Modifica original - Convierte de Array -> Matriz
np_array.reshape = (3,5) # Copia de original - Convierte de Array -> Matriz
# Numpy los ejes, axes, axis, y dimensiones son lo mismo

# -- MATRIZ
# -----------
matriz=np.arange(0,15).reshape(3,5)

# matriz.T
matriz.transpose()

matriz[2,4]
matriz[1, 1:4]
matriz[1,[0,2,4]]

matriz.ravel() # De una matriz a un arreglo unidimensional
matriz.flatten() # COPIA !! retorna una copia arregla unidimensional

```