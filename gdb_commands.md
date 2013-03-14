GDB Workflow

To compile a program with debugger symbols, use the -g flag when you compile. For programs with a Makefile, we'll include it for you.

Once that is done you can debug the program. The command to run gdb is 
***gdb EXECUTABLE_NAME***

Here you can run the executable using by entering 'run' or 'r'.

If your program has a segfault gdb will halt and let you know that you have hit an error. 
Once you're here, there are a couple commands that might be helpful. 
+'backtrace' or 'bt' will print the stack trace; this will show you the functions that have been called up to the point of the crash.
+'print VARIABLE_NAME' will print the value of a given variable name. This can be used to see what value is incorrect and is usually a good point to start looking for bugs.