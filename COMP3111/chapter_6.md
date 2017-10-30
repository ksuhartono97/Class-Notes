# Debugging

## First Defense
The error is impossible by design of the programming language. The compiler throws errors that tell you it doesn't work.  

## Second Defense
Correctness of the code, think about the code first before you code to solve the bugs.

## Regression Testing
Whenever you find a bug make a testcase for it in a regression testing folder, so that your program is secure from these bugs.

## Logging
Log stuff happening so you have a better idea of what is going on

## Debugging
Is a last resort, eventually you'll have to do it. An industry average is 10 bugs per 1000 lines of code.

Binary search on a buggy code is a good way to debug code.

Ways to debug:
- Try to think whether bug is where you think it is (explain why bug might not be there)
- Check for stupid mistakes:
  - Order of arguments
  - Spelling
  - Same object vs equal (a.equals(b) or a == b)
  - Deep vs shallow copying

## CMD debugging tool
`gdb` is a standard debugging tool.

- First you open the file with `gdb <file>`
- Then you can run `gdb run`
- It will stop at breakpoints that you've defined.

 
