xUnit.net is a free, open source, community-focused unit testing tool for the .NET Framework.
Different from MS test.
>[!question]- Why do I need to do this, isn't this tedious and a waste of time?
>https://www.reddit.com/r/learnprogramming/comments/u7r741/comment/i5gkz3d/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button
# How to use it?
#### First add a unit test project 
right click on solution, add new project, add xUnit test project.
	- If using [[Clean Architecture]], use the [[Tests - Clean Architecture]] folder structure.
There is no convention on naming, just name it appropriately.
#### What is Fact attribute?
`[Fact]` means that the method is a test that should be executed.
#### Naming Convention:
- Pascal Case
- First name is the name of the method to test,
- then followed by underscore and the test strategy to implement,
- the next underscore is the expected result of the test strategy.
```c#
public void NameOfTheMethodToTest_TestStrategy_expectedResult()
{
	//unit test code...
}
//sample
public void AddCity_FullCityName_ToBeSuccess() //add city using full city name expecting success
{
	//test if city is null
}
```
**Don't be confused**; the expected result is not the pass or fail of the test itself, but the expected result of the method being tested.
#### How to run a test?
For every test, there are three phases:
- **Arrange**: the declaration of variables and collecting inputs.
- **Act**: Perform the action you are testing.
- **Assert**: Verify the expected outcome.
#### sample:
suppose you have a math add method:
```c#
public class MyMath
{
    public int Add(int a, int b)
    {
        return a + b;
    }
}
```
You can test it by doing:
```c#
[Fact]
public void Add_AddTest()
{
	//arrange
	MyMath addTest = new MyMath();
	int a = 1;
	int b = 2;
	int expected = 3;
	
	//act
	int result = addTest.Add(a, b);
	 
	//assert
	Assert.Equal(expected, result);
}
```
Assert.Equal will return pass if they are equal, and the test will fail if they are not.

In VS studio open Test explorer in a dock or floating.
You can run the tests there and It will show how the test performed.

Now change the add method to deliberately return a fail, maybe instead of a `+` make it multiply `*`.
# What next?
- [[Best Practices Unit tests]].
- A Unit test must be isolated, no other classes, services, or database must be accessed in testing. So how do we test if we dont have data? we mock the data, see: [[Mocking]].
- Now that we know how to mock the DbContext, how do we mock the model objects? see [[AutoFixture]].
- [[Fluent Assertions]] - makes the Assert code look more human readable and easier to use.
- There is no output message in the test explorer window, there is only pass or fail. In order to have output messages like the equivalent of `console.writeline` you have to use `ITestOutputHelper`. See: [Capturing Output](https://xunit.net/docs/capturing-output). Allows you to see the output, which you can use to figure out why it failed or why something passed.
- Unit testing services, how to unit test a service [[Service Unit Test]].
- Unit testing the controller, [[Controller Unit Test]].
- [[Integration Test]], - Testing the whole stack instead of per unit. Essentially the opposite of unit test.
- <mark style="background: #FF5582A6;">WARNING</mark>: Contains and Equals method, compare by reference, not by value . see bottom part of [[reference type vs value type]]. So be carefull when using Assert.Contains or Assert.Equals.


```
//linq moq boilerplate
_mockDbSet.As<IQueryable<RecyclableType>>().Setup(m => m.Provider).Returns(dataList.AsQueryable().Provider);
_mockDbSet.As<IQueryable<RecyclableType>>().Setup(m => m.Expression).Returns(dataList.AsQueryable().Expression);
_mockDbSet.As<IQueryable<RecyclableType>>().Setup(m => m.ElementType).Returns(dataList.AsQueryable().ElementType);
_mockDbSet.As<IQueryable<RecyclableType>>().Setup(m => m.GetEnumerator()).Returns(dataList.GetEnumerator());
```