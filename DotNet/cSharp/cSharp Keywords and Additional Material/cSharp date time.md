#cSharp 
syntax:  
```c#
// 2015 is year, 12 is month, 25 is day  
DateTime date1 = new DateTime(2015, 12, 25); // 12/25/2015 12:00:00 AM  

// 2015 - year, 12 - month, 25 – day, 10 – hour, 30 – minute, 50 - second  
DateTime date2 = new DateTime(2012, 12, 25, 10, 30, 50);// 12/25/2015 10:30:00 AM }  
```
  
```c#
var now = DateTime.Now;  
now.Hour //returns the current hour only no minutes  
now.Minutes //returns the minutes  
```
  
its immutable, so to modify you use its methods and assign a new variable or re-initialize to the same ex:  
```c#
var tomorrow = now.AddDays(1) //returns tomorrow time  
var yesterday = now.AddDays(-1) //returns yesterday time  
```
  
if you want to specify the format use:  
```c#
now.ToString("MM/dd/yyyy") //returns 05/29/2015  
now.ToString("dddd, dd MMMM yyyy") //returns Friday, 29 May 2015  
now.ToString("HH:mm") //returns 05:50  
```
  
note: you can edit it to anything, you can replace : or / with any character like:  
```c#
now.ToString("HHxyzmm") //returns 05xyz50  
```
  
you can create any format using the components below:  
  
- d -> Represents the day of the month as a number from 1 through 31.  
- dd -> Represents the day of the month as a number from 01 through 31.  
- ddd-> Represents the abbreviated name of the day (Mon, Tues, Wed, etc).  
- dddd-> Represents the full name of the day (Monday, Tuesday, etc).  
- h-> 12-hour clock hour (e.g. 4).  
- hh-> 12-hour clock, with a leading 0 (e.g. 06)  
- H-> 24-hour clock hour (e.g. 15)  
- HH-> 24-hour clock hour, with a leading 0 (e.g. 22)  
- m-> Minutes  
- mm-> Minutes with a leading zero  
- M-> Month number(eg.3)  
- MM-> Month number with leading zero(eg.04)  
- MMM-> Abbreviated Month Name (e.g. Dec)  
- MMMM-> Full month name (e.g. December)  
- s-> Seconds  
- ss-> Seconds with leading zero  
- t-> Abbreviated AM / PM (e.g. A or P)  
- tt-> AM / PM (e.g. AM or PM  
- y-> Year, no leading zero (e.g. 2015 would be 15)  
- yy-> Year, leading zero (e.g. 2015 would be 015)  
- yyy-> Year, (e.g. 2015)  
- yyyy-> Year, (e.g. 2015)  
- K-> Represents the time zone information of a date and time value (e.g. +05:00)  
- z-> With DateTime values represents the signed offset of the local operating system's time zone from  
- Coordinated Universal Time (UTC), measured in hours. (e.g. +6)  
- zz-> As z, but with leading zero (e.g. +06)  
- zzz-> With DateTime values represents the signed offset of the local operating system's time zone from UTC, measured in hours and minutes. (e.g. +06:00)  
- f-> Represents the most significant digit of the seconds' fraction; that is, it represents the tenths of a second in a date and time value.  
- ff-> Represents the two most significant digits of the seconds' fraction in date and time  
- fff-> Represents the three most significant digits of the seconds' fraction; that is, it represents the milliseconds in a date and time value.  
- ffff-> Represents the four most significant digits of the seconds' fraction; that is, it represents the ten-thousandths of a second in a date and time value. While it is possible to display the ten-thousandths of a second component of a time value, that value may not be meaningful.  
- fffff-> Represents the five most significant digits of the seconds' fraction; that is, it represents the hundred-thousandths of a second in a date and time value.  
- ffffff-> Represents the six most significant digits of the seconds' fraction; that is, it represents the millionths of a second in a date and time value.  
- fffffff-> Represents the seven most significant digits of the second's fraction;