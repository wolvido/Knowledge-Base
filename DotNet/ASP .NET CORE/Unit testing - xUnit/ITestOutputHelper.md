There is no output message in the test explorer window, there is only pass or fail. In order to have output messages like the equivalent of `console.writeline` you have to use `ITestOutputHelper`. Allows you to see the output, which you can use to figure out why it failed or why something passed.  See: [Capturing Output](https://xunit.net/docs/capturing-output)
# How-To:
Simply inject it in the test class, assuming you are using x-unit.
```csharp
public class MyTestClass
{
    private readonly ITestOutputHelper _testOutputHelper;

    public MyTestClass(ITestOutputHelper testOutputHelper)
    {
        _testOutputHelper = testOutputHelper;
    }

    [Fact]
    public void MyTest()
    {
        var temp = "my class!";
        _testOutputHelper.WriteLine("This is output from {0}", temp);
    }
}
```