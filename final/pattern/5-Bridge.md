# Problem
We separate the abstraction and implementation make freely like UI theme with a platform
![](images/Pasted%20image%2020251013190508.png)
# Trade-off
- Increase elasticity but make the code more complex.
# Topology
Abstraction class have a reference to the implementation like from the above example 
Remote have an interface for each device whether you change the device then it do the as the same behavior.
# Use-when
Want to separate the abstraction from implementation. so we can change one without affecting the other.
# Example 
```python
class DrawingAPI:
    def draw_circle(self, x, y, radius):
        pass
class DrawingAPI1(DrawingAPI):
    def draw_circle(self, x, y, radius):
        print(f"API1.circle at {x},{y} radius {radius}")
class Circle:
    def __init__(self, x, y, radius, drawing_api):
        self.x = x
        self.y = y
        self.radius = radius
        self.drawing_api = drawing_api
    def draw(self):
        self.drawing_api.draw_circle(self.x, self.y, self.radius)
```
