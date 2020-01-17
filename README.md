# cc2020_cl_cam_ac_uk

## Potential improvments


Compiler Construction 2020
Computer Laboratory 
University of Cambridge 
Timothy G. Griffin (tgg22@cam.ac.uk) 

There are many possible extensions or modifications 
possible for the Slang interpreters.  Here are just 
a few ideas. They are listed from easiest to hardest, 
more or less. 

Note: only changes to the Jargon version of the 
the compiler need to be done. That is, changes
don't have to be pushed through all of the 
intermediate interpreters.  However, I will 
not except changes in github unless all of the 
code compiles... 

1. Write some interesting slang examples. Run the 
  interpreters on them and try to understand 
  the verbose output. 

1. Add division to the arithmetic operations. How will 
  you handle division by zero? 

3. Modify lexer to handle nested comments. 

4. Improve the concrete syntax of Slang 
  by changing the parser.  Also see if you can make 
  some of the type annotations optional. 

5. Implement simple "tuple pattern matching" in the compiler. 
  
For example, instead of writing 

     let rev (p : int * int) : int * int  = (snd p, fst p) 
     in 
        rev (21, 17) 
     end 

  allow users to write 

     let rev (x : int, y : int) : int * int  = (y, x) 
     in 
        rev (21, 17) 
     end 

### Hint : treat this as syntax sugar -- eliminate in front end by translating the second rev into the first. Or better yet, intro let bindings for "snd p" and "fst p". 

6. Implement simple optimisations : 
    --- peephole 
    --- inline expansion 
    --- constant folding 

7. Improve lets 

The current compiler translates let-bindings as 

    let x = e1 in e2 end   --->    (fun x -> e2 end)e1 

  This was nice in that we only had one form of abstraction 
  to worry about. But it is not very efficient for most code. 
  Imagine a function defined as 

  fun f(x) = 
    let x1 = e1 in 
    let x2 = e2 in 
    ... 
    let xk = ek in 
      e 
    end ... end 

  Work through how many closures get created an how things 
  are computed at runtime. Arg!  What to do? 
  Hint : put the values of these "local variables" 
  in the stack frame of f! If the arg x to f is "below" the 
  control entries (return address, pointer to f, saved frame 
  pointer), then push the values of the x_i "above" 
  the control entries.  You can now find their values by 
  an index off of the current frame pointer.  Now compare 
  the runtime of this implementation with the 
  closure-based approach ... 

8. Add mutual recursion to Slang1.  Such as 

    let g(x : int) : int = ... f(e) ... 
    and f(z :int) : int  = .... g(e') ... 
    in ... end 

   This requires careful treatment of environments! 

9. Generate ARM assembler from Jargon Machine code. 

10. Generate RISC-V assembler from Jargon Machine code. 

11. Add objects to SLang 

12. Implement a garbage collector for the Jargon VM.  

13. Implement elimination of tail-recursion in the compiler. 

14. Implement Objects in Slang. 

15. Implement exceptions in Slang. 

16. We have blurred the distinction between the defining 
  language (OCaml) and the defined language (Slang) 
  in several ways.  For example, Slang integers are 
  the ints supplied by OCaml on your machine. Now 
  suppose that Slang only allows 16-bit integers, 
  where overflow or underflow should raise a 
  run-time error.  Can you modify the implementation 
  to match this? Are there additional build-in functions 
  that you might want to add to such a language? 

17. Translate Jargon.listing into Java VM code. 
     
     
