# NUMPY

## Importacion
  > import numpy as np

## Cheat sheet


### LISTA

```python
lista = [1.73, 1.68, 1.71, 1.89, 1.79] # Lista
lista.shape # Fila,Columna

type(lista) # Saber el TIPO de mi VARIABLE

# Agregar valor a la lista
lista.append(10)

# Remover valor a la lista
lista.remove(1.68)
```

### ARREGLO

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
np.array([0,3,6],dtype=np.uint) # Entero sin signo
# np.array([0,1,0],dtype='?')
np.array([0,1,0],dtype=np.bool) # Mas recomendable
np.array([0,1,0],dtype=np.str) # Mas recomendable
np.array([1,2,0,4,5,'6'],dtype=np.complex) 

# CREAR ARREGLO
np.arange(0,10) # RANGO (Nro INICIO, Nro FIN)
np.arange(3, 10, 5) # RANGO (Nro INICIO, Nro FIN, SALTO)
np.linspace(3, 10, 5) # (Nro INICIO, Nro FIN, PARTICION)

np.zeros(5) # Arreglo unidimensional - 5 ceros
np.ones((4, 5),dtype=np.int32) # Arreglo bidimensional de 1's (fila, columna)
np.empty(10, dtype=np.int) # Crear arreglo con valores cualquiera
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
np.corrcoef(nArray1,nArray2) # Correlaci??n
np.std(nArray) # Desviaci??n estandar
np.column_stack((nArray1,nArray2)) # Juntar como 2 columnas
np.transpose(...) # Tranpuesta de la matriz
np.sort(nArray, order = 'llave') # Ordenar el array

# Creando MUESTRAS ALEATORIAS con DISTRIBUCION NORMAL
# np.random.normal(loc:Media, scale:Standard desviation ,size:# muestras)
arr_example = np.round(np.random.normal(1.75, 0.20, 5000),2)

# OTRO MODO DE GENERAR ARRAY
cabeceras = [ ('nombre', 'S10' ), ('edad', int) ]
datos = [ ('Heydy', 10), ('Maria', 70), ('Javier', 42), ('Samuel', 15) ]

usuarios = np.array(datos, dtype = cabeceras)
np.sort(usuarios, order = 'edad' )

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

```

### MATRIZ

```python
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

### ARCHIVOS - NUMPY
```python
nArray=np.arange(20)

np.savetxt('./ejemplo.csv',nArray,delimiter=";") # Guardar en un archivo mi data
np.loadtxt('./ejemplo.csv',delimiter=";") # Cargar mi data

np.save('ejemplo.npy',nArray) # genera un archivo binario
np.load('ejemplo.npy')

np.savez('ejemplo.npz',nArray) # Almacenar en archivos binarios comprimidos
np.load('ejemplo.npz')['arr_0']

# Archivos pocos convencionales
# Para leer archivos de forma flexible
# skip_header=1 <> Que la lectura inicie despues de la fila 1
np.genfromtxt('./datasets/paises.txt', usecols=[1,2],skip_header=1, 
              comments="#", delimiter=",") # , skip_footer=0
```