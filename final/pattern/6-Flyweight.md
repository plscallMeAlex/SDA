# Problem
We need to safe the memory when you **have a multiple of object** that have the same data like the alphabetic in editor. We use this method to safe the memory. It **sharing common data** between similar objects, instead of keeping duplicate copies.
# Trade-off 
Reduce the memory use but it make the code more complex and need to handle state good.
# Topology
It use a Flyweight factory to create and return the object that have the same data. 
# Use-when
when having a huge number of small object that share the similar data.
when memory usage is concern.
# Example
```python
class CharFlyweight:
    _pool = {}
    def __new__(cls, char):
        if char not in cls._pool:
            cls._pool[char] = super().__new__(cls)
            cls._pool[char].char = char
        return cls._pool[char]
        
a1 = CharFlyweight('a')
a2 = CharFlyweight('a')
b1 = CharFlyweight('b')

print(a1 is a2)  # True — same instance reused
print(a1 is b1)  # False — different char

```