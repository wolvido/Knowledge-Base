Class Factories are used in more complex situations where you need to decide dynamically which class to instantiate based on runtime conditions or configurations.
Sample:
```c#
using System;

// Abstract document processor
public abstract class DocumentProcessor
{
    public abstract void Process();
}

// Concrete document processors
public class PdfProcessor : DocumentProcessor
{
    public override void Process()
    {
        Console.WriteLine("Processing PDF document...");
    }
}

public class WordProcessor : DocumentProcessor
{
    public override void Process()
    {
        Console.WriteLine("Processing Word document...");
    }
}

public class ExcelProcessor : DocumentProcessor
{
    public override void Process()
    {
        Console.WriteLine("Processing Excel document...");
    }
}

// Document processor factory
public static class DocumentProcessorFactory
{
    public static DocumentProcessor CreateProcessor(string fileType)
    {
        switch (fileType.ToLower())
        {
            case "pdf":
                return new PdfProcessor();
            case "word":
                return new WordProcessor();
            case "excel":
                return new ExcelProcessor();
            default:
                throw new ArgumentException("Unsupported file type", nameof(fileType));
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        string fileType = //the result will be dynamic, it can be "pdf" or "word" or "excel".
        DocumentProcessor processor = DocumentProcessorFactory.CreateProcessor(fileType);
        processor.Process();
    }
}
```
This design creates extensibility, this will allow you to add new file types if necessary and process it dynamically. Prevents procedural design.