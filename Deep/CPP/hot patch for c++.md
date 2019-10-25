# hot patch for c++

A good article for this topic : [hot patch](https://blogs.msdn.microsoft.com/freik/2006/03/07/what-does-hot-patchability-mean-and-what-is-it-for/)

**When generate the code for funtions**:
- First,all functions must start with a 2 byte (or larger) instruction.
- Second, all functions must be preceded by 6 bytes of padding.

**When do hot patch**:
- 1.Pause the process and load your hot patch dll into the address space
- 2.Write the 6 bytes JMP [PC-relative scratch space] into the 6 bytes of padding before the function you're trying to replace
- 3.Write the 2 bytes jmp PC-6into the first two bytes of your function.

