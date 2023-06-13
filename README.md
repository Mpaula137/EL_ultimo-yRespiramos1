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
