```c#
string theString = "";
theString.Should().NotBeNull();
theString.Should().BeNull();
theString.Should().BeEmpty();
theString.Should().NotBeEmpty("because the string is not empty");
theString.Should().HaveLength(0);
theString.Should().BeNullOrWhiteSpace(); // either null, empty or whitespace only
theString.Should().NotBeNullOrWhiteSpace();

theString.Should().BeUpperCased();
theString.Should().NotBeUpperCased();
theString.Should().BeLowerCased();
theString.Should().NotBeLowerCased();
```