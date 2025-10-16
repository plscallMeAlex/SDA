# Problem
We want to construct the object but it contain a lot of parameter
```python
class Pizza:
	def __init__(self, cheese, pepperoni, pesly, ...):
		pass
```
So want to create a complex object make it easy to construct.
# Trade-off
- Make the code easy to read
- Addition class and increase the complexity
# Use-when
During you construct the SQL query, or create a custom car.
# Example
```python
class PizzaBuilder:
    def __init__(self):
        self.toppings = []
    def add_cheese(self):
        self.toppings.append('cheese')
        return self
    def add_pepperoni(self):
        self.toppings.append('pepperoni')
        return self
    def build(self):
        return Pizza(self.toppings)
class Pizza:
    def __init__(self, toppings):
        self.toppings = toppings
pizza = PizzaBuilder().add_cheese().add_pepperoni().build()
```
From the above is like create another class with the parameter as a method that append to list then you construct (return instance)