# Fibonacci series program in C#
In mathematics, the Fibonacci sequence is a sequence in which each number is the sum of the two preceding ones. 
Numbers that are part of the Fibonacci sequence are known as Fibonacci numbers, commonly denoted Fn . 
The sequence commonly starts from 0 and 1, although some authors start the sequence from 1 and 1 or sometimes (as did Fibonacci) from 1 and 2. 
Starting from 0 and 1, the sequence begins[1]
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ....
```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using Newtonsoft.Json;
					
public class Program
{
	public static void Main()
	{
		// here my target to print array range below (< 10)
		// [0,1,1,2,3,5,8]
		int n = 10;
		// SolutionOne(n); 
		// Check Time Complexity For SolutionOne?
		TestTimeComplexity(SolutionOne, n);
		
		// SolutionTwo(n);
		// Check Time Complexity For SolutionTwo?
		TestTimeComplexity(SolutionTwo, n);
		
		// SolutionThree(n);
		// Check Time Complexity For SolutionThree?
		TestTimeComplexity(SolutionThree, n);
	}
	
	// Fastest Sultion Taking upTo 0 MS iin Execution
	public static void SolutionTwo(int n)
	{
		List<int> responseList = new List<int>();
		int preValue1=0; int preValue2=1;
		for(int i=0; i < n; i++)
		{
			responseList.Add(preValue1);
			int newvalue = preValue1;
			preValue1 = preValue2;
			preValue2 = newvalue + preValue2;
		}
		// Note: JsonConvert can increase time of exceution?
		//Console.WriteLine("2. Response in array: " + JsonConvert.SerializeObject(responseList));
		Console.WriteLine("2. Response in string: " + string.Join(",",responseList.ToArray()));
		
	}
	
	// Second Fast Sultion Taking upTo 4 MS iin Execution
	public static void SolutionThree(int n)
	{
		var fibonacciSequence = Enumerable.Range(0, n)
                                          .Aggregate(new List<int> { 0, 1 }, (list, _) =>
                                          {
                                              list.Add(list[^1] + list[^2]);
                                              return list;
                                          })
                                          .Take(n)
                                          .ToList();
		// Note: JsonConvert can increase time of exceution?
        //Console.WriteLine("3. Response in array: " + JsonConvert.SerializeObject(fibonacciSequence));
		Console.WriteLine("3. Response in string: " + string.Join(",",fibonacciSequence.ToArray()));
	}
	
	// Third Fast Sultion Taking upTo 14 MS in Execution
	public static void SolutionOne(int n)
	{
		List<int> responseList = new List<int>();
		int preValue1=0; int preValue2=1;
		for(int i=0; i < n; i++)
		{
				if(i == 0)
					responseList.Add(preValue1);
				else if(i == 1)
					responseList.Add(preValue2);
				else
				{
					int newvalue = preValue1 + preValue2;
					responseList.Add(newvalue);
					preValue1 = preValue2;
					preValue2 = newvalue;
				}
			
		}
		// Note: JsonConvert can increase time of exceution?
		//Console.WriteLine("1. Response in array: " + JsonConvert.SerializeObject(responseList));
		Console.WriteLine("1. Response in string: " + string.Join(",",responseList.ToArray()));
	}
	
	
	public delegate void RunSolution(int n);
	// Using a parameterize delegate with void return for executing Solutions in TestTimeComplexity.
	public static void TestTimeComplexity(RunSolution func, int n)
	{
		Stopwatch _stopWatch = Stopwatch.StartNew();
		func(n);
		_stopWatch.Stop();
		 Console.WriteLine($"Time Taken: {_stopWatch.ElapsedMilliseconds} ms");
		// check memory cunsuption
		long memoryBefore = GC.GetTotalMemory(true);
		func(n);
		long memoryAfter = GC.GetTotalMemory(false);
		long memoryUsed = memoryAfter - memoryBefore;
		Console.WriteLine($"Memory Used: {memoryUsed} bytes");
		Console.WriteLine(" ");
	}
}
```
