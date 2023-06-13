# EL_ultimo-yRespiramos1
Ultimo taller de programación sobre diccionarios, manejo de diccionarios. 
## Primer punto:
- Desarrollar un algoritmo que imprima de manera ascendente los valores (todos del mismo tipo) de un diccionario.
```
def ingresar_diccionario(): #Funcion para ingresar el diccionario
    diccionario = {} #se almacenara el diccionario
    cadena = input("Ingresa el diccionario en formato clave:valor, separando cada par con comas: ")

    # Separar la cadena en pares clave:valor
    pares = cadena.split(",")

    for par in pares: # procesa los pares "A:c"
        clave, valor = par.split(":") 
        diccionario[clave.strip()] = valor.strip() #se almacenara en en dicionaliro quitando los espacios en blanco 

    return diccionario


def imprimir_valores_ascendentes(diccionario): #función para imprimir los valores del en orden ascendete
    valores = list(diccionario.values())
    valores.sort()  # Ordenar los valores de manera ascendente

    for valor in valores:
        print(valor)

diccionario= ingresar_diccionario()
print ("Este es tu dicionario", diccionario)
print (imprimir_valores_ascendentes(diccionario))
```
## Segundo Punto:
- Desarrollar una funci�on que reciba dos diccionarios como par�ametros y los mezcle, es decir, que se construya un nuevo diccionario con las llaves de los dos diccionarios; si hay una clave repetida en ambos diccionarios, se debe asignar el valor que tenga la clave en el primer diccionario.
```
def ingresar_diccionario(): #Funcion para ingresar el diccionario
    diccionario = {} #se almacenara el diccionario
    cadena = input("Ingresa el diccionario en formato clave:valor, separando cada par con comas: ")

    # Separar la cadena en pares clave:valor
    pares = cadena.split(",")

    for par in pares: # procesa los pares "A:c"
        clave, valor = par.split(":") 
        diccionario[clave.strip()] = valor.strip() #se almacenara en en dicionaliro quitando los espacios en blanco 

    return diccionario

def mezclar_diccionarios(diccionario1, diccionario2):
    """
    Mezcla dos diccionarios en uno nuevo, asignando valores del primer diccionario a claves repetidas.

    Args:
        diccionario1 (dict): El primer diccionario.
        diccionario2 (dict): El segundo diccionario.

    Returns:
        dict: Un nuevo diccionario mezclado.
    """
    mezcla_diccio = diccionario1.copy()  # Copiar el primer diccionario y se almacena en la variable

    for clave, valor in diccionario2.items(): # ciclo for par cada clave y valor en los itms del dicionario 2
        if clave not in mezcla_diccio: #si la clave no esta en la variable
            mezcla_diccio[clave] = valor #se agrega 

    return mezcla_diccio

diccionario1= ingresar_diccionario()
print ("Este es tu dicionario", diccionario1)
diccionario2= ingresar_diccionario()
print ("Este es tu dicionario", diccionario2)

dic_mezclado = mezclar_diccionarios(diccionario1, diccionario2)
print(dic_mezclado)
```
## Tercer punto:
- Dado el JSON:
Cree un programa que lea de un archivo con dicho JSON y:

