in [[Clean Architecture]], tests will be stored in the "tests" folder, outside src folder.

The difference in N-tier architecture is that in clean architecture each functionality layer(services, controllers, repository, etc..) will have its own test project. Same principle applies here [[Unit Testing - xUnit]].

If migrating from N-tier, simply copy paste the test classes to their respective test projects, of course just the test classes, not including anything else.

Of course, don't forget to add dependencies to the corresponding test projects.
- right click on ''dependencies'' of the test projects and simply add.

