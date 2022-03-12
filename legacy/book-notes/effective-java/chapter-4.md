# Chapter 4 - Classed and Interfaces

15. Minimize the accessibility of classes and members
    - Make classes and member as inaccessible as possible
    - No public mutable fields
    - No static final array field, as arrays are always mutable. 
    Use a public getter and private backing field, instead.

16. In public classes, use accessor methods, not public fields
    - Using public fields in public classes violates encapsulation.
    - If class is package-private or private nested, it can expose fields.

17. Minimize mutability

18. Favor composition over inheritance
    - Inheritance violates encapsulation as a change in super class may break subclasses.
    - Prefer using composition with a forwarding class if a proper interface exist for super class.
    For example, instead of subclassing `HashSet` to extend its behaviour, 
    create a `ForwardingSet` that references a `HashSet` and **implements** `Set` 
    interface and then **extend** it in your subclass.

19. Design and document for inheritance or else prohibit it
    - If there is an interface capturing the essence of a class, use wrapper pattern insted of subclassing.
    - If you have to make a concrete class inheritable, extract private helper method 
    for each overrideable method. By this way, both super class and subclasses can 
    reuse some code and super class can rely on them since they cannot be overridden by subclasses.

20. Prefer interfaces over abstract classes

21. Design interfaces for posterity
22. Use interfaces to only define types
    - Do not use interfaces for static constants. Use classes or enums.

23. Prefer class hierarchies over tagged classes

24. Favor static member classes over nonstatic

25. Limit source files to single top level class
