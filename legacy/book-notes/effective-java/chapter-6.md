# Chapter 6 - Enums and Annotations

34. Use enums instead of int constants
    - `switch` statements are dangerous, avoid them as much as possible.

35. Use instance fields instead of ordinals

36. Use `EnumSet` instead of bit fields

37. Use `EnumMap` instead of ordinal indexing
    ```java 
    // Naive stream-based approach - unlikely to produce an EnumMap! 
    System.out.println(Arrays.stream(garden)
        .collect(groupingBy(p -> p.lifeCycle)));
    
    // Using a stream and an EnumMap to associate data with an enum
    System.out.println(Arrays.stream(garden)
        .collect(groupingBy(p -> p.lifeCycle,
            () -> new EnumMap<>(LifeCycle.class), toSet())));
    ```

38. Emulate extensible enums with interfaces

39. Prefer annotations to naming patterns

40. Consistently use `@Override` annotation.

41. Use marker interfaces to define types
