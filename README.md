# Interfacing In C
Explanations, diagrams, and examples of interfacing in C in different ways

Interfaces allow code referencing the interface to work regardless of the implementation so long as the different implementations are consistent. 

# Singleton Link Time interfacing
The same function names and symbols are defined in multiple different files. 

**Only one set of definitions can be used per link target.**

The immediate example is `int main(int argc, char* argv[]);`, which must be defined for every executable with only one implementation being valid for a given link target.

A more meaningful example is `fopen`, `fread`, `fwrite`, `fclose`, `FILE*`, etc. There is a definition of these functions and symbols in each variant of the standard c libraries for `linux`, `mac`, and `windows` among others. 
The implementations vary widely as they must utilize system calls unique to their operating system, but at the interface level they function the same.

# Singleton Run Time interfacing
Similar to `Singleton Link Time Interfacing`, a single set of definitions can be utilized per execution.

Rather than defining the exact same symbols multiple times, a global set of function pointers is populated from a decision made at run time, however there can be multiple different sets of valid definitions for the interface within a link target. 

One example of this, though not necessarily a c example, is the command line options used for commands like `tar` or `git`. 

`tar -cf` and `tar -xf` function entirely differently because they define different implementations for the entrypoint that is actually used.

Another example of this is tools like `qemu-system-x86_64` allow you to specify a specific model of `cpu` which is used for the duration of the execution. 

# Static Multi-instance interfacing 
If you want to utilize multiple instances of an interface during execution and don't need it to be disable-able, you can use this type of interfacing. 

Multiple instances of the interface are populated and stored in some way, often in an array, before or during link-time. The array is typically not mutable after link-time. 

An example of this is the `initcall` system in the linux kernel. Different subsystems are allowed to define initialization functions and add them to the `initcall` lists. Which entries end up in the `initcall` lists is determined by whether or not the subsystem's code was compiled in at all. 
Every time the kernel boots up, it will execute all of the defined `initcall` entries.

# Dynamic Multi-instance interfacing
If you want to utilize multiple instances of an interface during execution and **do** want it to be disable-able and enable-able, you can use this type of interfacing. 

Multiple instances of the interface are populated and stored in an array or linked-list. This array or linked-list is mutable at execution time, enabling you to turn on and off specific instances of the interface.

An example of this is the `struct file_operation` handling in the linux kernel

