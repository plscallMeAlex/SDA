# Problem
We want to handle request by passing through each of the provided handler that response for it. To increase the elasticity of the request handling. 
# Trade-off
- Increase elasticity but it hard to debugging if chain is too long.
# Topology
The handler that connected like chain. If the request didn't handle by any handler then it error.
# Use-when
You have a series of possible handlers for a request
want to avoid tight coupling between sender and receiver.
You want to **add/remove/extend handlers easily**
You want **flexible, ordered processing**
# Example
```python
# Abstract Handler
class MailHandler:
    def __init__(self, next_handler=None):
        self.next_handler = next_handler

    def handle(self, mail):
        if self.next_handler:
            self.next_handler.handle(mail)


# Concrete Handlers
class SpamHandler(MailHandler):
    def handle(self, mail):
        if "spam" in mail.lower():
            print("SpamHandler: Marked as spam.")
        else:
            super().handle(mail)


class FanMailHandler(MailHandler):
    def handle(self, mail):
        if "fan" in mail.lower():
            print("FanMailHandler: Thanking the fan.")
        else:
            super().handle(mail)


class ComplaintHandler(MailHandler):
    def handle(self, mail):
        if "complaint" in mail.lower():
            print("ComplaintHandler: Forwarding to support team.")
        else:
            super().handle(mail)


class GeneralDeliveryHandler(MailHandler):
    def handle(self, mail):
        print("GeneralDeliveryHandler: Sending to general inbox.")


# Client code
if __name__ == "__main__":
    # Build the chain
    chain = SpamHandler(
        FanMailHandler(
            ComplaintHandler(
                GeneralDeliveryHandler()
            )
        )
    )

    # Test different mails
    mails = [
        "This is a spam message",
        "I am your biggest fan!",
        "I have a complaint about your service",
        "Hello, just checking in"
    ]

    for m in mails:
        print(f"\nMail: {m}")
        chain.handle(m)
```