Imprima los nombres completos (nombre y apellidos) de las personas que practican el deporte ingresado por el usuario.
Imprima los nombres completos (nombre y apellidos) de las personas que est�en en un rango de edades dado por el usuario.
```
import json

def leer_archivo_json(nombre_archivo):
    with open(nombre_archivo, 'r', encoding='utf-8') as archivo:
        contenido = json.load(archivo)
    return contenido

def obtener_nombres_completos_por_deporte(json_data, deporte):
    nombres_completos = []

    for persona, datos in json_data.items():
        if 'deportes' in datos and deporte in datos['deportes']:
            nombres_completos.append(datos['nombres'] + ' ' + datos['apellidos'])

    return nombres_completos

def obtener_nombres_completos_por_rango_edades(json_data, edad_min, edad_max):
    nombres_completos = []

    for persona, datos in json_data.items():
        if 'edad' in datos and edad_min <= datos['edad'] <= edad_max:
            nombres_completos.append(datos['nombres'] + ' ' + datos['apellidos'])

    return nombres_completos

# Leer el archivo JSON
json_data = leer_archivo_json('data.json')

# Obtener deporte ingresado por el usuario
deporte = input("Ingresa el deporte: ")

# Obtener nombres completos por deporte
nombres_por_deporte = obtener_nombres_completos_por_deporte(json_data, deporte)
print("Nombres completos de personas que practican", deporte)
for nombre in nombres_por_deporte:
 print(nombre)

# Obtener rango de edades ingresado por el usuario
edad_min = int(input("Ingresa la edad mínima: "))
edad_max = int(input("Ingresa la edad máxima: "))

# Obtener nombres completos por rango de edades
nombres_por_rango_edades = obtener_nombres_completos_por_rango_edades(json_data, edad_min, edad_max)
print("Nombres completos de personas en el rango de edades", edad_min, "a", edad_max)
for nombre in nombres_por_rango_edades:
    print(nombre)

```
## Cuarto Punto:
- El siguiente código contiene un JSON con el pronostivo detallado del clima para 8 días:
```
import json
from datetime import datetime

# Cargar el archivo JSON
jsonString = '''
{\"dt\": {\"0\": 1685116800, \"1\": 1685203200, \"2\": 1685289600, \"3\": 1685376000, \"4\": 1685462400, \"5\": 1685548800, \"6\": 1685635200, \"7\": 1685721600}, \"sunrise\": {\"0\": 1685097348, \"1\": 1685183745, \"2\": 1685270143, \"3\": 1685356542, \"4\": 1685442942, \"5\": 1685529342, \"6\": 1685615743, \"7\": 1685702145}, \"sunset\": {\"0\": 1685143042, \"1\": 1685229458, \"2\": 1685315875, \"3\": 1685402291, \"4\": 1685488708, \"5\": 1685575124, \"6\": 1685661541, \"7\": 1685747958}, \"moonrise\": {\"0\": 1685118300, \"1\": 1685207460, \"2\": 1685296620, \"3\": 1685385720, \"4\": 1685474880, \"5\": 1685564220, \"6\": 1685653740, \"7\": 1685743500}, \"moonset\": {\"0\": 0, \"1\": 1685164320, \"2\": 1685253000, \"3\": 1685341560, \"4\": 1685430120, \"5\": 1685518740, \"6\": 1685607600, \"7\": 1685696640}, \"moon_phase\": {\"0\": 0.22, \"1\": 0.25, \"2\": 0.28, \"3\": 0.31, \"4\": 0.35, \"5\": 0.38, \"6\": 0.41, \"7\": 0.45}, \"pressure\": {\"0\": 1011, \"1\": 1012, \"2\": 1012, \"3\": 1012, \"4\": 1012, \"5\": 1012, \"6\": 1012, \"7\": 1011}, \"humidity\": {\"0\": 85, \"1\": 61, \"2\": 68, \"3\": 74, \"4\": 84, \"5\": 66, \"6\": 81, \"7\": 82}, \"dew_point\": {\"0\": 23.93, \"1\": 22.5, \"2\": 23.67, \"3\": 23.35, \"4\": 24.22, \"5\": 22.73, \"6\": 22.58, \"7\": 24.02}, \"wind_speed\": {\"0\": 2.94, \"1\": 2.95, \"2\": 2.88, \"3\": 2.76, \"4\": 2.77, \"5\": 2.97, \"6\": 2.94, \"7\": 2.79}, \"wind_deg\": {\"0\": 196, \"1\": 182, \"2\": 182, \"3\": 177, \"4\": 183, \"5\": 193, \"6\": 195, \"7\": 181}, \"weather\": {\"0\": {\"id\": 804, \"main\": \"Clouds\", \"description\": \"overcast clouds\", \"icon\": \"04n\"}, \"1\": {\"id\": 500, \"main\": \"Rain\", \"description\": \"light rain\", \"icon\": \"10d\"}, \"2\": {\"id\": 803, \"main\": \"Clouds\", \"description\": \"broken clouds\", \"icon\": \"04d\"}, \"3\": {\"id\": 803, \"main\": \"Clouds\", \"description\": \"broken clouds\", \"icon\": \"04d\"}, \"4\": {\"id\": 804, \"main\": \"Clouds\", \"description\": \"overcast clouds\", \"icon\": \"04n\"}, \"5\": {\"id\": 803, \"main\": \"Clouds\", \"description\": \"broken clouds\", \"icon\": \"04n\"}, \"6\": {\"id\": 803, \"main\": \"Clouds\", \"description\": \"broken clouds\", \"icon\": \"04n\"}, \"7\": {\"id\": 803, \"main\": \"Clouds\", \"description\": \"broken clouds\", \"icon\": \"04d\"}}, \"clouds\": {\"0\": 100, \"1\": 100, \"2\": 66, \"3\": 64, \"4\": 98, \"5\": 67, \"6\": 83, \"7\": 60}, \"pop\": {\"0\": 0, \"1\": 0.2, \"2\": 0, \"3\": 0, \"4\": 0.4, \"5\": 0, \"6\": 0, \"7\": 0}, \"uvi\": {\"0\": 0, \"1\": 1.36, \"2\": 2.29, \"3\": 1.85, \"4\": 0, \"5\": 1.89, \"6\": 2.24, \"7\": 1.42}}
'''

# Convertir el JSON en un diccionario de Python
data = json.loads(jsonString)

# Obtener la cantidad de registros en los datos
numerecord = len(data['dt'])

# Iterar sobre cada registro y mostrar la fecha y hora local correspondiente
for i in range(numerecord):
    timestamp = data['dt'][str(i)]
    sunrise_timestamp = data['sunrise'][str(i)]
    sunset_timestamp = data['sunset'][str(i)]

    date = datetime.fromtimestamp(timestamp)
    sunrise = datetime.fromtimestamp(sunrise_timestamp)
    sunset = datetime.fromtimestamp(sunset_timestamp)

    print(f"Registro {i+1}")
    print("Fecha y hora:", date)
    print("Amanecer:", sunrise)
    print("Atardecer:", sunset)
    print()

```
## Quinto Punto:
- A través de un programa conectese a al menos 3 API's , obtenga el JSON, imprimalo y extraiga los pares de llave : valor.
```
import requests

def get_json_and_extract_pairs(url):# Función para obtener el JSON de una API y extraer los pares clave-valor
    respuesta = requests.get(url)
    respuesta.raise_for_status()  # Comprobar si hay errores en la respuesta
    json_data = respuesta.json()

    print("JSON de la API:")# Imprimir el JSON completo
    print(json_data)
    print()

    print("Pares clave-valor:")# Extraer y mostrar los pares clave-valor
    for key, value in json_data.items():
        print(key, ":", value)
    print()

# Ejemplo de uso con tres APIs diferentes
api_urls = [                                    
    "https://api.example.com/endpoint1",
    "https://api.example.com/endpoint2",
    "https://api.example.com/endpoint3"
]

for url in api_urls:
    try:
        get_json_and_extract_pairs(url)
    except requests.exceptions.RequestException as e:
        print("Error al realizar la solicitud:", e)
        print()

```
Admito que utilice chat gpt para los últimos dos puntos, pero no hubiera podido no me corria:/
