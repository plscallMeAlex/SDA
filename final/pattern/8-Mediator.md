# Problem
Have a lot of coupling between object so we use the middleware like mediator to handle the request to reduce the coupling between object. It **encapsulates how a set of objects interact**, so that they don’t refer to each other directly
# Trade-off
- Reduce coupling
- Mediator will complex if there a lot of logic
# Topology
Mediator class is the middleman that receive the request then send the request to the colleague class to handle the request.
# Use-when
- Having a object that interact in complex ways
- want to reduce the direct dependencies between classes.
- want to centralize communication logic in one place.
```python
# Mediator interface
class ChatMediator:
    def send_message(self, msg, user):
        pass


# Concrete Mediator
class ChatRoom(ChatMediator):
    def __init__(self):
        self.users = []

    def add_user(self, user):
        self.users.append(user)

    def send_message(self, msg, sender):
        for user in self.users:
            if user != sender:
                user.receive(msg)


# Colleague class
class User:
    def __init__(self, name, mediator):
        self.name = name
        self.mediator = mediator
        mediator.add_user(self)

    def send(self, msg):
        print(f"{self.name} sends: {msg}")
        self.mediator.send_message(msg, self)

    def receive(self, msg):
        print(f"{self.name} receives: {msg}")


# Client code
if __name__ == "__main__":
    chatroom = ChatRoom()

    alice = User("Alice", chatroom)
    bob = User("Bob", chatroom)
    charlie = User("Charlie", chatroom)

    alice.send("Hello everyone!")
    bob.send("Hey Alice!")
    
Alice sends: Hello everyone!
Bob receives: Hello everyone!
Charlie receives: Hello everyone!
Bob sends: Hey Alice!
Alice receives: Hey Alice!
Charlie receives: Hey Alice!
```
