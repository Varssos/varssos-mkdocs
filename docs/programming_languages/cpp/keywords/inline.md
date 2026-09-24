# Inline

[More details about inline functions](https://www.geeksforgeeks.org/inline-functions-cpp/)

C++ provides inline functions to reduce the function call overhead. An inline function is a function that is expanded in line when it is called. When the inline function is called, the whole code of the inline function gets inserted or substituted at the point of the inline function call. This substitution is performed by the C++ compiler at compile time. **Inline function may increase efficiency if it is small.**

## Syntax

```cpp
inline return-type function-name(parameters)
{
    // function code
}
```

## Compiler may not perform inlining in such circumstances like

1. If a function contains a loop (for, while, do-while)
2. If a function contains static variables
3. If a function is recursive
4. If a function return type is other than void, and the return statement doesn't exist in the function body
5. If a function contains switch or goto statement

!!! warning
    Inlining is only a request to the compiler, not a command. The compiler can ignore the request for inlining.

## Inline function advantages

1. Function call overhead doesn't occur.
2. Saves overhead to push/pop variables on the stack when function is called
3. Saves overhead of a return call from a function
4. It is able to specify compiler optimization for such inline functions

## Inline functions disadvantages

1. The added variables from the inlined function consume additional registers
2. If you use too many inline functions then the size of the binary executable file will be large, because of the duplication of code
3. Too much inlining can also reduce your instruction cache hit rate
4. Inline function may increase compile time overhead
5. Inline functions may not be useful for many embedded systems, because in embedded systems code size is more important than speed
