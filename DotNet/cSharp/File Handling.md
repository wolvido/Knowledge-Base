#cSharp 
File handling is in Namespace System.IO.
Namespace System.IO 
	Classes:
		- File, FileInfo
		- Directory, DirectoryInfo
		- Path
		there also many classes but these are the most common. Its impossible to know all classes in dotnet

The most common classes used in File Handling is  File, FileInfo | Directory, DirectoryInfo | Path. The methods are self explanatory

FileInfo: provides instance methods
File: provides static methods
DirectoryInfo: same as Fileinfo
Directory: same as file
if youre confused about static vs instance see: [[purpose of static]]
Difference is, using static methods is slower than instance, since the OS will have to do security checking every time static is called, in instance methods you check once and run again and again until object is closed.
# Most Common Uses in File Handling
## File, FileInfo
- Create()
- Copy()
- Delete()
- Exist()
- GetAttributes()
- Move()
- ReadAllText()
## Directory, DirectoryInfo
  - CreateDirectory()
  - Delete()
  - Exists()
  - GetCurrentDirectory()
  - GetFiles()
  - Move()
  - GetLogicalDrives()
## Path
- GetDirectoryName()
- GetFileName()
- GetExtension()
- GetTempPath()

sample use:
```c#
class Program
{
    static void Main()
    {
        string filePath = "sample.txt";
        string destinationPath = "copy.txt";
        
        // Using File class
        File.WriteAllText(filePath, "Hello, World!");
        string contents = File.ReadAllText(filePath);
        Console.WriteLine(contents);
        File.Copy(filePath, destinationPath);
        File.Delete(filePath);
        
        // Using FileInfo class
        FileInfo fileInfo = new FileInfo(filePath);
        if (fileInfo.Exists)
        {
            long fileSize = fileInfo.Length;
            DateTime lastModified = fileInfo.LastWriteTime;
        }
        
        string newFilePath = "newfile.txt";
        fileInfo.MoveTo(newFilePath);
        
        using (FileStream fileStream = fileInfo.OpenRead())
        {
            // Read data from the file stream if needed
        }
    }
}
```

There is also Filestream, a more specialized Class in System.IO. Most of the time File will suffice since File and FileInfo uses FileStream, but for large files, you might want to use FileStream.