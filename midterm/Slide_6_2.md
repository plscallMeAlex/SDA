# SDA Adapter and Facade
## Introduction
The slide talks about **good design principles** and **two important design patterns: Adapter and Facade**
- The **principles** (SRP, LSP, ISP) help you design the classes and interfaces that are **clean, flexible, and easy to change.**
- The **patterns** (Adapter and Facade) are ways to **connect or simplify systems without rewriting everything.**
The goal is to build software that is:
- **easy to maintain** (you can change one part without breaking everything),
- **easy to extend** (adding new feature without editing the old code),
- **easy to use** (hide the complexity internally)
## Four Design Smells
There are warning sign that show your design is weak.
- **Rigidity**: changing one thing makes you change many other things.
- **Fragility**: one small change causes bugs else where.
- **Immobility**: can't use class because it tied up with others.
- **Needless Repetition**: duplicate code everywhere.
## The 3 principles
### Single Responsibility Principle (SRP)
A class should have one reason to change and each class must do one jobs (**one responsibility**), if not while the requirement change it will break the code.
**Example:**
- Student stores data and decides sorting order.
- Student only store data. Sorting is handled by (another class) a separate Comparator or Utility class.
### Liskov Substitution Principle (LSP)
![[Pasted image 20250821191350.png]]
The subclass must be usable anywhere the parent class is used.
>> **"คลาสลูก (Subclass) ต้องสามารถใช้แทนคลาสแม่ (Superclass) ได้ โดยที่ไม่ทำให้พฤติกรรมของโปรแกรมผิดเพี้ยน"**

Where the parent class can be usable then the sub-class is need to be usable also
- Inheritance safely
- Keep polymorphism work correctly.
 If the class behavior is very different then extract it don't do inheritance.
### Interface Segregation Principle (ISP)
Clients don't need to implement the method that they don't need. 
And it need to break large interface to smaller and focused one.
![[Pasted image 20250821194203.png]]
## Structural Pattern
Used to rearrange the structure or composition (เชื่อมต่อ) of the object make the system flexible, maintainable and reusable.
It contain 2 Pattern
- **Adapter** - Make the class interface ทำให้ class ที่ interface ไม่เข้ากัน สามารถใช้งานร่วมกันได้
	**example**: USB-C -> USB-A adapter.
- **Facade** - ทำ interface ง่าย ๆ ซ่อนความซับซ้อนของ subsystem
	**example**: ปุ่มเดียวครอบคลุมทั้ง TV, Radio, Projector.
### Adapter Pattern
Adapter is used to convert invert the interface of some class that client aspect to another class by without rewrite the code of that class.
- Role is the middle man for converting the class to other class.
- Suitable for the lib or API that we can't change
- Client can use via desire interface.
#### Use When?
When we want to integrate a new project with a new project without rewriting a old code.
When the interface of the class is not follow the client desire.
When it have a code legacy or 3rd-party-lib that cannot change.
#### Example
We have code that need to use duck
```java
interface Duck {
    void quack();
    void fly();
}
```
But we have turkey which the interface is not the same
```java
class Turkey {
    void gobble() { System.out.println("Gobble gobble!"); }
    void fly() { System.out.println("Flying short distance"); }
}
```
The client want to use duck but have Turkey ?
Then create the TurkeyAdapter implement Duck
```java
class TurkeyAdapter implements Duck {
    Turkey turkey;
    TurkeyAdapter(Turkey turkey) { this.turkey = turkey; }

    public void quack() { turkey.gobble(); }
    public void fly() {
        for(int i=0; i<5; i++) { turkey.fly(); } // ไก่งวงบินสั้น → ทำซ้ำ
    }
}
```
Result is the client is using Duck but internally using the turkey.
### Facade Pattern
Facade use **"make interface simpler"** to hide the complexity in the internal subsystem.
- Not change the interface of current subsystem.
- Just create another middle class to make the client use simpler.
- Hide the step inside the system.
#### Use When ?
- When the system have a lot of complexity of **class/subsystem** that client need to use by itself all.
- Want to reduce the dependent of subsystem directly.
- When we want the newcomer understand the system easier โดยมี method รวบรัด
#### Example
If we have **Home Theater** (Main System) it need have this **subsystem** also:
- **DVDPlayer**
- **Projector**
- **SoundSystem**
Before the client need ทูเปิดทีละเครื่อง -> มันยุ่งยาก
**Solution**: Create **HomeTheaterFacade**
```java
class HomeTheaterFacade {
    DVDPlayer dvd;
    Projector projector;
    SoundSystem sound;

    HomeTheaterFacade(DVDPlayer d, Projector p, SoundSystem s) {
        dvd = d; projector = p; sound = s;
    }

    void watchMovie(String movie) {
        System.out.println("Get ready to watch a movie...");
        projector.on();
        sound.on();
        sound.setSurroundSound();
        dvd.on();
        dvd.play(movie);
    }
}
```
**Result:** User will only call this function.
```java
homeTheater.watchMovie("Inception");
```
Instead of calling each subsystem by one.
### Adapter vs Decorator
**Adapter**
- Change the interface appearance to be compatible.
- Use when: client want อยากได้ interface แต่ object เดิมให้ interface ไม่ตรง
- Focus: interface compatibility.
- Example: USB adapter USB-C to USB-A.
**Decorator**
- Not changing the interface -> instead wrap a new function (wrapping the object)
- Use when: Add behavior without editing the code.
- Focus: add functionality by using the old method.
- Example: Basic Coffee -> wrap with milk -> wrap with caramel. (It still a coffee).
