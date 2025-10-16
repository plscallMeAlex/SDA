# Abstract Factory & Memento
## Abstract Factory
We need to refer to the factory use method first
### Factory Method
It found out that if we want a class to create objects, but we don't want the hardcode then concrete class it creates.
It remove dependency on concrete classes. It **allow subclasses to decide which concrete class to instantiate**. So it **remove tight coupling** between **creator code** and **concrete product classes**.
```lua
          Creator
          +----------------+
          | +factoryMethod()|
          +----------------+
                  ^
                  |
        ---------------------
        |                   |
   ConcreteCreator1      ConcreteCreator2
          |                   |
          v                   v
      Product               Product
      +-------+             +-------+
      | do()  |             | do()  |
      +-------+             +-------+
          ^
          |
     ConcreteProduct1 / ConcreteProduct2
```
### Abstract Factory Method
It found that if we want to create families of related objects without specifying their concrete classes.
Handle for the **multiple products** that should be **compatible with each other**.
It remove the need to **hard-code a family of objects** and **ensure it work together**.
```lua
           AbstractFactory
          +----------------------+
          | +createProductA()    |
          | +createProductB()    |
          +----------------------+
                  ^
                  |
        -----------------------
        |                     |
   ConcreteFactory1       ConcreteFactory2
        |                     |
        v                     v
 ProductA1 + ProductB1    ProductA2 + ProductB2
   +-----+ +-----+         +-----+ +-----+
   | doA | | doB |         | doA | | doB |
   +-----+ +-----+         +-----+ +-----+
```
### Summary Both
- **Factory**: One creator -> one product (class depend on one class).
- **Abstract Factory:** One factory -> multiple related products (family).

## Memento
(Behavioral) Is the method that we want to undo or revert back to the previous state of an object without reveal the detail implementation.
### Roles
- **Originator** - The object that we want to save the state and create memento to make a restore.
- **Memento** - A snapshot of the Originator's. Immutable.
- **Caretaker** - Use to manage mementos. Stores them and can restore the originator's state.
![[Pasted image 20250821014446.png]]
```python
# Memento: stores the state
class Memento:
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state

# Originator: creates and restores mementos
class TextEditor:
    def __init__(self):
        self._text = ""

    def write(self, text):
        self._text = text

    def read(self):
        return self._text

    def save(self):
        return Memento(self._text)

    def restore(self, memento):
        self._text = memento.get_state()

# Caretaker: manages mementos
class UndoManager:
    def __init__(self):
        self._history = []

    def add_memento(self, memento):
        self._history.append(memento)

    def get_memento(self, index):
        return self._history[index]

# --- Example Usage ---
editor = TextEditor()
undo_manager = UndoManager()

editor.write("Hello")
undo_manager.add_memento(editor.save())  # Save state

editor.write("Hello, World")
undo_manager.add_memento(editor.save())  # Save state again

editor.write("Hello, World!!!")

print("Current Text:", editor.read())

# Undo last change
editor.restore(undo_manager.get_memento(1))
print("After Undo 1:", editor.read())

# Undo to first change
editor.restore(undo_manager.get_memento(0))
print("After Undo 2:", editor.read())


%% Current Text: Hello, World!!!
After Undo 1: Hello, World
After Undo 2: Hello
 %%
```

[[Slide_5_2|Back]], [[Slide_6_1|Next]]
