# Difference between method overloading and method overriding in C#

Method overloading and method overriding are two fundamental concepts in object-oriented programming (OOP) in C#. While both involve methods, they serve different purposes and are used in different contexts.

# 1. Method Overloading
Definition: Method overloading allows a class to have multiple methods with the same name but different signatures. A method signature can differ by the number of parameters, the types of parameters, or the order of parameters.

# Key Points:

1. Same Method Name: The methods share the same name.
2. Different Parameters: Each overloaded method must have a different parameter list.
3. Compile-Time Polymorphism: Method overloading is resolved at compile time, which is why it is also known as compile-time polymorphism.
4. Usage: Overloading is typically used when you want the same method to handle different types or numbers of arguments.
Example:

```csharp
public class Calculator
{
    // Method with two int parameters
    public int Add(int a, int b)
    {
        return a + b;
    }

    // Overloaded method with three int parameters
    public int Add(int a, int b, int c)
    {
        return a + b + c;
    }

    // Overloaded method with two double parameters
    public double Add(double a, double b)
    {
        return a + b;
    }
}

class Program
{
    static void Main()
    {
        Calculator calc = new Calculator();
        Console.WriteLine(calc.Add(5, 10)); // Calls Add(int, int)
        Console.WriteLine(calc.Add(5, 10, 15)); // Calls Add(int, int, int)
        Console.WriteLine(calc.Add(5.5, 10.5)); // Calls Add(double, double)
    }
}
```
# 2. Method Overriding
Definition: Method overriding allows a subclass to provide a specific implementation of a method that is already defined in its base (parent) class. The overridden method in the child class should have the same signature as the method in the base class.

# Key Points:

1. Same Method Signature: The overriding method must have the same name, return type, and parameters as the method in the base class.
2. Run-Time Polymorphism: Method overriding is resolved at runtime, which is why it is also known as runtime polymorphism.
3. Requires virtual and override: The base class method must be marked with the virtual keyword, and the derived class method must use the override keyword.
4. Usage: Overriding is used when the subclass needs to modify or extend the behavior of the base class method.
Example:

```csharp
public class Animal
{
    // Base class method marked as virtual
    public virtual void Speak()
    {
        Console.WriteLine("The animal makes a sound.");
    }
}

public class Dog : Animal
{
    // Derived class method overrides the base class method
    public override void Speak()
    {
        Console.WriteLine("The dog barks.");
    }
}

class Program
{
    static void Main()
    {
        Animal myAnimal = new Animal();
        myAnimal.Speak(); // Output: The animal makes a sound.

        Dog myDog = new Dog();
        myDog.Speak(); // Output: The dog barks.

        Animal anotherAnimal = new Dog();
        anotherAnimal.Speak(); // Output: The dog barks. (due to polymorphism)
    }
}
```
Summary of Differences:
<table>
<thead>
<tr><th>Aspect</th><th>Method Overloading</th><th>Method Overriding</th></tr>
</thead>
<tbody>
<tr><td><strong>Definition</strong></td><td>Multiple methods with the same name but different signatures in the same class.</td><td>Redefining a base class method in a derived class with the same signature.</td></tr><tr><td><strong>Polymorphism Type</strong></td><td>Compile-time (static) polymorphism</td><td>Runtime (dynamic) polymorphism</td></tr><tr><td><strong>Signature</strong></td><td>Must differ by parameters (number, type, or order)</td><td>Must have the same signature (name, return type, and parameters)</td></tr><tr><td><strong>Keywords</strong></td><td>No special keywords required</td><td>Requires <code>virtual</code> (base class) and <code>override</code> (derived class)</td></tr><tr><td><strong>Purpose</strong></td><td>To perform different tasks with the same method name based on different inputs.</td><td>To modify or extend the behavior of an inherited method.</td></tr><tr><td><strong>Class Relationship</strong></td><td>Can be within the same class or a derived class</td><td>Must be between a base class and a derived class</td></tr>
</tbody>
</table>


Both method overloading and method overriding are essential for achieving polymorphism in C#, allowing you to create flexible and maintainable code.
