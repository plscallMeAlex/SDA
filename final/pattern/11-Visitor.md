# Problem
We want to add the operation to the object without editing the class. Make it easy to add the operation
# Trade-off
Easy to add a new operation
It need to create a new class and more complex.
# Topology
Visitor class having a method for each type, object receive visitor and call the method that have the same type.
# Example
```python
class Visitor:
    def visit_element_a(self, element):
        pass
    def visit_element_b(self, element):
        pass
class ElementA:
    def accept(self, visitor):
        visitor.visit_element_a(self)
class ElementB:
    def accept(self, visitor):
        visitor.visit_element_b(self)
class ConcreteVisitor(Visitor):
    def visit_element_a(self, element):
        print("Visited A")
    def visit_element_b(self, element):
        print("Visited B")
elements = [ElementA(), ElementB()]
visitor = ConcreteVisitor()
for e in elements:
    e.accept(visitor)
```
