# Problem
We want a object and group of object using the same interface like tree structure that go from the log to the leaf it because make it ease of using the tree structure.
# Trade-off
- Work well with tree
- It will complicated if in the deeply tree.
# Topology 
- Component (interface), Leaf, Composite (have a child which can be leaf or composite)
# Use-when
Dealing with a file structure or menu in Microsoft application.
# Example
```python
class Component:
    def operation(self):
        pass
class Leaf(Component):
    def operation(self):
        return "Leaf"
class Composite(Component):
    def __init__(self):
        self.children = []
    def add(self, component):
        self.children.append(component)
    def operation(self):
        return "+".join(child.operation() for child in self.children)

```
We use via the component and inside the composite have the children can be leaf or composit .