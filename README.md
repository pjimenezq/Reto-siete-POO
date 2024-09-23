# Reto siete POO
## Punto uno: El menú 

**Instrucciones**

Take the Menu code from Reto 3 and implement a new Class that creates and iterable with all the items in an order, it should allow looping and contain all item attributes.

**Código**
```
class MenuItem:
    def __init__(self, name, price):
        self.name = name
        self.price = price

class Beverage(MenuItem):
    def __init__(self, name, price, alcohol, temperature):
        super().__init__(name, price)
        self.alcohol = alcohol
        self.temperature = temperature
    
    def __str__(self):
        return str(self.name+": "+str(self.price)+" ("+self.alcohol+", "+self.temperature+")")

class MainCourse(MenuItem):
    def __init__(self, name, price, vegetarian, spicy):
        super().__init__(name, price)
        self.vegetarian = vegetarian
        self.spicy = spicy
    
    def __str__(self):
        return str(self.name+": "+str(self.price)+" ("+self.vegetarian+", "+self.spicy+")")


class Dessert(MenuItem):
    def __init__(self, name, price, peanuts, vegan):
        super().__init__(name, price)
        self.peanuts = peanuts
        self.vegan = vegan

    def __str__(self):
        return str(self.name+": "+str(self.price)+" ("+self.peanuts+", "+self.vegan+")")


class Order:
    #Iterable para registrar items en una orden e imprimir el valor de la cuenta
    def __init__(self, order_list: list=[]):
        self.order_list = order_list

    def add_items(self, new_items_list: list= []):
        #Agregar un nuevo item a la orden
        x = 0
        while x<len(new_items_list):
            self.order_list.append(new_items_list[x])#Los nuevos items son añadidos a la lista order_list
            x+=1
    def bill_amount(self):
        x = 0
        sum = 0 #Esta variable es para sumar todos los precios de los items que están en order_list
        while x<len(self.order_list):
            sum+=self.order_list[x].price
            x+=1
        if self.order_list.count(beer)>=3:#Hay un descuento para las cervezas: paga 2 y lleva 3
            beer_count = self.order_list.count(beer)
            beer_discount = int(beer_count/3)
            sum-=(beer.price*beer_discount)

        print("The total price is $" +str(sum)) 

    def __iter__(self):
        return RegistroMenuItemsIterador(self.order_list)
    
class RegistroMenuItemsIterador:
    #Implementa un iterador para recorrer los items registrados en la orden
    def __init__(self, order_list):
        self.order_list=order_list
        self.index = 0

    def __iter__(self):
        return self
    
    def __next__(self):
        if self.index<len(self.order_list):
            x=self.index
            self.index+=1
            return self.order_list[x]
        else:
            raise StopIteration

beer = Beverage("Beer", 10.000, "Alcoholic", "Cold" )
water = Beverage("Bottle of water", 6.500, "Non-alcoholic", "Room temperature" )
soda = Beverage("Coca-Cola", 6.000,"Non-alcoholic", "Cold" )
coffee = Beverage("Cappuccino", 6.100, "Non-alcoholic", "Hot" )
salad = MainCourse("Caesar salad", 23.000, "Non-vegetarian", "Non-spicy" )
lasagna = MainCourse("Lasagna", 25.000, "Vegetarian", "Non-spicy")
tacos = MainCourse("Chicken Tacos", 20.000, "Non-vegetarian", "Spicy")
waffle = Dessert("Nutella waffles", 15.000, "Contains peanuts", "Non-vegan" )
iceCream = Dessert("Lemon ice cream", 5.000, "Without peanuts", "Vegan" )
tiramisu = Dessert("Tiramisu", 12.000, "Without peanuts", "Non-vegan")

order = Order([waffle, salad, beer])
order.add_items([beer, beer, lasagna, tacos, coffee ])


for item in order:
    print(item)

order.bill_amount()

```
