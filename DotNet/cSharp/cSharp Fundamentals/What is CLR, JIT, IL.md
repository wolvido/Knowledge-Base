keywords:
	# IL code  
	# CIL code  
	# MSIL code  
	# purpose of IL, CIL, MSIL  
	# how do code become cross platform

When compiling the source code, it becomes the Intermediate language (IL) code.  
source code ---compiling---> IL code  
  
CLR(Common Language Runtime) translates the IL code into machine code in a process called Just In Time Compiling (JIT).  
source code ---compiling---> IL code ---CLR-JIT---> machine code  
  
The purpose of IL is runtime efficiency, IL is faster to translate into a certain machine code because it is much closer to a machine code than a source code. Translating source code into machine code will be much slower and runtime will suffer, so runtime is reduced at the cost of increased compiling time by packaging the source code into IL. IL is what gets distributed, the CLR translates IL into a certain machine code much faster.
Its a tradeoff between compile time and runtime, runtime is much more important.

There is also DLR(Dynamic Runtime Language) it sits on top of CLR and handles dynamic for C#.