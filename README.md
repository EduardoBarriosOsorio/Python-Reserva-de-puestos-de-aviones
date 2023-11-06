# Python-Reserva-de-puestos-de-aviones
Existen jets privados de 7 filas de asientos (desde la A a la G), con 3 asientos por fila(1+pasillo+2)

Se quiere desarrollar un programa para reservar asientos que sea capaz de:

Identificar asientos están disponibles y cuáles ocupados.
Mecanismo para preguntar por asientos disponibles con parametros:
Asientos individuales disponibles
Dos asientos juntos disponibles
Fila de asientos disponible
Si no hay asientos diponibles mostrar por pantalla: NO QUEDAN ASIENTOS PARA ESTE VUELO

Mecanismo que le permita realizar una reserva de asientos
Permita realizar un cálculo en el valor total de una reserva asumiendo las siguientes tarifas:
Asiento solo (i.e. A1) = 125.000 pesos.
Asiento ventana (i.e A3) = 100.000 pesos.
Asiento Pasillo (i.e A2) = 90.000 pesos.


#Pseudocódigo.

Crear matriz que represente los asientos de avion
mostrar los asientos disponibles
mostrar los asientos desocupados
cuantos asientos individuales existen disponibles
cuantos asientos juntos hay disponibles
cuantas filas completas hay disponibles
si no hay de ningun tipo disponible avisar por pantalla
Mecanismo de reserva:
  preguntar cuantos quiere comprar:
  si 1:
    ofrecer asientos individuales
    cual asiento quiere?
    confirmar costo
  si 2:
    ofrezco asientos juntos
    cual asiento quiere?
    confirmar costo
  si 3:
    ofrecer filas
    cual fila quiere?
    confirmar costo
  mostrar asiento reservado
  volver al inicio.





  #Creamos el avión.
  import numpy as np
avion = np.full((7,3),0)
filas = np.array(["A","B","C","D","E","F","G"])
print(avion)

#Identificamos asientos disponibles y asientos individuales disponibles
desocupados = []
#se identifican los asientos individuales disponibles
for i in range(0, 7):
  for j in range(0,3):
    if avion[i][j] == 0:
      desocupados.append(filas[i]+str(j+1))
      
print("Asientos disponibles: ", end='')
for asiento in desocupados:
  print(asiento, end=' ')
print("")
print("Asientos individuales disponibles: ", end='')
for asiento in desocupados:
  print(asiento, end=' ')

  #Se identifican los asientos juntos disponibles
  desocupados_2 = []
for i in range(0, 7):
  if avion[i][1] == 0 and avion[i][2] == 0:
    desocupados_2.append(filas[i]+"2"+"-"+filas[i]+"3")

print("Asientos juntos disponibles: ", end='')
for asiento in desocupados_2:
  print(asiento, end=' ')

  #Se identifican filas disponibles
  desocupados_3 = []
for i in range(0, 7):
  if not avion[i].any():        #[0,0,0] -> false -> not false ->true
    desocupados_3.append(filas[i])

print("Asientos juntos disponibles: ", end='')
for asiento in desocupados_3:
  print(f"Fila {asiento}", end=' ')

  # Mecanismo de reserva
  print("mecanismo de reserva")

cant_asientos = int(input("Ingrese el número de asientos que desea reservar"))

if cant_asientos == 1:
  print("Los asientos disponibles son: ", end='')
  for i in desocupados:
    print(i,end=' ')

  reserva = input("Ingrese el asiento que desea reservar")
  if int(reserva[1])==1:
    costo = 125000
  elif int(reserva[1])==2:
    costo = 90000
  elif int(reserva[1])==3:
    costo = 100000
  print(f"El costo de la reserva es {costo}, ?Desea continuar? S/N")

  confirmacion = input()

  if confirmacion == "S":
    for i in range(0,len(filas)):
      if reserva[0] == filas[i]:
        avion[i][int(reserva[1])-1] = 1
        print(f"Asiento {reserva} reservado")

elif cant_asientos == 2:

  print("Los asientos disponibles son: ", end='')
  for i in desocupados_2:
    print(i,end=' ')

  reserva = input("Ingrese los asientos que desea reservar")
  print(f"El costo de la reserva es 190.000, ?Desea continuar? S/N")
  confirmacion = input()
  if confirmacion == "S":
    for i in range(0,filas.size):
      if reserva[0] == filas[i]:
        avion[i][1] = 1
        avion[i][2] = 1
        print(f"Asientos {reserva} reservado")


