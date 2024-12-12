#cSharp 
Like a class but without constructor and cant inherit or be derived. It can inherit from interface though.

Typically, you use structure types to design small data-centric types that provide little or no behavior.
If you're focused on the behavior of a type, consider defining a [class](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/class).

sample uses of struct:
- Point or Vector Representation:
```c#
struct Point
{
    public int X;
    public int Y;
}
```
A `Point` struct can be used to represent coordinates in a 2D space.

- Color Representation:
```c#
struct Color
{
    public byte Red;
    public byte Green;
    public byte Blue;
}
```
 A `Color` struct can be used to represent RGB color values.
 
 - Complex Number Representation:
```c#
struct ComplexNumber
{
    public double Real;
    public double Imaginary;
}
```
A `ComplexNumber` struct can be used to represent complex numbers.

- Date and Time Representation:
```c#
struct DateTime
{
    public int Year;
    public int Month;
    public int Day;
    public int Hour;
    public int Minute;
    public int Second;
}
```
A simplified `DateTime` struct for representing date and time values.

- Currency Representation:
```c#
struct Money
{
    public decimal Amount;
    public string CurrencyCode;
}
```
A `Money` struct can be used to represent currency values.

- Immutable Configuration Settings:
```c#
struct ConfigurationSettings
{
    public readonly string SettingName;
    public readonly object SettingValue;
}
```
An `ConfigurationSettings` struct that stores immutable configuration settings.

- Geographical Coordinates:
```c#
struct GeoCoordinate
{
    public double Latitude;
    public double Longitude;
}
```
A `GeoCoordinate` struct for representing geographical coordinates.

- 2D Rectangle:
```c#
struct Rectangle
{
    public double Width;
    public double Height;
}
```
A `Rectangle` struct to represent the dimensions of a 2D rectangle.

- 3D Point in Space:
```c#
struct Point3D
{
    public double X;
    public double Y;
    public double Z;
}
```
A `Point3D` struct for representing points in 3D space.

sample use:
```c#
using System;

public struct Point
{
    public int X;
    public int Y;

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }
}

public class Program
{
    public static void Main()
    {
        // Create a Point struct
        Point point1 = new Point(10, 20);

        // Access and display the X and Y coordinates
        Console.WriteLine($"Point 1: X = {point1.X}, Y = {point1.Y}");

        // Create another Point struct
        Point point2 = new Point(5, 8);

        // Copy the value of point2 to point1 (they are independent copies)
        point1 = point2;

        // Modify point2, which doesn't affect point1
        point2.X = 100;
        point2.Y = 200;

        // Display the values of point1 and point2
        Console.WriteLine($"Point 1: X = {point1.X}, Y = {point1.Y}");
        Console.WriteLine($"Point 2: X = {point2.X}, Y = {point2.Y}");
    }
}
```