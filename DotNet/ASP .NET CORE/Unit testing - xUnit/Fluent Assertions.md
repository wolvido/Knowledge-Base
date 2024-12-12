The assert code is somewhat hard to read as a human, **Fluent Assertions** makes the Assert code look more human readable and easier to use.
![[Pasted image 20240214183342.png]]
# How-To:
First In your test project, Nuget install **`FluentAssertions`**.
sample:
```c#
[Fact]
public void ShouldAddTwoNumbers()
{
	// Arrange
	int a = 2;
	int b = 3;
	
	// Act
	int result = a + b;
	
	// Assert
	result.Should().Be(5); // Fluent Assertions syntax
}
```
#### Chaining
One neat feature is the ability to chain a specific assertion on top of an assertion.
```c#
dictionary.Should().ContainValue(myClass).Which.SomeProperty.Should().BeGreaterThan(0);

someObject.Should().BeOfType<Exception>().Which.Message.Should().Be("Other Message");

xDocument.Should().HaveElement("child").Which.Should().BeOfType<XElement>().And.HaveAttribute("attr", "1");
```
This chaining can make your unit tests a lot easier to read.
## Assertions
See all the assertions below, or you can also see it in intellisense
##### Basic Assertions
```c#
object theObject = null;
theObject.Should().BeNull("because the value is null");
theObject.Should().NotBeNull();
```
Check the type:
```c#
theObject = "whatever";
theObject.Should().BeOfType<string>(); 
theObject.Should().BeOfType(typeof(string));
```
Check equivalence or not:
```c#
theObject.Should().Be(otherObject, "because they have the same values");
theObject.Should().NotBe(otherObject);
```
If you want to make sure two objects are not just functionally equal but refer to the exact same object in memory, use the following two methods:
```c#
theObject = otherObject;
theObject.Should().BeSameAs(otherObject);
theObject.Should().NotBeSameAs(otherObject);
```
##### Nullable Assertions:
```c#
short? theShort = null;
theShort.Should().NotHaveValue();
theShort.Should().BeNull();
theShort.Should().Match(x => !x.HasValue || x > 0);

int? theInt = 3;
theInt.Should().HaveValue();
theInt.Should().NotBeNull();

DateTime? theDate = null;
theDate.Should().NotHaveValue();
theDate.Should().BeNull();
```
###### Booleans:
```c#
bool theBoolean = false;
theBoolean.Should().BeFalse("it's set to false");

theBoolean = true;
theBoolean.Should().BeTrue();
theBoolean.Should().Be(otherBoolean);
theBoolean.Should().NotBe(false);
```
###### [[Strings - Fluent Assertions]]
###### [[Numeric types and everything else that implements IComparable - Fluent Assertions]]
###### [[Collection - Fluent Assertions]]
#### The Rest From the Documentation:
###### [Exceptions - Fluent Assertions](https://fluentassertions.com/exceptions/)
###### [Dates & Times - Fluent Assertions](https://fluentassertions.com/datetimespans/)
###### [Dictionaries - Fluent Assertions](https://fluentassertions.com/dictionaries/)
###### [Guids - Fluent Assertions](https://fluentassertions.com/guids/)
###### [Enums - Fluent Assertions](https://fluentassertions.com/enums/)
###### [System.Data - Fluent Assertions](https://fluentassertions.com/data/)
###### [Object graph comparison - Fluent Assertions](https://fluentassertions.com/objectgraphs/)
###### [Event Monitoring - Fluent Assertions](https://fluentassertions.com/eventmonitoring/)
###### [Type, Method, and Property assertions - Fluent Assertions](https://fluentassertions.com/typesandmethods/)
###### [Assembly References - Fluent Assertions](https://fluentassertions.com/assemblies/)
###### [XML - Fluent Assertions](https://fluentassertions.com/xml/)
###### [Execution Time - Fluent Assertions](https://fluentassertions.com/executiontime)
###### [HttpResponseMessages - Fluent Assertions](https://fluentassertions.com/httpresponsemessages/)