# Chapter 8 - Methods

49. Check parameters for validity
    - Check parameters validity in the beginning of the method
    - Use `@throws` annotation for exceptions that can be thrown when validating parameters
    - Use `Objects.requireNonNull(x)`
    - For unexported code, use assertions.

50. Make defensive copies when needed (important)
    - When receiving from client or providing to client 

51. Design method signatures carefully
    - Choose method names carefully
    - Don’t go overboard in providing convenience methods.
    - Avoid long parameter lists.
    - For parameter types, favor interfaces over classes
    - Prefer two-element enum types to boolean parameters

52. Use overloading judiciously

53. Use varargs judiciously
    - Ensure at least one element by using remaining arguments pattern
        ```java
        // The WRONG way to use varargs to pass one or more arguments!
        static int min(int... args) { 
            if (args.length == 0)
                throw new IllegalArgumentException("Too few arguments"); 
            int min = args[0];
            for (int i = 1; i < args.length; i++)
                if (args[i] < min) 
                    min = args[i];
            return min; 
        }

        // The right way to use varargs to pass one or more arguments
        static int min(int firstArg, int... remainingArgs) {
            ...
        }
        ```
    - Use overloading to avoid array allocation and initialization cost that 
    comes with varargs by implemented overloaded methods for most frequently 
    used number of arguments.
        ```java
        public void foo() { }
        public void foo(int a1) { }
        public void foo(int a1, int a2) { }
        public void foo(int a1, int a2, int a3) { }
        public void foo(int a1, int a2, int a3, int... rest) { }
        ```

54. Return empty collections or arrays, not null
    - Use `Collections.emptyList()` to avoid new allocations

55. Return optionals judiciously
    - Java `Optional` is introduced for return types, don't use them for arguments.

56. Write doc comments for all exposed API elements (important)
