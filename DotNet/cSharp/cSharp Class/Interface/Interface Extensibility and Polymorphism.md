---
keywords: interface list
---
#cSharp 

this example:
```c#
public interface ILogger
{
    void Log(string message);
}

public class ConsoleLogger : ILogger
{
    public void Log(string message)
    {
        Console.WriteLine($"[Console] {DateTime.Now}: {message}");
    }
}

public class FileLogger : ILogger
{
    private string filePath;

    public FileLogger(string filePath)
    {
        this.filePath = filePath;
    }

    public void Log(string message)
    {
        // You can implement file logging here, but for simplicity, we'll just print to the console.
        Console.WriteLine($"[File] {DateTime.Now}: {message}");
    }
}

public class DbMigrator
{
    private ILogger logger;

    public DbMigrator(ILogger logger)
    {
        this.logger = logger;
    }

    public void Migrate()
    {
        // Simulate a database migration
        logger.Log("Starting database migration...");
        logger.Log("Database migration completed successfully.");
    }
}

class Program
{
    static void Main(string[] args)
    {
        ILogger consoleLogger = new ConsoleLogger();
        ILogger fileLogger = new FileLogger("log.txt");

        DbMigrator migratorWithConsoleLogger = new DbMigrator(consoleLogger);
        DbMigrator migratorWithFileLogger = new DbMigrator(fileLogger);
		//notice we initiated a console logger and a file logger without ever changing the code in db migrator
		//that is extensibility, that is the true power of interface.
		//interface allows for classes to have extension points like Ilogger that changes its behaviour without modifying the class. You only need to extend behaviour by creating a new implementation of the interface. Genius.
		//basically just inject an extension point / interface in a class, and create as many polymorph as possible.

        migratorWithConsoleLogger.Migrate();
        migratorWithFileLogger.Migrate();

        Console.ReadKey(); // To keep the console window open
    }
}
```
A file or console logger is not the only scenario possible. To give you an idea, here are some mind-blowing uses:
- If you have a gps app, and you need to calculate the shortest route, you can make a IRouteCalculator Interface, then in case you develop a new algorithm that calculates a faster route, you can just make that algorithm and inject it in the class through the interface parameter without ever modifying anything, just add the algorithm alongside the old.
- or maybe an app that needs encryption, you just make an IEncryptor and add encrypting algorithms as many as you want without modifying anything.
- many more scenarios can exist just use your imagination, I know you can easily.

**NOTE:** 
- if your confused about this `ILogger consoleLogger = new ConsoleLogger();` where the interface is used as a variable, see [[Interface as a variable]].
- You can also use a class to feed the injection see sample below.

Another example that uses a list of interface implementation:
```c#
// Define the IReportGenerator interface
public interface IReportGenerator
{
    void GenerateReport();
}

// Implement the interface in different report generator classes
public class PdfReportGenerator : IReportGenerator
{
    public void GenerateReport()
    {
        Console.WriteLine("Generating PDF report...");
    }
}

public class CsvReportGenerator : IReportGenerator //another implement
{
    public void GenerateReport()
    {
        Console.WriteLine("Generating CSV report...");
    }
}

public class ReportProcessor
{
    private List<IReportGenerator> _reportGenerators = new();
    
    public void AddReportGenerator(IReportGenerator reportGenerator)
    {
        _reportGenerators.Add(reportGenerator);
    }
    
    public void GenerateReports()
    {
        foreach (var generator in _reportGenerators)
        {
            generator.GenerateReport();
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        ReportProcessor reportProcessor = new ReportProcessor();
        
        // Add report generators to the processor
        //its the PdfReportGenerator class itself that is in the object parameter, not the PdfReportGenerator object
        reportProcessor.AddReportGenerator(new PdfReportGenerator()); 
        reportProcessor.AddReportGenerator(new CsvReportGenerator());
        
        // Generate reports
        reportProcessor.GenerateReports();
    }
}
```
##### Interface with generic
It allows interface to be even more polymorphic. see [[Polymorphism]].
In technical terms, we understand that classes can accept generic, generic in interface allows or forces the deriving classes of the interface to use a generic on their contracts/interface methods. The classes can then implement the generic.  see example below. see [[Knowledge Base/DotNet/cSharp/cSharp Keywords and Additional Material/generic|generic]] if you forgot.
example:
```c#
// Define a generic interface
public interface IRepository<T> //it is the repository of type T, it can be a repository of Animals, Users, etc.
{
    // Method to add T to the repository
    void Add(T item);

    // Method to retrieve a T by its ID
    T GetById(int id);

    // Method to update an existing T item
    void Update(T item);

    // Method to delete a T item
    void Delete(T item);
}

public class UserRepository : IRepository<User> // A class that implements the generic interface
{
    private List<User> users = new List<User>();

    public void Add(User item) //in this example the class sets the T as User type.
    {
        users.Add(item);
    }

    public User GetById(int id)
    {
        return users.FirstOrDefault(user => user.Id == id);
    }

    public void Update(User item)
    {
        var existingUser = GetById(item.Id);
        if (existingUser != null)
        {
            // Update the user
            existingUser.Name = item.Name;
            existingUser.Email = item.Email;
        }
        else
        {
            throw new InvalidOperationException("User not found");
        }
    }

    public void Delete(User item)
    {
        users.Remove(item);
    }
}

public class User // A sample class that represents a User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

class Program
{
    static void Main(string[] args)
    {
        // Create an instance of UserRepository
        var userRepository = new UserRepository();

        // Add a new user
        var newUser = new User { Id = 1, Name = "John Doe", Email = "john@example.com" };
        userRepository.Add(newUser);

        // Retrieve and update the user
        var retrievedUser = userRepository.GetById(1);
        if (retrievedUser != null)
        {
            retrievedUser.Name = "Updated Name";
            userRepository.Update(retrievedUser);
        }

        // Delete the user
        userRepository.Delete(newUser);

        // User no longer exists in the repository
        var nonExistentUser = userRepository.GetById(1);
        if (nonExistentUser == null)
        {
            Console.WriteLine("User with ID 1 not found.");
        }
    }
}
```