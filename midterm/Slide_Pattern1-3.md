# Principle
## High-Level Principle
- SOLID 
- คิดตื้น
- เน้น **การนิยามนโยบาย กฎเกณฑ์ หรือ behavior หลักของระบบ**
- ไม่ผูกติดกับรายละเอียดการทำงานจริง (implementation detail)
## Low-Level Principle
- คิดลึก
- เป็นหลักการออกแบบระดับ "รายละเอียด" (concrete level)
- เน้นการ **implement** ฟังก์ชันการทำงานที่จับต้องได้
# Observer Pattern
It like having a host (Subject) and broadcast to the object that subscribed.
**Subscribe/Notify**
![[Pasted image 20250822142122.png]]

## Use When
- Subject เปลี่ยนบ่อย need to notify many observer
- don't want a tight coupling.  (subject just notify, observer just subscribe or unsub)
- One to many
## Example Code
```csharp
// Subject
class Stock
{
    private List<IObserver> observers = new List<IObserver>();
    private int price;

    public void Attach(IObserver observer) => observers.Add(observer);
    public void Detach(IObserver observer) => observers.Remove(observer);

    public void SetPrice(int newPrice)
    {
        price = newPrice;
        Notify();
    }

    private void Notify()
    {
        foreach (var observer in observers)
        {
            observer.Update(price);
        }
    }
}

// Observer interface
interface IObserver
{
    void Update(int price);
}

// Concrete Observer
class Investor : IObserver
{
    private string name;
    public Investor(string name) => this.name = name;

    public void Update(int price)
    {
        Console.WriteLine($"{name} ได้รับแจ้ง: ราคาหุ้นเปลี่ยนเป็น {price} บาท");
    }
}
```
Usage
```csharp
var stock = new Stock();
var a = new Investor("คุณเอ");
var b = new Investor("คุณบี");

stock.Attach(a);
stock.Attach(b);

stock.SetPrice(100); // แจ้งทั้งคุณเอและคุณบี
stock.SetPrice(120); // แจ้งอีกครั้ง
```
# Delegation Pattern
Delegation การส่งต่อ (delegate) งานที่ตัวเองไม่ทำไปให้อีกวัตถุ
"**Instead of do by itself just passing to another to work on**"
![[Pasted image 20250822143319.png]]
## Use When
- Don't want a class to do everything.
- Use the composition concept instead of inheritance.
## Example Code
```csharp
// Delegate class
class Secretary
{
    public void ArrangeMeeting()
    {
        Console.WriteLine("เลขาจัดประชุมเรียบร้อยแล้ว");
    }
}

// Delegator class
class Boss
{
    private Secretary secretary = new Secretary();

    public void HandleTask()
    {
        Console.WriteLine("เจ้านายไม่ทำเอง มอบหมายให้เลขา");
        secretary.ArrangeMeeting(); // delegate ไปที่ Secretary
    }
}

class Program
{
    static void Main()
    {
        Boss boss = new Boss();
        boss.HandleTask();
    }
}
```

# Strategy Pattern
เราสามารถการทำงานระหว่าง runtime ได้โดยไม่ต้องแก้ code
เหมือนเราเลือก strategy ที่จะทำสับเปลี่ยนได้
![[Pasted image 20250822144133.png]]
## Use When
- Have a multiple strategy (algorithm) to use that can swap the usage.
- Don't want the long if else (if (stra1) {do_strategy1} else if (stra2) {do_strategy2} ). **Make the code cleaner**.
- Open for add (strategy) but close for modify.
## Example Code
```csharp
// Strategy Interface
interface IPaymentStrategy
{
    void Pay(int amount);
}

// Concrete Strategies
class CashPayment : IPaymentStrategy
{
    public void Pay(int amount) => Console.WriteLine($"จ่ายเงินสด {amount} บาท");
}

class CreditCardPayment : IPaymentStrategy
{
    public void Pay(int amount) => Console.WriteLine($"จ่ายด้วยบัตรเครดิต {amount} บาท");
}

class PromptPayPayment : IPaymentStrategy
{
    public void Pay(int amount) => Console.WriteLine($"จ่ายด้วย PromptPay {amount} บาท");
}

// Context
class ShoppingCart
{
    private IPaymentStrategy paymentStrategy;

    public ShoppingCart(IPaymentStrategy strategy)
    {
        paymentStrategy = strategy;
    }

    public void Checkout(int amount)
    {
        paymentStrategy.Pay(amount);
    }
}
```
Usage
```csharp
class Program
{
    static void Main()
    {
        ShoppingCart cart1 = new ShoppingCart(new CashPayment());
        cart1.Checkout(500);

        ShoppingCart cart2 = new ShoppingCart(new PromptPayPayment());
        cart2.Checkout(1200);
    }
}
```

