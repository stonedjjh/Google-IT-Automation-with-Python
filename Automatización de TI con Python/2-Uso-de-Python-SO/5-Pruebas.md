# Pruebas

En esta sección se presentan algunas pruebas para validar el funcionamiento de los scripts desarrollados en este curso. Estas pruebas incluyen casos de uso comunes y escenarios de error para asegurar que los scripts se comporten de manera esperada.

## Pruebas Manuales

Las pruebas manuales implican ejecutar los scripts y verificar los resultados de forma manual. Esto puede incluir la ejecución de comandos en la terminal, la revisión de archivos de salida o la observación del comportamiento del sistema.

## Pruebas Automáticas

Las pruebas automáticas son aquellas que se ejecutan de manera programada y verifican los resultados de forma automática. Estas pruebas pueden ser unitarias, de integración o funcionales, dependiendo del alcance y el objetivo de la prueba.

## Pruebas Unitarias

Las pruebas unitarias son una parte esencial del desarrollo de software, ya que permiten verificar que cada componente individual de un programa funcione correctamente. En Python, se pueden utilizar bibliotecas como `unittest` o `pytest` para escribir y ejecutar pruebas unitarias.

> [!IMPORTANT]
> Una característica importante de una prueba unitaria es el aislamiento. La prueba unitaria solo debe probar la unidad de código a la que apuntan, la función o el método que se está probando.
> [!NOTE]
> Las pruebas unitarias deben ser rápidas, repetibles y fáciles de escribir. Además, es importante que las pruebas sean independientes entre sí para evitar que el resultado de una prueba afecte a otra.
> Nuestras pruebas nunca deben modificar el entorno de producción

### `unittest`

Proporciona a los desarrolladores un conjunto de herramientas para construir y ejecutar pruebas. Estas pruebas pueden ejecutarse en componentes individuales o aislando unidades de código para garantizar su corrección. Al ejecutar unittests, los desarrolladores pueden identificar y corregir cualquier error que aparezca, creando un código más fiable.

**Conceptos:**

- **Test fixture:** Se refiere a la preparación para realizar una o más pruebas. Además, los fixture de prueba también incluyen cualquier acción involucrada en la limpieza de la prueba. Esto podría implicar la creación de bases de datos temporales o proxy, directorios o el inicio de un proceso de servidor.

- **Caso de prueba:** Es la unidad individual de prueba que busca una respuesta específica a un conjunto de entradas. Si es necesario, TestCase es una clase base proporcionada por unittest y se puede utilizar para crear nuevos casos de prueba.

- **Conjunto de pruebas:** Es una colección de casos de prueba, suites de prueba o una combinación de ambos. Se utiliza para compilar pruebas que deben ejecutarse juntas.

- **Ejecutor de pruebas:** Ejecuta la prueba y proporciona a los desarrolladores los datos del resultado. El ejecutor de pruebas puede utilizar distintas interfaces, como la gráfica o la textual, para proporcionar al desarrollador los resultados de la prueba. También puede proporcionar un valor especial a los desarrolladores para comunicar los resultados de la prueba.

```Python
import unittest

class TestCakeFactory(unittest.TestCase):
 def test_create_cake(self):
   cake = CakeFactory("vanilla", "small")
   self.assertEqual(cake.cake_type, "vanilla")
   self.assertEqual(cake.size, "small")
   self.assertEqual(cake.price, 8) # Vanilla cake, small size

 def test_add_topping(self):
     cake = CakeFactory("chocolate", "large")
     cake.add_topping("sprinkles")
     self.assertIn("sprinkles", cake.toppings)

 def test_check_ingredients(self):
     cake = CakeFactory("chocolate", "medium")
     cake.add_topping("cherries")
     ingredients = cake.check_ingredients()
     self.assertIn("cocoa", ingredients)
     self.assertIn("cherries", ingredients)
     self.assertNotIn("vanilla extract", ingredients)

 def test_check_price(self):
     cake = CakeFactory("vanilla", "large")
     cake.add_topping("sprinkles")
     cake.add_topping("cherries")
     price = cake.check_price()
     self.assertEqual(price, 13) # Vanilla cake, large size + 2 toppings


# Running the unittests
unittest.TextTestRunner().run(unittest.TestLoader().loadTestsFromTestCase(TestCakeFactory))
```

#### Métodos de la clase TestCase

- **assertEqual():** Su función es verificar que dos valores sean iguales. Si los valores coinciden, la prueba continúa; si son diferentes, el método lanza una excepción de tipo AssertionError, lo que marca la prueba como fallida y detiene la ejecución de ese test específico.

