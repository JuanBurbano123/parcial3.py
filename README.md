# integrantes del grupo: Juan Pablo Burbano

productos = {
    1: ("Cafe", 3000, 20),
    2: ("Jugo natural", 5000, 15),
    3: ("Sandwich", 8000, 10),
    4: ("Empanada", 2500, 25),
    5: ("Hamburguesa", 12000, 8)
}

def mostrar_productos(productos):
    print("========== CATALOGO DE PRODUCTOS ==========")
    for codigo, informacion in productos.items():
        nombre = informacion[0]
        precio = informacion[1]
        existencias = informacion[2]
        print("Codigo:", codigo)
        print("Producto:", nombre)
        print("Precio: ", precio)
        print("Existencias:", existencias)
        print("--------------------------------")

def registrar_producto(productos, pedido, codigo, cantidad):
    if codigo not in productos:
        print("Producto no encontrado")
    elif cantidad <= 0:
        print("Cantidad no valida")
    else:
        nombre = productos[codigo][0]
        precio = productos[codigo][1]
        existencias = productos[codigo][2]
        if cantidad > existencias:
            print("No hay suficientes unidades disponibles")
        else:
            subtotal = precio * cantidad
            pedido.append((codigo, nombre, cantidad, subtotal))
            productos[codigo] = (nombre, precio, existencias - cantidad)
            print("Producto agregado correctamente")

def mostrar_resumen(pedido):

    print("========== RESUMEN DEL PEDIDO ==========")

    print("Producto       Cantidad       Subtotal")

    for codigo, nombre, cantidad, subtotal in pedido:

        print(nombre, "      ", cantidad, "      $", subtotal)

def calcular_total(pedido):
    total = 0
    for producto in pedido:
        total = total + producto[3]
    if total >= 50000:
        descuento = total * 0.10
    else:
        descuento = 0
    total_final = total - descuento
    return total, descuento, total_final

pedido = []

opcion = 0

while opcion != 3:
    print("========== CAFETERIA ==========")
    print("1. Mostrar productos")
    print("2. Agregar producto al pedido")
    print("3. Finalizar pedido")
    opcion = int(input("\nSeleccione una opcion: "))
    if opcion == 1:
        mostrar_productos(productos)
    elif opcion == 2:
        mostrar_productos(productos)
        codigo = int(input("\nIngrese el codigo del producto: "))
        cantidad = int(input("Ingrese la cantidad que desea: "))
        registrar_producto(productos, pedido, codigo, cantidad)
    elif opcion == 3:
        if len(pedido) == 0:
            print("No se han agregado productos al pedido")
        else:
            mostrar_resumen(pedido)
            total, descuento, total_final = calcular_total(pedido)
            print("--------------------------------")
            print("Total: ", total)
            print("Descuento: ", descuento)
            print("TOTAL A PAGAR: ", total_final)
        print("\nGracias por utilizar la cafeteria")

    else:
        print("Opcion no valida")
