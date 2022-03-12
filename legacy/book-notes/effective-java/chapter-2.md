# Chapter 2 - Creating and Destroying Objects

1. Consider static factory methods over constructors
    - Unlike constructors, they have names.
    - Unlike constructors, they are not required to create new objects. 
    Useful for singleton and caching.
    - Greater flexibility in choosing the returned type, which can be an 
    interface instead of concrete type.
    - By convention, static factory methods for an interface named `Type` were 
    put in a noninstantiable companion class named `Types`. For example,
    `Collection` interface and `Collections` class.
    - Adhere to the common naming conventions when implementing static factory methods:
        - `from` - A type-conversion method that takes a single parameter and returns a corresponding instance of this type, for example:
            ```java
            Date d = Date.from(instant);
            ```
        - `of` - An aggregation method that takes multiple parameters and returns an instance of this type that incorporates them, for example:
            ```java
            Set<Rank> faceCards = EnumSet.of(JACK, QUEEN, KING);
            ```
        - `valueOf`—A more verbose alternative to from and of, for example:
            ```java
            BigInteger prime = BigInteger.valueOf(Integer.MAX_VALUE);
            ```
        - `instance` or `getInstance` — Returns an instance that is described by 
        its parameters (if any) but cannot be said to have the same value, for example:
            ```java
            StackWalker luke = StackWalker.getInstance(options);
            ```
        - `create` or `newInstance` — Like instance or getInstance, except that the 
        method guarantees that each call returns a new instance, for example:
            ```java
            Object newArray = Array.newInstance(classObject, arrayLen);
            ```
        - `getType` — Like `getInstance`, but used if the factory method is in a different
        class. Type is the type of object returned by the factory method, for example: 
            ```java
            FileStore fs = Files.getFileStore(path);
            ```
        - `newType` — Like `newInstance`, but used if the factory method is in a 
        different class. Type is the type of object returned by the factory method, for example:
            ```java
            BufferedReader br = Files.newBufferedReader(path);
            ```
        - `type` — A concise alternative to getType and newType, for example:
            ```java
            List<Complaint> litany = Collections.list(legacyLitany);
            ```
2. Consider a builder when faced many constructor parameters
3. Enforce the singleton property with either one of these:
    - Private constructor
    ```java
    // Singleton with static factory
    public class Elvis {
        private static final Elvis INSTANCE = new Elvis(); 
        private Elvis() { ... }
        public static Elvis getInstance() { return INSTANCE; }
        public void leaveTheBuilding() { ... } 
    }
    ```
    - Enum type if the type does not need to inherit from a super class
    ```java
    // Enum singleton - the preferred approach
    public enum Elvis {
        INSTANCE;
        public void leaveTheBuilding() { ... } 
    }
    ```
4. Enforce noninstantiability with a private constructor
5. Prefer dependency injection to hardwiring resources
6. Avoid creating unnecessary objects
    - A `String` object is reused in same JVM if it is declared with string literal.
    So it is safe to return them from a function as they are reused. 
    However, this creates a new `String` object every time, therefore, avoid it.
        ```java
        String s = new String("bikini");
        ```
    - Some objects are expensive to create.
        ```java
            // Performance can be greatly improved!
            static boolean isRomanNumeral(String s) {
                return s.matches("^(?=.)M*(C[MD]|D?C{0,3})" 
                + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");
            }
        ```
        ```java
        // Reusing expensive object for improved performance
        public class RomanNumerals {
            private static final Pattern ROMAN = Pattern.compile( "^(?=.)M*(C[MD]|D?C{0,3})"
            + "(X[CL]|L?X{0,3})(I[XV]|V?I{0,3})$");

            static boolean isRomanNumeral(String s) { 
                return ROMAN.matcher(s).matches();
            } 
        }
        ```
    - Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
        ```java
        // Hideously slow! 
        private static long sum() { 
            Long sum = 0L;
            for (long i = 0; i <= Integer.MAX_VALUE; i++) 
                sum += i; // auto-boxing occurs here
            return sum; 
        }
        ```
7. Eliminate obsolete object references
    - Null out references once they become obsolote.
    - Nulling out object references should be the exception rather than the norm. 
    Use narrowest scope possible for variables so that their references drop out automatically.
    - Whenever a class manages its own memory, the pro- grammer should be alert for memory leaks.
    - Another common sources of memory leaks are caches, listeners and other callbacks.
8. Avoid finalizers and cleaners
    - TODO: Take a look at `AutoCloseable` interface
9. Prefer try-with-resources to try-finally
