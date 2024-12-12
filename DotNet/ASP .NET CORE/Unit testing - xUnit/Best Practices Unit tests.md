###### **Isolated**
Separated from other dependencies and database.
No other classes, services, or database must be accessed in testing.
>[!question] So how do we tests if you don't have data? 
>you do [[Mocking]]
###### **One Method At A Time**
Should not test more than one method in a single test case.
	A single test case should test a single outcome of all the possible outcomes.
Should not call more than one method at a time, mock as much as possible. see: [[Mocking]].
	But, private methods are not a concern, you can call private methods.
###### **Unordered**
Individual Unit test cases should pass in any order and must not affect each other.
###### **Fast**
test cases should not take too much milliseconds and should reach more than half a second, if it does then that means your test case is too large or it is trying to access a database.
###### **Repeatable**
Tests can be run repeatedly and return the same results. Assuming no changes to the code have been made.
###### **Timely**
Time taken to write a test should not exceed the time taken to write the code being tested.