GDB Workflow
=============

To compile a program with debugger symbols, use the -g flag when you compile. For programs with a Makefile, we'll include it for you.

Once that is done you can debug the program. The command to run gdb is 
`gdb EXECUTABLE_NAME`

Here you can run the executable using by entering `run` or `r`. If you need to add commandline arguments, you can add them when you run the executable. For example:
`run ARG_1 ARG_2 ...`

If your program has a segfault gdb will halt and let you know that you have hit an error. 
When the program stops, there are a couple commands that might be helpful.
+ `backtrace` or `bt` will print the stack trace; this will show you the functions that have been called up to the point of the crash.
+ `print VARIABLE_NAME` will print the value of a given variable name. This can be used to see what value is incorrect and is usually a good point to start looking for bugs.

It is also useful to stop the execution of your program at an arbritary point. This can be accomplished by setting breakpoints. To set a breakpoint, use the `break` command. The break requires a line number to be specified, and if there are multiple source files, you must specify that too. For example:
+ `break 10`
+ `break sourcefile.cpp:10`

Once you hit a breakpoint, you can use the `print` and `backtrace` commands. To proceed with program execution, there are two commands you can use.
+ `continue` or `c` to run the program until it encounters the next breakpoint or the end of execution.
+ `step` or `s` to step through the the program line by line.

To delete a breakpoint
`delete BREAKPOINT_NUMBER`

To list all breakpoints
`info breakpoints`