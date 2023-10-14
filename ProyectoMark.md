# Pythom 
import csv

class Producto:
    def __init__(self, nombre, codigo, precio, proveedor, existencia, estado, descuento):
        self.nombre = nombre
        self.codigo = codigo
        self.precio = precio
        self.proveedor = proveedor
        self.existencia = existencia
        self.estado = estado
        self.descuento = descuento

# Función para agregar un producto al archivo
def agregar_producto(productos, archivo):
    print("Agregar Producto:")
    codigo = input("Código: ")
    
    for producto in productos:
        if producto.codigo == codigo:
            print("El código ya existe. No se pudo agregar el producto.")
            return
    
    nombre = input("Nombre: ")
    precio = float(input("Precio: "))
    proveedor = input("Proveedor: ")
    existencia = int(input("Existencia: "))
    estado = input("Estado (A/R): ").upper()
    descuento = float(input("Descuento: "))
    
    nuevo_producto = Producto(nombre, codigo, precio, proveedor, existencia, estado, descuento)
    productos.append(nuevo_producto)
    
    with open(archivo, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([nombre, codigo, precio, proveedor, existencia, estado, descuento])
    
    print("Producto agregado con éxito.")

# Función para buscar un producto por código o nombre
def buscar_producto(productos, termino):
    print("Buscar Producto:")
    for producto in productos:
        if termino in (producto.codigo, producto.nombre):
            print(f"Nombre: {producto.nombre}")
            print(f"Código: {producto.codigo}")
            print(f"Precio: {producto.precio}")
            print(f"Proveedor: {producto.proveedor}")
            print(f"Existencia: {producto.existencia}")
            print(f"Estado: {producto.estado}")
            print(f"Descuento: {producto.descuento}")
            print()

# Función para modificar los datos de un producto
def modificar_producto(productos, codigo):
    print("Modificar Producto:")
    for producto in productos:
        if producto.codigo == codigo:
            print("Código no puede modificarse.")
            nuevo_nombre = input(f"Nuevo nombre ({producto.nombre}): ") or producto.nombre
            nuevo_precio = float(input(f"Nuevo precio ({producto.precio}): ") or producto.precio)
            nuevo_proveedor = input(f"Nuevo proveedor ({producto.proveedor}): ") or producto.proveedor
            nuevo_existencia = int(input(f"Nueva existencia ({producto.existencia}): ") or producto.existencia)
            nuevo_estado = input(f"Nuevo estado (A/R) ({producto.estado}): ").upper() or producto.estado
            nuevo_descuento = float(input(f"Nuevo descuento ({producto.descuento}): ") or producto.descuento)
            
            producto.nombre = nuevo_nombre
            producto.precio = nuevo_precio
            producto.proveedor = nuevo_proveedor
            producto.existencia = nuevo_existencia
            producto.estado = nuevo_estado
            producto.descuento = nuevo_descuento
            
            print("Datos modificados con éxito.")
            return
    print("Producto no encontrado.")

# Función para cargar productos desde un archivo
def cargar_productos(archivo):
    productos = []
    try:
        with open(archivo, newline='') as file:
            reader = csv.reader(file)
            for row in reader:
                nombre, codigo, precio, proveedor, existencia, estado, descuento = row
                producto = Producto(nombre, codigo, float(precio), proveedor, int(existencia), estado, float(descuento))
                productos.append(producto)
    except FileNotFoundError:
        pass
    return productos

def main():
    archivo = "productos.csv"
    productos = cargar_productos(archivo)
    
    while True:
        print("Menú:")
        print("1. Agregar producto")
        print("2. Buscar producto")
        print("3. Modificar datos de un producto")
        print("4. Salir")
        
        opcion = input("Opción: ")
        
        if opcion == "1":
            agregar_producto(productos, archivo)
        elif opcion == "2":
            termino = input("Buscar por código o nombre: ")
            buscar_producto(productos, termino)
        elif opcion == "3":
            codigo = input("Código del producto a modificar: ")
            modificar_producto(productos, codigo)
        elif opcion == "4":
            print("Saliendo...")
            break
        else:
            print("Opción no válida. Inténtelo de nuevo.")

if __name__ == "__main__":
    main()

# C++proyecto

#include <iostream>
#include <fstream>
#include <string>
using namespace std;
// Programa para gestión de productos

// Estructura para representar un producto
struct Producto {
  string nombre;
  string codigo;
  float precio;
  string proveedor;
  int existencia;
  char estado;
  float descuento;
};
// Solicita los datos al usuario y agrega el producto
void agregarProducto(Producto productos[], int &contador) {
  Producto nuevoProducto;
  cout << "Ingrese nombre del producto: ";
  cin.ignore();
  getline(cin, nuevoProducto.nombre);
  cout << "Ingrese código del producto: ";
  cin >> nuevoProducto.codigo;
  cout << "Ingrese precio del producto: ";
  cin >> nuevoProducto.precio;
  cout << "Ingrese proveedor del producto: ";
  cin.ignore();
  getline(cin, nuevoProducto.proveedor);
  cout << "Ingrese existencia del producto: ";
  cin >> nuevoProducto.existencia;
  cout << "Ingrese estado del producto (A/R): ";
  cin >> nuevoProducto.estado;
  cout << "Ingrese descuento del producto: ";
  cin >> nuevoProducto.descuento;

  productos[contador] = nuevoProducto;
  contador++;

  cout << "Producto agregado con éxito." << endl;
}
//Función para buscar un producto por código o nombre e Imprime los datos del producto si lo encuentra
void buscarProducto(Producto productos[], int contador, string codigo_o_nombre) {
  for (int i = 0; i < contador; i++) {
    if (productos[i].codigo == codigo_o_nombre || productos[i].nombre.find(codigo_o_nombre) != string::npos) {
      cout << "Nombre: " << productos[i].nombre << endl;
      cout << "Código: " << productos[i].codigo << endl;
      cout << "Precio: " << productos[i].precio << endl;
      cout << "Proveedor: " << productos[i].proveedor << endl;
      cout << "Existencia: " << productos[i].existencia << endl;
      cout << "Estado: " << productos[i].estado << endl;
      cout << "Descuento: " << productos[i].descuento << endl;
    }
  }
}

// Función para modificar un producto dado su código y Permite cambiar todos los campos menos el código

void modificarProducto(Producto productos[], int contador, string codigo) {
  for (int i = 0; i < contador; i++) {
    if (productos[i].codigo == codigo) {
      cout << "Ingrese nuevo nombre del producto: ";
      cin.ignore();
      getline(cin, productos[i].nombre);
      cout << "Ingrese nuevo precio del producto: ";
      cin >> productos[i].precio;
      cout << "Ingrese nuevo proveedor del producto: ";
      cin.ignore();
      getline(cin, productos[i].proveedor);
      cout << "Ingrese nueva existencia del producto: ";
      cin >> productos[i].existencia;
      cout << "Ingrese nuevo estado del producto (A/R): ";
      cin >> productos[i].estado;
      cout << "Ingrese nuevo descuento del producto: ";
      cin >> productos[i].descuento;

      cout << "Producto modificado con éxito." << endl;
      return;
    }
  }
  cout << "Producto no encontrado." << endl;
}

// Paara guardar los productos a un archivo y que no se piedan
void guardarDatos(Producto productos[], int contador) {
  ofstream archivo("datos.txt");
  for (int i = 0; i < contador; i++) {
    archivo << productos[i].nombre << "|"
            << productos[i].codigo << "|"
            << productos[i].precio << "|"
            << productos[i].proveedor << "|"
            << productos[i].existencia << "|"
            << productos[i].estado << "|"
            << productos[i].descuento << endl;
  }
  archivo.close();
}

void leerDatos(Producto productos[], int &contador) {
  ifstream archivo("datos.txt");
  string linea;
  while (getline(archivo, linea)) {
    Producto p;
    // Extraer datos de la línea y asignar a p
    
    productos[contador++] = p;
  }
  archivo.close();
}

int main() {

  string codigo; // declarar aqui para que esté en scope

  Producto productos[100];
  int contador = 0;
  
//Lee los productos de un archivo y retorna el contador

  leerDatos(productos, contador);

  int opcion;
  do {
    cout << "Menú:" << endl;
    cout << "1. Agregar Producto" << endl;
    cout << "2. Buscar Producto" << endl;
    cout << "3. Modificar Producto" << endl;
    cout << "0. Salir" << endl;
    cout << "Seleccione una opción: ";
    cin >> opcion;

    switch (opcion) {
      case 1:
        agregarProducto(productos, contador);
        break;

      case 2:
        // código para buscar
        
        break;

      case 3: 
        cout << "Ingrese el código del producto a modificar: ";
        cin >> codigo;
        modificarProducto(productos, contador, codigo);
        break;
    }

  } while (opcion != 0);

  guardarDatos(productos, contador);

  return 0;
}