| Parámetro | Tipo      | Descripción                                                                          |
| --------- | --------- | ------------------------------------------------------------------------------------ |
| first     | Requerido | El primer valor o expresión a comparar (usualmente el resultado real de tu función). |
| second    | Requerido | El segundo valor o expresión (usualmente el resultado esperado que tú ya conoces).   |
| msg       | Opcional  | Un string con un mensaje personalizado que se mostrará solo si la prueba falla.      |

```PYTHON
import unittest

def sumar(a, b):
    return a + b

class TestSuma(unittest.TestCase):
    def test_sumar_positivos(self):
        # first=sumar(2, 2), second=4
        self.assertEqual(sumar(2, 2), 4, "La suma de 2+2 debería ser 4")

if __name__ == "__main__":
    unittest.main()
```

> [!TIP]
> Al automatizar, recuerda: el "primer" parámetro suele ser el valor dinámico (la llamada a la función) y el "segundo" el valor estático (lo que esperas).

- El método `assertEqual(a, b)` comprueba que `a == b`

- El método `assertNotEqual(a, b)` comprueba que `a != b`

- El método `assertTrue(x)` comprueba que bool(x) es `True`

- El método `assertFalse(x)` comprueba que bool(x) es `Falso`

- El método `assertIs(a, b)` comprueba que `a es b`

- El método `assertIsNot(a, b)` comprueba que `a no es b`

- El método `assertIsNone(x)` comprueba que `x es None`

- El método `assertIsNotNone(x)` comprueba que `x no es Ninguno`

- El método `assertIn(a, b)` comprueba que `a está en b`

- El método `assertNotIn(a, b)` comprueba que `a no está en b`

- El método `assertIsInstance(a, b)` comprueba que `isinstance(a, b)`

- El método `assertNotIsInstance(a, b)` comprueba que `no isinstance(a, b)`

#### Interfaz de línea de comandos

La interfaz de línea de comandos te permite interactuar con una aplicación o programa a través de la línea de comandos de tu sistema operativo, terminal o consola comenzando tu código con un comando de texto. Cuando desee ejecutar pruebas en Python, puede utilizar el módulo unittest desde la línea de comandos para ejecutar pruebas desde módulos, clases o incluso métodos de prueba individuales. Esto también le permite ejecutar varios archivos a la vez.

Para llamar a un módulo entero:

`python -m unittest test_module1 test_module2`

Para llamar a una clase de prueba:

`python -m unittest test_module.TestClass`

Para llamar a un método de prueba:

`python -m unittest test_module.TestClass.test_method`

Los módulos de prueba también se pueden llamar utilizando una Ruta de archivo, como se escribe a continuación:

`python -m unittest tests/test_something.py`

#### Convenciones en Pruebas Unitarias (`unittest`)

Para que el sistema de pruebas de Python reconozca y ejecute los casos de prueba de forma automática, se deben seguir ciertas convenciones de nomenclatura.

##### 1. El sufijo `_test.py`

Cuando se crea un archivo para probar un módulo (por ejemplo, si tu script se llama `validaciones.py`), el archivo de pruebas debe nombrarse con el sufijo **`_test`**.

- **Ejemplo**: `validaciones_test.py`
- **Razón**: Esto permite que herramientas de descubrimiento de pruebas encuentren el archivo fácilmente en el directorio del proyecto.

##### 2. El prefijo `test_` en los métodos

Dentro de la clase que hereda de `unittest.TestCase`, solo los métodos que comienzan con la palabra **`test`** serán ejecutados como pruebas por el framework.

- **Correcto**: `def test_suma_positivos(self):` -> Se ejecutará.
- **Incorrecto**: `def suma_positivos_test(self):` -> Será ignorado por el test runner.

##### Ejemplo de Estructura

```python
import unittest
from mi_modulo import funcion_a_probar

class TestMiModulo(unittest.TestCase):
    # Este método será ejecutado automáticamente
    def test_caso_exitoso(self):
        self.assertEqual(funcion_a_probar(10), "Esperado")

    # Este método NO será ejecutado como prueba (útil para funciones auxiliares)
    def ayuda_auxiliar(self):
        pass

if __name__ == "__main__":
    unittest.main()
```

> [!IMPORTANT]
> Seguir estas reglas de nombres es lo que permite usar el comando python3 -m unittest en la terminal para ejecutar todas las pruebas de un proyecto a la vez sin necesidad de especificar cada archivo.

### `pytest`

Pytest es una potente herramienta de pruebas de Python que ayuda a los programadores a escribir programas más eficaces y estables. Ayuda a simplificar el proceso de escribir, organizar y ejecutar pruebas. Se puede utilizar para escribir una variedad de pruebas, incluyendo: integración, de extremo a extremo, y las pruebas funcionales. Soporta el descubrimiento automático de pruebas y genera informes de pruebas informativos

