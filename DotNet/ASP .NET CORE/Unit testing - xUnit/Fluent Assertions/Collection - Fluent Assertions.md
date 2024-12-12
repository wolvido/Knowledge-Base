.Net Lists actually already have many methods that are extremely versatile can be used like Fluent Assertions and alongside them.
```c#
IEnumerable<int> collection = new[] { 1, 2, 5, 8 };

collection.Should().NotBeEmpty()
    .And.HaveCount(4)
    .And.ContainInOrder(new[] { 2, 5 })
    .And.ContainItemsAssignableTo<int>();

collection.Should().Equal(new List<int> { 1, 2, 5, 8 });
collection.Should().Equal(1, 2, 5, 8); 
collection.Should().NotEqual(8, 2, 3, 5);
collection.Should().BeEquivalentTo(new[] {8, 2, 1, 5});
collection.Should().NotBeEquivalentTo(new[] {8, 2, 3, 5});

collection.Should().HaveCount(c => c > 3)
  .And.OnlyHaveUniqueItems();

collection.Should().HaveCountGreaterThan(3);
collection.Should().HaveCountGreaterThanOrEqualTo(4);
collection.Should().HaveCountLessThanOrEqualTo(4);
collection.Should().HaveCountLessThan(5);
collection.Should().NotHaveCount(3);
collection.Should().HaveSameCount(new[] { 6, 2, 0, 5 });
collection.Should().NotHaveSameCount(new[] { 6, 2, 0 });

collection.Should().StartWith(1);
collection.Should().StartWith(new[] { 1, 2 });
collection.Should().EndWith(8);
collection.Should().EndWith(new[] { 5, 8 });

collection.Should().BeSubsetOf(new[] { 1, 2, 3, 4, 5, 6, 7, 8, 9, });

collection.Should().ContainSingle();
collection.Should().ContainSingle(x => x > 3);
collection.Should().Contain(8)
  .And.HaveElementAt(2, 5)
  .And.NotBeSubsetOf(new[] {11, 56});

collection.Should().Contain(x => x > 3);
collection.Should().Contain(collection, "", 5, 6); // It should contain the original items, plus 5 and 6.

collection.Should().OnlyContain(x => x < 10);
collection.Should().ContainItemsAssignableTo<int>();
collection.Should().NotContainItemsAssignableTo<string>()

collection.Should().ContainInOrder(new[] { 1, 5, 8 });
collection.Should().NotContainInOrder(new[] { 5, 1, 2 });

collection.Should().ContainInConsecutiveOrder(new[] { 2, 5, 8 });
collection.Should().NotContainInConsecutiveOrder(new[] { 1, 5, 8});

collection.Should().NotContain(82);
collection.Should().NotContain(new[] { 82, 83 });
collection.Should().NotContainNulls();
collection.Should().NotContain(x => x > 10);

object boxedValue = 2;
collection.Should().ContainEquivalentOf(boxedValue); // Compared by object equivalence
object unexpectedBoxedValue = 82;
collection.Should().NotContainEquivalentOf(unexpectedBoxedValue); // Compared by object equivalence

const int successor = 5;
const int predecessor = 5;
collection.Should().HaveElementPreceding(successor, element);
collection.Should().HaveElementSucceeding(predecessor, element);

collection.Should().BeEmpty();
collection.Should().BeNullOrEmpty();
collection.Should().NotBeNullOrEmpty();

IEnumerable<int> otherCollection = new[] { 1, 2, 5, 8, 1 };
IEnumerable<int> anotherCollection = new[] { 10, 20, 50, 80, 10 };
collection.Should().IntersectWith(otherCollection);
collection.Should().NotIntersectWith(anotherCollection);

var singleEquivalent = new[] { new { Size = 42 } };
singleEquivalent.Should().ContainSingle()
    .Which.Should().BeEquivalentTo(new { Size = 42 });
```