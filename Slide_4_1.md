# Template and Command Patterns.
## Template Method
Template method is stay inside the behavioral patterns 
### Behavioral DP
Behavioral pattern = rules about how object talk to each other and who does what in a program
instead of focus on the structure it focused how the object work together.
### Problem We found
**Duplicated code** is difficult to change, maintain or extend.
Like - 
Class A have some method the same as Class B
![[Pasted image 20250819014338.png]]
Called duplication.
But when do an abstraction than it cause again so we use!
### Use When ?
- If want to control the main structure to follow the specific pattern.
- Prevent the duplication.
- Want main process have the same algorithm 

### **Template Method** Pattern
![[Pasted image 20250819015104.png]]
The template define an algorithm to the abstract class and some of step might go to sub-classes.
So the it like 

The prepare method in base class (skeleton class) that some step already implemented in the base class some are abstract methods (must be implemented by subclass), some are hook (provide default by base can be override) 

The subclass provide only missing detail like the **brew()** and **addCondiments()**
#### Example in plain words: **Building a House**

1. **Template Method (final `buildHouse()`)**:
    
    - Lay foundation
        
    - Build walls
        
    - Add roof
        
    - (Hook) paint house (optional)
        
    - Add furniture
        
2. **Abstract Methods**:
    
    - Build walls (wood walls? brick walls? glass walls?) → subclasses decide.
        
    - Add roof (tile? thatch? concrete?) → subclasses decide.
        
3. **Hook**:
    
    - Paint house (default: do nothing, subclass may override).

### Template Vs. Strategy Pattern
- Template encapsulate (hide) a steps of algorithm
- Strategy encapsulate the entire algorithm.
We can use both patterns at the same time.
**Template** using inheritance like the **factory method** can seen as specialization of the template method. It offer the code reuse benefit (typically not seen with the strategy pattern)
**Strategy** using composition/delegation instead and it provide the run-time flexibility cause using composition/delegation.

## Command
Command is also stay in the behavioral patterns.

### Problem that found
The program is in charge of all action events if we implementing these feature would lead to a huge if-elseif or switch blocks. So we can reduce the control flow statement by using a class as a method called.

### **Command**
The command method is like sending a command class like setting a commands to execute by use the method.
**The command consist of these component:**
- Command (interface) - abstract execute method.
- Concrete Command - Used to implement execute that call the receiver.
- Receiver - The class object or object that need to be act. 
- Invoker - Trigger the command.
- Client (Main program)- wire it all together.

Can put any generic method inside the command. 
```java
// Command Interface
interface Command {
    void execute();
}

// Receiver
class Light {
    void turnOn() {
        System.out.println("Light is ON");
    }
    void turnOff() {
        System.out.println("Light is OFF");
    }
}

// Concrete Commands
class TurnOnLightCommand implements Command {
    private Light light;
    public TurnOnLightCommand(Light light) { this.light = light; }
    public void execute() { light.turnOn(); }
}

class TurnOffLightCommand implements Command {
    private Light light;
    public TurnOffLightCommand(Light light) { this.light = light; }
    public void execute() { light.turnOff(); }
}

// Invoker
class RemoteControl {
    private Command command;
    public void setCommand(Command command) { this.command = command; }
    public void pressButton() { command.execute(); }
}

// Client
public class Main {
    public static void main(String[] args) {
	    // Init reciever object.
        Light livingRoomLight = new Light();
		
	    // Use a command to wrap up the reciever
        Command lightsOn = new TurnOnLightCommand(livingRoomLight);
        Command lightsOff = new TurnOffLightCommand(livingRoomLight);

        RemoteControl remote = new RemoteControl();

        remote.setCommand(lightsOn);
        remote.pressButton();  // Light is ON

        remote.setCommand(lightsOff);
        remote.pressButton();  // Light is OFF
    }
}
```
#### Use When?
- Want to แยก command or request out of the user (**invoker** who calling) and **receiver** (object who โดนกระทำ)
- Keeping the order of the commands.
- Want it to undo and redo.
- Making code flexible. (like we don't need to know how the Open Button of TV remote's work just only know sending command to TV)
