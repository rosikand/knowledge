---
categories: [advanced, debugging]
---

# PDB: Pythin Debugger 

Similar to GDB, Python has a built-in debugger module that allows you to set breakpoints during execution. 

## How to use 

1. `import pdb`
2. Type `pdb.set_trace()` at your breakpoint. 
3. Run as usual. 
4. Use `n` (next) ([or](https://docs.python.org/3/library/pdb.html) `s` (step)) to go to the next line. Use `c` (continue) to go to the next breakpoint. See [here](https://docs.python.org/3/library/pdb.html) for more details. 

