#cSharp 
In the context of unit testing, an **assert** is a statement or a method that checks whether a certain condition is true or false. It is used to validate that the behavior of the code being tested conforms to expectations.
syntax:
```c#
Assert.AssertionMethod(expectedValueOrCondition, actualValueOrCondition);
```
sample:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class CalculatorTests
{
    [TestMethod]
    public void Add_ShouldReturnSum()
    {
        // Arrange the data
        Calculator calculator = new Calculator();
        int a = 5;
        int b = 7;

        // Act on the data
        int result = calculator.Add(a, b);

        // Assert
        Assert.AreEqual(12, result); // Verifies that result is equal to 12
    }
}
```
In the example above, `Assert.AreEqual` is used to check whether the `result` is equal to the expected value of 12. If this condition is true, the test passes; otherwise, it fails

# Assert Methods:
**1. Assert.AreEqual(expected, actual)**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class StringHelperTests
{
    [TestMethod]
    public void Concatenate_ShouldReturnConcatenatedString()
    {
        // Arrange
        string str1 = "Hello, ";
        string str2 = "world!";
        string expected = "Hello, world!";

        // Act
        string result = StringHelper.Concatenate(str1, str2);

        // Assert
        Assert.AreEqual(expected, result); // Verifies that the result is as expected
    }
}
```
In this example, we have a `StringHelper` class with a `Concatenate` method, and we use `Assert.AreEqual` to validate the concatenation result.

**2. Assert.IsTrue(condition)**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class MathHelperTests
{
    [TestMethod]
    public void IsPrime_ShouldReturnTrueForPrimeNumber()
    {
        // Arrange
        int primeNumber = 7;

        // Act
        bool result = MathHelper.IsPrime(primeNumber); //MathHelper.IsPrime returns true if prime

        // Assert
        Assert.IsTrue(result); // Verifies that the number is prime
    }
}
```
Here, we have a `MathHelper` class with an `IsPrime` method, and we use `Assert.IsTrue` to validate that a prime number is correctly identified as prime.

**3. Assert.IsFalse(condition)**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class MathHelperTests
{
    [TestMethod]
    public void IsPrime_ShouldReturnFalseForNonPrimeNumber()
    {
        // Arrange
        int nonPrimeNumber = 10;

        // Act
        bool result = MathHelper.IsPrime(nonPrimeNumber);

        // Assert
        Assert.IsFalse(result); // Verifies that the number is not prime
    }
}
```
Same with IsTrue but the opposite

**4. Assert.IsNull(obj)**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class EmployeeServiceTests
{
    [TestMethod]
    public void GetEmployeeById_ShouldReturnNullForNonExistentId()
    {
        // Arrange
        int nonExistentId = 999;

        // Act
        Employee result = EmployeeService.GetEmployeeById(nonExistentId);

        // Assert
        Assert.IsNull(result); // Verifies that null is returned for a non-existent ID
    }
}
```
Here, we're using `Assert.IsNull` to verify that the `GetEmployeeById` method returns `null` for a non-existent employee ID.

**5. Assert.IsNotNull(obj)**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;

[TestClass]
public class EmployeeServiceTests
{
    [TestMethod]
    public void GetEmployeeById_ShouldReturnNotNullForExistingId()
    {
        // Arrange
        int existingId = 123;

        // Act
        Employee result = EmployeeService.GetEmployeeById(existingId);

        // Assert
        Assert.IsNotNull(result); // Verifies that a non-null result is returned for an existing ID
    }
}
```
In this example, we use `Assert.IsNotNull` to verify that the `GetEmployeeById` method returns a non-null result for an existing employee ID.

**6. `Assert.ThrowsException<TException>(action)`**:
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System;

[TestClass]
public class FileParserTests
{
    [TestMethod]
    public void ParseFile_InvalidFile_ShouldThrowFileNotFoundException()
    {
        // Arrange
        string invalidFilePath = "invalid.txt";

        // Act & Assert
        Assert.ThrowsException<FileNotFoundException>(() => FileParser.ParseFile(invalidFilePath));
        // Verifies that a FileNotFoundException is thrown when parsing an invalid file
    }
}
```
Parameters:
- TException - the type of exception expected
- action - the action to be tested, this is a method.
This is used to test and exception.
In this case, we're using `Assert.ThrowsException` to verify that the `ParseFile` method correctly throws a `FileNotFoundException` when trying to parse an invalid file.
see [[Lambda]] if youre confused about =>

**7. Assert.Collection(collection, assertActions)**
```c#
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System;
using System.Collections.Generic;

[TestClass]
public class StudentCollectionTests
{
    [TestMethod]
    public void FilterStudentsByGrade_ShouldOnlyIncludeAStudents()
    {
        // Arrange
        List<Student> students = new List<Student>
        {
            new Student("Alice", "A"),
            new Student("Bob", "B"),
            new Student("Charlie", "A"),
            new Student("David", "C"),
        };

        // Act
        List<Student> result = StudentCollection.FilterStudentsByGrade(students, "A");

        // Assert
        Assert.Collection(result,
            student => Assert.AreEqual("Alice", student.Name),
            student => Assert.AreEqual("Charlie", student.Name)
        );
        // Verifies that only students with grade "A" are included in the result
    }
}
```
Here, we use `Assert.Collection` to verify that the `FilterStudentsByGrade` method correctly filters and returns a collection of students with the specified grade "A."

Parameters:
- `collection`: The collection (e.g., a list or an array) that you want to assert.
- `assertActions`: A series of actions  that specify the assertions you want to perform for each element in the collection.
**Note:**
It is required to us a lambda or a delegate data type for the `assertActions`.
see: [[Delegate]] or [[Lambda]] for more details.