**Conceptos:**

- **`assert()`:** Un assert es una herramienta de depuración comúnmente utilizada en Python que permite a los programadores incluir comprobaciones de sanidad en su código. Aseguran que ciertas condiciones o suposiciones se cumplen durante el tiempo de ejecución. Si la condición proporcionada a `assert()` resulta ser falsa, indica un error en el código, se lanza una excepción y se detiene la ejecución del programa. Normalmente, el código proporciona una condición assert seguida de un mensaje opcional. Un ejemplo es

- **Fixtures:** Se utilizan para separar partes de código que sólo se ejecutan para las pruebas. Son piezas reutilizables de código de configuración y desmontaje de pruebas que se comparten en varias pruebas. Los Fixtures benefician a los desarrolladores ayudándoles a mantener sus pruebas limpias y evitando la duplicación de código. Veamos un ejemplo de uso de un pytest en Python:

```Python
import pytest
# Ejemplo assert
def divide(a, b):
    assert b != 0, "Cannot divide by zero"
    return a / b

# ejemlpo fixtures
class Fruit:
    def __init__(self, name):
        self.name = name
        self.cubed = False


    def cube(self):
        self.cubed = True


class FruitSalad:
    def __init__(self, *fruit_bowl):
        self.fruit = fruit_bowl
        self._cube_fruit()


    def _cube_fruit(self):
        for fruit in self.fruit:
            fruit.cube()


# Arrange
@pytest.fixture
def fruit_bowl():
    return [Fruit("apple"), Fruit("banana")]


def test_fruit_salad(fruit_bowl):
    # Act
    fruit_salad = FruitSalad(*fruit_bowl)


    # Assert
    assert all(fruit.cubed for fruit in fruit_salad.fruit)

# En este ejemplo, test_fruit_salad  solicita fruit_bowl. Cuando pytest reconoce esto, ejecuta la función fixture fruit_bowl y toma el objeto que devuelve en test_fruit_salad como argumento fruit_bowl.
```

## Pruebas de caja blanca(white-box testing)

Las pruebas de caja blanca, también conocidas como pruebas estructurales o pruebas de código, se centran en la estructura interna del código. Estas pruebas requieren que el probador tenga conocimiento del código fuente y se enfoquen en probar cada ruta posible a través del código para asegurar que todas las partes del programa funcionen correctamente.

## Pruebas de caja negra(black-box test)

Las pruebas de caja negra se centran en la funcionalidad del programa sin tener en cuenta su estructura interna. Estas pruebas se basan en las especificaciones del programa y se enfocan en probar las entradas y salidas para asegurar que el programa funcione según lo esperado.

## Pruebas de Intregración

Las pruebas de integración se centran en verificar que diferentes módulos o componentes de un programa funcionen correctamente juntos. Estas pruebas aseguran que las interfaces entre los módulos sean correctas y que los datos se transmitan correctamente entre ellos.

## Pruebas de regresión

Una **prueba de regresión** es un tipo de prueba de software que se realiza para confirmar que un cambio reciente en el código (como una corrección de un error, una actualización de versión o la adición de una nueva función) **no haya afectado negativamente** las funciones que ya funcionaban correctamente.

## Pruebas de humo

Las pruebas de humo, también conocidas como pruebas de construcción, son un tipo de prueba rápida y superficial que se realiza para verificar si una aplicación o sistema es lo suficientemente estable como para realizar pruebas más exhaustivas. Estas pruebas se centran en verificar las funciones básicas del sistema para asegurarse de que no haya fallos críticos que impidan su uso.

## Pruebas de carga

Las pruebas de carga se centran en evaluar el rendimiento de un sistema bajo condiciones de carga específicas. Estas pruebas simulan múltiples usuarios o procesos que acceden al sistema simultáneamente para medir su capacidad de respuesta, estabilidad y escalabilidad.

## referencias

[https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/](https://landing.google.com/sre/sre-book/chapters/monitoring-distributed-systems/)

[https://landing.google.com/sre/sre-book/chapters/testing-reliability/](https://landing.google.com/sre/sre-book/chapters/testing-reliability/)

[https://testing.googleblog.com/2007/10/performance-testing.html](https://testing.googleblog.com/2007/10/performance-testing.html)

[https://www.guru99.com/smoke-testing.html](https://www.guru99.com/smoke-testing.html)

[https://www.guru99.com/exploratory-testing.html](https://www.guru99.com/exploratory-testing.html)

[https://testing.googleblog.com/2008/09/test-first-is-fun_08.html](https://testing.googleblog.com/2008/09/test-first-is-fun_08.html)
