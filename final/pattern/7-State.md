# Problem
We want to change the behavior of the object via internal state. For elasticity of changing the state of behavior.
# Trade-off
- Increase elasticity but it also increase the number of class
# Topology
State interface context class can change the state
# Use-when
Vending machine that it will change the state.
# Example
```python
class State:
    def handle(self):
        pass
class OnState(State):
    def handle(self):
        print("Light is ON")
class OffState(State):
    def handle(self):
        print("Light is OFF")

class Light: # Context class
    def __init__(self):
        self.state = OffState()
    def set_state(self, state):
        self.state = state
    def press(self):
        self.state.handle()
```
