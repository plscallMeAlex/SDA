# Problem
We want to looping through the object that have a complex structure without showing the structure.
# Trade-off
- can using with a various of data structure like list, tree, array
- have additional class
# Topology
Having an iterator class separately, the client use the iterator interface to looping.
# Use-when
We need to traverse a custom data structure
Want to hide the internal data structure details
Want to standardize iteration across different types of collections.
# Example
```python
# Iterator interface
class Iterator:
    def has_next(self):
        pass

    def next(self):
        pass


# Concrete Iterator
class NameIterator(Iterator):
    def __init__(self, names):
        self._names = names
        self._index = 0

    def has_next(self):
        return self._index < len(self._names)

    def next(self):
        if self.has_next():
            name = self._names[self._index]
            self._index += 1
            return name
        raise StopIteration


# Aggregate (collection)
class NameCollection:
    def __init__(self):
        self._names = []

    def add_name(self, name):
        self._names.append(name)

    def create_iterator(self):
        return NameIterator(self._names)


# Client code
if __name__ == "__main__":
    collection = NameCollection()
    collection.add_name("Alice")
    collection.add_name("Bob")
    collection.add_name("Charlie")

    iterator = collection.create_iterator()

    while iterator.has_next():
        name = iterator.next()
        print(name)
```