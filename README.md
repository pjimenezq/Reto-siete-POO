# Reto siete POO
## Punto uno: El menú 

**Instrucciones**

Take the Menu code from Reto 3 and implement a new Class that creates and iterable with all the items in an order, it should allow looping and contain all item attributes.

**Código**
```
class Order:

    def __init__(self):
        self.order=[]
    
    def agregar_menu_item(self, name, price, atributo_uno, atributo_dos):
        self.order.append((name, price, atributo_uno, atributo_dos))

    def __iter__(self):
        return RegistroMenuItemsIterador(self.order)
    
class RegistroMenuItemsIterador:
    def __init__(self, menu_items):
        self.order=menu_items
        self.indice = 0
    
    def __iter__(self):
        return self
    
    def __next__(self):
        if self.indice < len(self.order):
            item=self.order[self.indice]
            self.indice+=1
            return item
        else:
            raise StopIteration

orden = Order()
orden.agregar_menu_item("Beer", 10.000, "Alcoholic", "Cold" )
orden.agregar_menu_item("Tiramisu", 12.000, "Without peanuts", "Non-vegan")
orden.agregar_menu_item("Lemon ice cream", 5.000, "Without peanuts", "Vegan" )

for menuItem in orden:
    name, price, attribute_one, attribute_two = menuItem
    print(f"{name}: {price} {attribute_one, attribute_two}")

```