elif cant_asientos == 3:
  print("Los asientos disponibles son: ", end='')
  for i in desocupados_3:
    print(i,end=' ')

  reserva = input("Ingrese la fila que desea reservar")
  print(f"El costo de la reserva es 315.000, ?Desea continuar? S/N")
  
  confirmacion = input()
  if confirmacion == "S":
    for i in range(0,filas.size):
      if reserva == filas[i]:
        avion[i][0] = 1
        avion[i][1] = 1
        avion[i][2] = 1
        print(f"Fila {reserva} reservada")


## TODO JUNTO!!
import numpy as np
avion = np.full((7,3),0)
filas = np.array(["A","B","C","D","E","F","G"])
print(avion)
while True:
  if avion.all():
    print("El avion esta lleno")
    break
  #Se identifican los asientos individuales disponibles
  desocupados = []
  for i in range(0, 7):
    for j in range(0,3):
      if avion[i][j] == 0:
        desocupados.append(filas[i]+str(j+1))
  #Se imprimen los asientos desocupados
  print("Asientos disponibles: ", end='')
  for asiento in desocupados:
    print(asiento, end=' ')
  print("")
  #Se imprimen los asientos individuales disponibles
  print("Asientos individuales disponibles: ", end='')
  for asiento in desocupados:
    print(asiento, end=' ')
  #Se identifican los asientos juntos disponibles
  desocupados_2 = []
  for i in range(0, 7):
    if avion[i][1] == 0 and avion[i][2] == 0:
      desocupados_2.append(filas[i]+str(2)+"-"+filas[i]+str(3))
  print("")
  #Se imprimen los asientos juntos disponibles
  print("Asientos juntos disponibles: ", end='')
  for asiento in desocupados_2:
    print(asiento, end=' ')
  #Se identifican las filas disponibles
  desocupados_3 = []
  for i in range(0, 7):
    if not avion[i].all():
      desocupados_3.append(filas[i])
  print("")
  #Se imprimen las filas disponibles
  print("Filas completas disponibles: ", end='')
  for asiento in desocupados_3:
    print(f"Fila {asiento}", end=' ')


  #Mecanismo de reserva
  print("mecanismo de reserva")


  cant_asientos = int(input("Ingrese el número de asientos que desea reservar"))
  if cant_asientos == 1:
    print("Los asientos disponibles son: ", end='')
    for i in desocupados:
      print(i,end=' ')
    reserva = input("Ingrese el asiento que desea reservar")
    if int(reserva[1])==1:
      costo = 125000
    elif int(reserva[1])==2:
      costo = 90000
    elif int(reserva[1])==3:
      costo = 100000
    print(f"El costo de la reserva es {costo}, ?Desea continuar? S/N")
    confirmacion = input()
    if confirmacion == "S":
      for i in range(0,filas.size):
        if reserva[0] == filas[i]:
          avion[i][int(reserva[1])-1] = 1
          print(f"Asiento {reserva} reservado")

  elif cant_asientos == 2:
    print("Los asientos disponibles son: ", end='')
    for i in desocupados_2:
      print(i,end=' ')
    reserva = input("Ingrese los asientos que desea reservar")
    print(f"El costo de la reserva es 190.000, ?Desea continuar? S/N")
    confirmacion = input()
    if confirmacion == "S":
      for i in range(0,filas.size):
        if reserva[0] == filas[i]:
          avion[i][1] = 1
          avion[i][2] = 1
          print(f"Asientos {reserva} reservado")


  elif cant_asientos == 3:
    print("Los asientos disponibles son: ", end='')
    for i in desocupados_3:
      print(i,end=' ')
    reserva = input("Ingrese la fila que desea reservar")
    print(f"El costo de la reserva es 315.000, ?Desea continuar? S/N")
    confirmacion = input()
    if confirmacion == "S":
      for i in range(0,filas.size):
        if reserva == filas[i]:
          avion[i][0] = 1
          avion[i][1] = 1
          avion[i][2] = 1
          print(f"Fila {reserva} reservada")

  print(avion)
  mantener_reserva = input("Desea continuar? S/N")
  if mantener_reserva == "N":
    break










