# Problem
We want to control the object like the security concern, or logging to increase the elasticity of the access (because it cause via interface)
# Trade-off
- Increase elasticity
- Also increase complexity.
# Topology
Proxy having the interface before gaining the access to the data.
```python
Client ---> Proxy ---> RealSubject
```
# Use-when
Want to increase the elasticity of accessing the data.
# Example
```python
class RealImage:
    def display(self):
        print("Displaying image")
class ProxyImage:
    def __init__(self):
        self.real_image = None
    def display(self):
        if not self.real_image:
            self.real_image = RealImage()
        self.real_image.display()

image = ProxyImage()
image.display()
```
