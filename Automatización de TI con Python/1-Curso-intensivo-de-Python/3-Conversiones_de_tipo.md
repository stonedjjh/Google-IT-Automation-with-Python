# Conversiones de Tipo

En ocasiones necesitaremos concatenar variables de distintos tipos para esto Python nos da 2 opciones las conversiones explícitas y las implícitas.

## Conversiones explícitas

A veces, es posible que necesites convertir un tipo de dato a otro de forma explícita. Esto se llama conversión explícita o casting. Por ejemplo, si quieres concatenar una cadena con un número, necesitas convertir el número a una cadena primero:

```python
c ="Hola "
d = 37

print (c + d)
# TypeError: can only concatenate str (not "int") to str
```

para solucionarlo debemos usar la funcion str

```python
c ="Hola "
d = 37
print (c + str(d))
# Hola 37
```

## Conversiones Implícitas

En algunos casos, Python puede convertir automáticamente un tipo de dato a otro sin que el programador tenga que hacer nada. Esto se llama conversión implícita. Por ejemplo:

```python
print(7+8.5)
# 15.5
```
