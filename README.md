# Interfacing In C
Explanations, diagrams, and examples of interfacing in C in different ways

Interfaces allow code referencing the interface to work regardless of the implementation so long as the different implementations are consistent. 

# Link Time interfacing
The same function names and symbols are defined in multiple different files. 

**Only one set of definitions can be used per link target.**

The immediate example is `int main(int argc, char* argv[]);`, which must be defined for every executable with only one implementation being valid for a given link target.

A more meaningful example is `fopen`, `fread`, `fwrite`, `fclose`, `FILE*`, etc. There is a definition of these functions and symbols in each variant of the standard c libraries for `linux`, `mac`, and `windows` among others. 
The implementations vary widely as they must utilize system calls unique to their operating system, but at the interface level they function the same.

# 
