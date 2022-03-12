# Chapter 3 - Methods common to all objects

10. Obey the general contract when overriding `equals`
    - Try to avoid overriding `equals`.
        - Each instance of the class is inherently unique.
        - There is no need for the class to provide a “logical equality” test.
        - A super class has already overridden `equals`, and the super class 
        behavior is appropriate for this class.
        - The class is private or package private and it's `equals` method will 
        never be invoked.
    - The equals method implements an equivalence relation, which has these properties:
        - Reflexive
        - Symmetric
            ```java
            // Broken - violates symmetry!
            public final class CaseInsensitiveString {
                private final String s;

                public CaseInsensitiveString(String s) {
                    this.s = Objects.requireNonNull(s);
                }

                // Broken - violates symmetry!
                @Override
                public boolean equals(Object o) {
                    if (o instanceof CaseInsensitiveString)
                        return s.equalsIgnoreCase(((CaseInsensitiveString) o).s);
                    if (o instanceof String) // One-way interoperability!
                        return s.equalsIgnoreCase((String) o);
                    return false;
                }
            }
            ```
        - Transitive
        - Consistent for successive invokes
        - For any non-null reference value `x,x.equals(null)` must return false.
    - Recipe for a high-quality equals method
        - Use the == operator to check if the argument is a reference to this object.
        - Use the instanceof operator to check if the argument has the correct type. 
        If not, return false. Typically, the correct type is the class in which 
        the method occurs. Occasionally, it is some interface implemented by this 
        class. Use an interface if the class implements an interface that refines 
        the equals contract to permit comparisons across classes that implement the interface. 
        Collection interfaces such as Set, List, Map, and Map.Entry have this property.
        - Cast the argument to the correct type.
        - For each “significant” field in the class, check if that field of 
        the argument matches the corresponding field of this object.
        ```java
        // Class with a typical equals method
        public final class PhoneNumber {
            private final short areaCode, prefix, lineNum;

            public PhoneNumber(int areaCode, int prefix, int lineNum) {
                this.areaCode = rangeCheck(areaCode, 999, "area code");
                this.prefix = rangeCheck(prefix, 999, "prefix");
                this.lineNum = rangeCheck(lineNum, 9999, "line num");
            }

            private static short rangeCheck(int val, int max, String arg) {
                if (val < 0 || val > max)
                    throw new IllegalArgumentException(arg + ": " + val);
                return (short) val;
            }

            @Override
            public boolean equals(Object o) {
                if (o == this)
                    return true;
                if (!(o instanceof PhoneNumber))
                    return false;
                PhoneNumber pn = (PhoneNumber) o;
                return pn.lineNum == lineNum && pn.prefix == prefix 
                        && pn.areaCode == areaCode;
            }
        }
        ```
11. Always override `hashCode` when you override equals.
    - Do not be tempted to exclude significant fields from the hash code 
    computation to improve performance. 
    - If you have a bona fide need for hash functions less likely to produce collisions, 
    see Guava’s com.google.common.hash.Hashing [Guava].
12. Always override to `String`
13. Override clone judiciously
    - Like a constructor, a clone method must never invoke an overridable method on the clone under construction.
14. Consider implementing `Comparable`
    - Use static `compare` method instead of `<` or `>` operators.
    - Construct a comparator object as static final field instead of creating it every time.
    - Do not use difference-based comparison.
