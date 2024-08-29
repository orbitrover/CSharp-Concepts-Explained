# Extension Method In C#
<div class="markdown prose w-full break-words dark:prose-invert light">
	<p>In C#, <strong>extension methods</strong> allow you to add new methods to existing types (such as classes, interfaces, or structs) without modifying the original type's source code or creating a new derived type. This is particularly useful when you want to add functionality to types that you don't own or can't change, such as .NET framework classes or third-party libraries.</p>
	<h3>Key Points of Extension Methods:</h3>
	<ul>
		<li><strong>Static Class</strong>: Extension methods are defined as static methods in a static class.</li>
		<li><strong><code>this</code> Keyword</strong>: The first parameter of the method is prefixed with the <code>this</code> keyword, and this parameter specifies the type the method extends.</li>
		<li><strong>Instance-like Invocation</strong>: Once an extension method is defined, you can call it as if it were an instance method on the type it extends.</li>
		<li><strong>No Modifications</strong>: The original type is not modified; the extension methods are syntactic sugar that the compiler uses to treat the static methods as if they were instance methods.</li></ul>
	<h3>Example of an Extension Method</h3>

	
```csharp
using System;

// Use the Extension Method
public class Program
{
	public static void Main()
	{
		string sentence = "This is an example sentence with five words.";

	        // Using the extension method as if it were an instance method
	        int wordCount = sentence.WordCount();
	
	        Console.WriteLine($"The sentence has {wordCount} words.");
			
					int number = 42;
	
	        // Using the extension method to check if the number is even
	        bool isEven = number.IsEven();
	
	        Console.WriteLine($"{number} is even: {isEven}");
	
	        int anotherNumber = 33;
	
	        // Using the extension method on another number
	        bool isAnotherEven = anotherNumber.IsEven();
	
	        Console.WriteLine($"{anotherNumber} is even: {isAnotherEven}");
		Console.WriteLine(" ");
		// here is a complex example of filtering a class list with using linq filter like where or find
		ComplexExtensionMethodClass.Run();
	}
}

// Step 1: Create a static class to hold the extension method
public static class StringExtensions
{
	// Step 2: Define the extension method
	public static int WordCount(this string str)
	{
		if (string.IsNullOrEmpty(str))
			return 0;

		// Split the string into words by spaces
		string[] words = str.Split(new char[] { ' ', '\t', '\n' }, StringSplitOptions.RemoveEmptyEntries);

		return words.Length;
	}
	
	// Extension method to check if an integer is even
	public static bool IsEven(this int number)
	{
		return number % 2 == 0;
	}
}
public class ComplexExtensionMethodClass
{
    public static void Run()
    {
        var employees = new List<Employee>
        {
            new Employee { EmployeeId = 1, EmployeeName = "John Doe", EmployeeMobile = "1234567890" },
            new Employee { EmployeeId = 2, EmployeeName = "Jane Smith", EmployeeMobile = "0987654321" },
            new Employee { EmployeeId = 3, EmployeeName = "Alice Johnson", EmployeeMobile = "5555555555" }
        };

        // Find employee by name
        var employeeByName = employees.FindByProperty("EmployeeName", "Jane Smith");
        Console.WriteLine($"Found Employee: {employeeByName?.EmployeeName}, Mobile: {employeeByName?.EmployeeMobile}");

        // Find employee by mobile
        var employeeByMobile = employees.FindByProperty("EmployeeMobile", "5555555555");
        Console.WriteLine($"Found Employee: {employeeByMobile?.EmployeeName}, Mobile: {employeeByMobile?.EmployeeMobile}");

        // Example with a different class
        var products = new List<Product>
        {
            new Product { ProductId = 1, ProductName = "Laptop", Price = 1000 },
            new Product { ProductId = 2, ProductName = "Smartphone", Price = 500 }
        };

        var productByName = products.FindByProperty("ProductName", "Laptop");
        Console.WriteLine($"Found Product: {productByName?.ProductName}, Price: {productByName?.Price}");
    }
}
public static class ListExtensions
{
    public static T FindByProperty<T>(this List<T> list, string propertyName, object value)
    {
        return list.FirstOrDefault(item =>
        {
            var prop = typeof(T).GetProperty(propertyName, BindingFlags.IgnoreCase | BindingFlags.Public | BindingFlags.Instance);
            if (prop == null)
            {
                throw new ArgumentException($"Property '{propertyName}' not found on type '{typeof(T)}'");
            }
            var propValue = prop.GetValue(item);
            return propValue != null && propValue.Equals(value);
        });
    }
}
public class Employee
{
    public int EmployeeId { get; set; }
    public string EmployeeName { get; set; }
    public string EmployeeMobile { get; set; }
}

public class Product
{
    public int ProductId { get; set; }
    public string ProductName { get; set; }
    public double Price { get; set; }
}
```
<h3>Explanation:</h3>
<ol>
	<li><p><strong>Static Class</strong>: The extension method <code>WordCount</code> is defined in a static class named <code>StringExtensions</code>.</p></li>
	<li><p><strong><code>this</code> Keyword</strong>: The method signature <code>public static int WordCount(this string str)</code> indicates that this method is an extension of the <code>string</code> type. The <code>this</code> keyword before the first parameter (<code>string str</code>) tells the compiler that this is an extension method.</p></li>
	<li><p><strong>Method Usage</strong>: In the <code>Main</code> method, <code>WordCount</code> is called on the <code>sentence</code> string variable as if it were an instance method, even though it's technically a static method defined elsewhere.</p></li>
</ol>
<h3>Benefits of Extension Methods:</h3>
<ul>
	<li><strong>Convenience</strong>: Makes it easier to call utility functions in a way that feels natural and keeps code clean.</li>
	<li><strong>Encapsulation</strong>: Allows you to add methods to types without modifying the types themselves, adhering to the open/closed principle.</li>
	<li><strong>Readability</strong>: Improves code readability by allowing methods to be called in a natural, instance-method-like syntax.</li>
</ul>
<h3>Limitations:</h3>
<ul>
	<li><strong>Only Accessible via Static Class</strong>: Extension methods are only available when the static class containing them is in scope.</li>
	<li><strong>Overload Resolution</strong>: If an instance method with the same signature exists on the type, it will take precedence over the extension method.</li>
	<li><strong>Misuse</strong>: Overuse or misuse of extension methods can lead to cluttered or confusing code if not carefully managed.</li>
</ul>
 <h3>Conclusion:</h3>
 <p>Extension methods are a powerful feature in C# that allows you to extend existing types with new functionality in a clean and natural way, without altering the original types.</p>
 </div>
