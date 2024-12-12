#cSharp 
# A basic introduction
The main objective in unit testing is to isolate a unit part of code and validate its to correctness and reliable.
We will use Microsoft Testing tools, which is MS Unit Test
### Startup
Create a test:
![[Pasted image 20231004113149.png]]

![[Pasted image 20231004113250.png]]

In order to access all the project, add a reference in the test project.
![[Pasted image 20231004113423.png]]

In the samples below we will use **Asserts**/ see: [[Asserts]] for more info, if youre not familliar with asserts it is recommended to read [[Asserts]] note.
## How to Unit test
sample:
```c#
public class BasicMaths
{
    public double Add(double num1, double num2)
    {
        return num1 + num2;
    }
    public double Subtract(double num1, double num2)
    {
        return num1 - num2;
    }
    public double divide(double num1, double num2)
    {
        return num1 / num2;
    }
    public double Multiply(double num1, double num2)
    {
        // To trace error while testing, writing + operator instead of * operator.
        return num1 + num2;
    }
}
```

test project:
```c#
[TestClass]
public class UnitTest1
{
	[TestMethod]
	public void Test_AddMethod()
	{
		BasicMaths bm = new BasicMaths(); //arrange the test data
		
		double res = bm.Add(10, 10); //act on the data
		
		Assert.AreEqual(res, 20); //assert checks wether the statement is true or false
	}
	[TestMethod]
	public void Test_SubtractMethod()
	{
		BasicMaths bm = new BasicMaths();
		
		double res = bm.Subtract(10, 10);
		
		Assert.AreEqual(res, 0);
	}
	[TestMethod]
	public void Test_DivideMethod()
	{
		BasicMaths bm = new BasicMaths();
		
		double res = bm.divide(10, 5);
		
		Assert.AreEqual(res, 2);
	}
	[TestMethod]
	public void Test_MultiplyMethod()
	{
		BasicMaths bm = new BasicMaths();
		
		double res = bm.Multiply(10, 10);
		
		Assert.AreEqual(res, 100);
	}
}
```