# Decorator Pattern
Adding the functionality by just wrapping without edit the old code.
"**Decorate more but can use the old functional**"
## Use When
- Add more ability but don't want to edit the class.
- Want to decorate flexible.
- Don't want too much inheritance (**CoffeeWithMilkAndSugarAndWhip** we can use wrapping it self) 
## Example Code
```csharp
// Component
interface IBeverage
{
    string GetDescription();
    double GetCost();
}

// Concrete Component
class MilkTea : IBeverage
{
    public string GetDescription() => "ชานม";
    public double GetCost() => 25;
}

// Base Decorator
abstract class ToppingDecorator : IBeverage
{
    protected IBeverage beverage;
    public ToppingDecorator(IBeverage beverage) { this.beverage = beverage; }

    public abstract string GetDescription();
    public abstract double GetCost();
}

// Concrete Decorators
class Bubble : ToppingDecorator
{
    public Bubble(IBeverage beverage) : base(beverage) { }
    public override string GetDescription() => beverage.GetDescription() + " + ไข่มุก";
    public override double GetCost() => beverage.GetCost() + 5;
}

class WhippedCream : ToppingDecorator
{
    public WhippedCream(IBeverage beverage) : base(beverage) { }
    public override string GetDescription() => beverage.GetDescription() + " + วิปครีม";
    public override double GetCost() => beverage.GetCost() + 10;
}
```
Usage
```csharp
class Program
{
    static void Main()
    {
        IBeverage order = new MilkTea();                  // เริ่มจากชานม
        order = new Bubble(order);                        // ใส่ไข่มุก
        order = new WhippedCream(order);                  // ใส่วิปครีมเพิ่ม

        Console.WriteLine(order.GetDescription());        // ชานม + ไข่มุก + วิปครีม
        Console.WriteLine($"ราคา: {order.GetCost()} บาท"); // 40 บาท
    }
}
```

# Factory Method
มีตัว factory สำหรับไว้สร้าง object แทนที่เราจะสร้าง new object ด้วยตัวเองใน main program.
เหมือนเราส่งตัวเลือกหรือสั่งทำ (string) ไปให้ factory มันจะสร้างให้เรา.
"อยากได้ object แต่ไม่อยากบอกว่าต้องสร้างแบบไหน ก็แค่ส่งให้ factory เป็นคนสร้างเอง"
## Use When.
- ไม่รู้ล่วงหน้าว่าจะสร้างสินค้าประเภทไหน อาจจะเพราะขึ้นอยู่กับสถาณการ์ณ
- ให้ subclass ตัดสินว่าจะสร้างอะไร
- ลดการใช้ new กับ object ตรงๆ
- Open for add but close for modify (Open-Closed Principle)
## Example Code
```csharp
// Product
abstract class Vehicle
{
    public abstract void Drive();
}

// Concrete Products
class Car : Vehicle
{
    public override void Drive() => Console.WriteLine("ขับรถเก๋งไปทำงาน");
}

class Truck : Vehicle
{
    public override void Drive() => Console.WriteLine("ขับรถกระบะขนของ");
}

// Creator
abstract class VehicleFactory
{
    public abstract Vehicle CreateVehicle();
}

// Concrete Factories
class CarFactory : VehicleFactory
{
    public override Vehicle CreateVehicle() => new Car();
}

class TruckFactory : VehicleFactory
{
    public override Vehicle CreateVehicle() => new Truck();
}
```
Usage
```csharp
class Program
{
    static void Main()
    {
        VehicleFactory factory;

        factory = new CarFactory();
        Vehicle car = factory.CreateVehicle();
        car.Drive();

        factory = new TruckFactory();
        Vehicle truck = factory.CreateVehicle();
        truck.Drive();
    }
}
```
