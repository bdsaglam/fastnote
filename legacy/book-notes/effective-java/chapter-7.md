# Chapter 7 - Lambdas and Streams

42. Prefer lambdas to anonymous classes
    - Omit the types of all lambda parameters unless their presence makes your program clearer.
    - Lambdas lack names and documentation; if a computation isn’t 
    self-explanatory, or exceeds a few lines, don’t put it in a lambda.
    
43. Prefer method references to lambdas
    ```java
    // lambda
    map.merge(key, 1, (count, incr) -> count + incr);

    // static method reference
    map.merge(key, 1, Integer::sum);
    ```

44. Favor the use of standard functional interfaces
    ```java
    // Unnecessary functional interface; use a standard one instead.
    @FunctionalInterface interface EldestEntryRemovalFunction<K,V>{ 
        boolean remove(Map<K,V> map, Map.Entry<K,V> eldest);
    }
    ```

    | Interface      	| Function Signature  	|
    |----------------	|---------------------	|
    | UnaryOperator 	| `T apply(T t)`    	|
    | BinaryOperator 	| `T apply(T t1, T t2)` |
    | Predicate      	| `boolean test(T t)`   |
    | Function       	| `R apply(T t)`        |
    | Supplier       	| `T get()`             |
    | Consumer       	| `void accept(T t)`    |
    | ...       	    | ...                   |

    - Don’t be tempted to use basic functional interfaces with boxed primitives 
    instead of primitive functional interfaces.
    - Prefer custom interfaces over standard functional interfaces, for example, 
    `Comparator<T>` vs `ToIntBiFunction<T, T>`, when:
        - It will be commonly used and could benefit from a descriptive name. 
        - It has a strong contract associated with it.
        - It would benefit from custom default methods.
    - Always annotate your functional interfaces with the `@FunctionalInterface` annotation.

45. Use streams judiciously
    - Overusing streams makes programs hard to read and maintain.
    - In the absence of explicit types, careful naming of lambda parameters is 
    essential to the readability of stream pipelines.
    - Using helper methods is even more important for readability in stream pipelines than in iterative code.
    - Refrain from using streams to process char values.

46. Prefer side-effect free functions in streams
    - It is customary and wise to statically import all members of Collectors 
    because it makes stream pipelines more readable.

47. Prefer Collection over stream as a return type

48. Use caution when making streams parallel
    - Parallelizing a pipeline is unlikely to increase its performance 
    if the source is from Stream.iterate, or the intermediate operation limit is used. 
    - Performance gains from parallelism are best on streams over 
    ArrayList, HashMap, HashSet, and ConcurrentHashMap instances; arrays; 
    int ranges; and long ranges.
