CS 102 C++ Debugging Workflow
====================
If you run into common trouble in your PAs or labs, give these strategies a try before you ask for help on a GitHub issue.

If you use this guide and still can't figure out what's wrong, you can ask for help. However, we want to see you've tried to figure it out first yourself, so please show how you've tried to:

+ **Understand the issue**
+ **Find where the error is happening**
+ **Fix the issue**
	
	
These steps are outlined below for a variety of common C++ programming issues.



Segmentation Faults
------

+ **Understand the issue**
	+ Segmentation faults occur when you try to access an area of memory you do not have permission to access. This can happen for a variety of reasons:
		+ A pointer you tried to _dereference_ (meaning you tried to access the memory at the location pointed to by the pointer, either with the `->` operator or `(*ptr).` notation) was `NULL`. This means you tried to access the memory at address location `0x00...0`, which is protected. 
		+ A pointer you tried to _dereference_ was outside of the memory your process has been allowed to modify. This might happen if you go past the end of an array you allocated with `malloc` or `new`, for instance.
+ **Find where the error is happening**
	+ Using `gdb` or another debugger, find the line number where the error is occuring. Print the value of the pointer(s) you are dereferencing at that line to see if any of them are `NULL`. 
	+ If the line is in a loop, check the loop conditions to see if they iterate further than they should (past the bounds of an array, for example).
+ **Fix the issue**
	+ Once you know which pointer is misbehaving, find out why. Check places where you might have:
		+ Changed the value of the pointer unintentionally/erroneously
		+ Passed the value to a function that might have modified the value of the pointer
		+ Left a pointer uninitialized (e.g.: you declared the pointer `int ptr` but never set it to anything)


Double Free Errors
------------
+ **Understand the issue**
	+ These errors are messy looking on the terminal, but don't be scared away by them. These types of errors often occur when you try to `free` (i.e.: deallocate) the memory pointed to by a pointer that has already been freed once already. 
+ **Find where the error is happening**
	+ When `free` is called on a pointer, the destructor(s) of the object(s) being pointed to is (are) called. A good strategy is to put a breakpoint in the destructor of the class being destroyed at the line where the memory error is occurring. Once again, `gdb` is a good tool here. You will probably find that your code calls the destructor for your object(s) earlier than expected. Printing a backtrace where the memory issue occurs will show you which methods were called to cause the issue. 
+ **Fix the issue**
	+ Hint: Destructors are called on passed-by-value objects. 
	+ Hint: What can you do to the value of pointers after calling `free` on them in the future to make it clear that they are no longer valid?
	

Infinite Loops
----------
+ **Understand the issue**
	+ Loops need valid end conditions, otherwise they will run forever (and potentially crash). If you are running your code and it seems to 'hang' for a really long time, it may be stuck in an infinite loop.
+ **Find where the error is happening**
	+ Print statements (i.e.: `cout << "Looping at line 53... iteration #"<<i<<endl;` for a `for` loop on `int i`) are often a quick indicator for these errors, since a print statement in an infinite loop will be fairly obvious on the terminal. `gdb` can also be used here, though, and is more useful if the fix isn't immediately obvious. You can `print` the value of your loop variables/terminal conditions after each iteration to see if their values are what you expect them to be.
+ **Fix the issue**
	+ It's hard to guess what your issue is, but it may be that:
		+ You have a while loop with an expression that always evaluates to `true`
		+ Your `for` loop is changing the value of the iteration variable (e.g. `i` in `for(int i=0;...;...)` is being changed inside the loop erroneously)
	+ Once you've pinpointed the problem loop, use `gdb` to inspect the value of the terminal conditions on each iteration, and make sure it's what you expect.

Submitting an Issue
---------
Before you submit an issue, demonstrate that you have attempted to solve the problem yourself. This means when you create an issue you should supply:

    + The line number where the error is occuring.
    + The steps you have taken to diagnose the problem. This is particularly important because it gives the staff a starting point when examining the issue. 
    + The point where you believe the error is, and why you don't understand what is happening.
