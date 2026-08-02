# Call Stacks

When calling a function, the system sets aside space in memory for that function to do its necessary work.

Such chunks of memory are often called as **stack frames** or **function frames**.

More than one function's stack frame can exist in memory at a given time.
If `main()` calls `move()`, which then calls `direction()`, then all three functioncs have open frames.

These frames are arranged in a **stack**. The frame for the most-recently called function is always on top of the stack.

When a new function is called a new frame is **pushed** onto the top of the stack and becomes the **active frame**

When a function finishes its work, its frame is **popped** off of the stack, enabling the frame directly below to become the new, active function on top of the stack. This function pick up immediately where it left off.

