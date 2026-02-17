# Programación Orientada a Objetos

Es un paradigma de la programación en que representamos objetos en propiedades y métodos.

## Clase

Una clase es un plano o plantilla para crear objetos. Define un conjunto de atributos y métodos que los objetos creados a partir de la clase pueden tener.

### Clases en Python

Una clase se define con la palabra reservada `class` el nombre de la clase que por conversión se usa pascal case seguida de :

```Python
class <MiClase>:
    #atributos
    atributo1
    atributo2
    #métodos
    def metodo1(self):
        #código del método
```

Un ejemplo menos abstracto seria:

```Python
class Triangle:
    def __init__(self, base, height):
        self.base = base
        self.height = height
    def area(self):
        return 0.5 * self.base * self.height
    def __add__(self, other):
        return self.area() + other.area()
```

En este ejemplo se define una clase Triangulo con 2 atributos base y altura 3 metodos el constructor, el metodo area que calcula el area y un "dunder methods"(explicado mas abajo) que suma el area del mismo objeto con el de otro objeto

## Objeto

Un objeto es una instancia de una clase. Es una entidad que tiene atributos y métodos definidos por la clase a la que pertenece.

```Python
class Triangle:
    def __init__(self, base, height):
        self.base = base
        self.height = height
    def area(self):
        return 0.5 * self.base * self.height
    def __add__(self, other):
        return self.area() + other.area()
#triangle1 y 2 son objetos de la clase Triangle
triangle1 = Triangle(10, 5)
triangle2 = Triangle(6, 8)
print("The area of triangle 1 is", triangle1.area())
# The area of triangle 1 is 25.0
print("The area of triangle 2 is", triangle2.area())
# The area of triangle 2 is 24.0
print("The area of both triangles is", triangle1 + triangle2)
# The area of both triangles is 49.0
```

## Atributo

Un atributo es una característica o propiedad de un objeto.

## Método

Un método es una función que está asociada a un objeto y que puede acceder a sus atributos y realizar acciones específicas.

Los métodos en Python se dividen en varias categorías:

- **Métodos de instancia**: Los métodosde instancia son los más comunes en Python. Los métodos de instancia se definen dentro de una clase creando funciones dentro de la definición de la clase. Cuando instancias de una clase, esas instancias individuales pueden tener sus métodos llamados para que el programa pueda controlar y modificar esas instancias directamente. Los métodos de instancia pueden tomar un parámetro llamado `self`, que representa la instancia sobre la que se está ejecutando el método, que te permite acceder a atributos de la instancia usando notación por puntos, como `self.name`, que accederá al atributo name de esa instancia específica del objeto de clase. Cuando tienes variables que contienen diferentes valores para diferentes instancias, se llaman variables de instancia.

- **Métodos de clase**: Los métodos de clase, por otro lado, se llaman para la clase misma en lugar de para una instancia. Están marcados con un decorador `@classmethod` y toman un parámetro `cls` que apunta a la clase -y no a una instancia específica- cuando se llama al método. Un caso de uso común para los métodos de clase es crear y modificar estructuras de datos que contengan registros para todas las instancias de una clase. Normalmente, los programadores hacen una lista dentro de la definición de la clase, y métodos para añadir instancias de la clase a esa lista con el fin de realizar un seguimiento de esa clase.

- **Métodos estáticos**: Por último, los métodos estáticos, marcados con un decorador `@staticmethod`, no toman un parámetro self o cls. Los métodos estáticos se comportan como funciones simples, excepto que puedes llamarlos directamente desde la clase. Es importante tener en cuenta que no es necesario instanciar la clase, los métodos sólo residen en ella. Esto se debe a que las definiciones de clase son en sí mismas un objeto (es decir, una instancia de la clase base abstracta), lo que reduce la sobrecarga y permite encapsular las funciones de forma sencilla. Los programadores utilizan métodos estáticos cuando el método no necesita acceder a ninguna instancia o dato específico de la clase.

### Elección del tipo de método

El tipo de método que elija utilizar (de instancia, de clase o estático) dependerá de los datos a los que deba acceder el método. Piensa en estos métodos como diferentes herramientas de tu caja de herramientas, cada una con un caso de uso diferente dependiendo de los datos con los que necesites trabajar.

- Los métodos de instancia son para datos de objetos individuales

- Métodos de clase para datos compartidos, Métodos estáticos para tareas relacionadas que no necesitan acceder o modificar ningún objeto o datos de clase

## Pilares de la POO

- **Encapsulación**: Proceso de ocultar los detalles internos de un objeto y exponer solo lo necesario a través de una interfaz pública. En Python, se suele indicar que un atributo es "privado" anteponiendo un guion bajo `_variable` o doble guion bajo `__variable`.

- **Abstracción**: Consiste en reducir un objeto a sus características esenciales, ignorando los detalles irrelevantes. Permite enfocarse en _qué hace_ un objeto en lugar de _cómo lo hace_ (ej. usar un método `.conducir()` sin saber cómo funciona el motor por dentro).

- **Herencia**: Permite que una clase (hija) herede atributos y métodos de otra clase (padre). Esto facilita la reutilización de código y la creación de jerarquías lógicas.

```python
class Animal:
    def saludar(self):
        print("Hola")

class Perro(Animal): # Herencia
    def saludar(self):
        print("Guau!")
```

- **Polimorfismo:** Es la capacidad de diferentes clases de responder al mismo mensaje (método) de maneras distintas. En el ejemplo anterior, tanto un Gato como un Perro pueden tener un método .saludar(), pero cada uno lo hace a su manera.

## Constructores y otros métodos especiales

Los constructores son métodos especiales que se ejecutan automáticamente cuando se crea una nueva instancia de una clase. En Python, el constructor se define con el método `__init__()`. Este método se utiliza para inicializar los atributos de la instancia con valores específicos.

```python
class Apple:
    def __init__(self):
        self.color = "red"
        self.flavor = "sweet"

honeycrisp = Apple()
print(honeycrisp.color)

# prints "red"
```

> [!IMPORTANT]
> Un constructor (como `__init__`) es un método especial de clase que configura el objeto en Python. Cuando se hace un argumento a una clase, el primer constructor debe ser siempre `self`.

Además del constructor `__init__()`, Python tiene otros métodos especiales que comienzan y terminan con dobles guiones bajos (conocidos como "dunder methods"). Estos métodos permiten definir comportamientos personalizados para operaciones comunes, como la representación de objetos, la comparación, la suma, etc.

Por ejemplo, el método especial `__str__` controla cómo tu objeto es convertido a una representación de cadena para la salida. Cuando escribes algo en `print()`, Python llama al método `__str__()` del objeto y muestra lo que ese método devuelve. En la mayoría de los casos, la salida por defecto es sólo el nombre de la clase y una posición de memoria:

```Python
class Apple:
    def __init__(self):
        self.color = "red"
        self.flavor = "sweet"
    def __str__(self):
        return "an apple which is {} and {}".format(self.color, self.flavor)

honeycrisp = Apple("red", "sweet")
print(honeycrisp)
# prints "an apple which is red and sweet"
```

Estos son algunos de los otros métodos especiales que puedes sobreescribir en tus propias clases:

**`__len__`** devuelve la longitud del objeto o colección.

**`__contains__`** comprueba si el objeto contiene un elemento.

**`__eq__`** comprueba si dos objetos son iguales.
