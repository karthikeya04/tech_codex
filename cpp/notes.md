# C++ Notes
TODO Add https://docs.google.com/document/d/1Cjjr6838O12L25kyg0QO6unilZ01XCSJwojVY1r38wE/

## Operators and Functions
- Philosophically the same
- Can provide a return value and perform side effects
    - x = 5; here the operator = returns a reference to x with the side effect that x is updated to 5
    - No point in defining a function with a void return type with no side effects

## Namespaces
- Can only be declared in the global scope or inside other namespaces

## Scope, Duration and Linkage
- Scope and Linkage are for identifiers which in this context refer to functions, variables and type definitions 
    - By type definitions I refer to Classes, Structs and Enums
    - TODO what is the behaviour for typedefs?
- Duration is for variables

Scope
- Where the identifier can be accessed
- There are two types
	- Block scope
		- Accessible from point of declaration to end of the block
		- Ex: Local vars, Function params, Local type definitions 
	- Global scope
		- Accessible from point of declaration to end of the file(the translation unit)
			- Global vars and type definitions, functions
                - Global => outside of any blocks, namespaces are only for identifier resolution

Duration (Storage duration)
- When the variable is created and destroyed
- There are three types
    - Automatic
        - [Point of declaration, Exiting the block]
        - local variables, function params
    - Static
        - [Program begin, Program end]
            - TODO Have to be more specific than this, there's literature available
        - global variables, static local variables
    - Dynamic
        - under Programmer control
            - [malloc, free], [new, delete], [new [], delete []] etc.
- thread\_local is a relevant keyword for this

Linkage
- Whether the declaration of the same identifier in different translation units is linked to a single definition
- There are three types
    - No linkage
        - Do not participate in the linking process
        - Local variables, Local type definitions
    - Internal linkage
        - Limited to the translation unit only
        - Examples
            - const global variables declared without the extern keyword
            - identifiers defined within anonymous namespaces
            - non-const global variables and functions defined with the static keyword
    - External linkage
        - Unified to one definition across all translation units (ODR Rule)
        - Examples
            - Global type definitions
            - Functions (External by default)
            - Non-const global variables (External by default)
            - Const global variables declared with the extern keyword
        - constexpr variables cannot be externally linked
            - Because they are not available when compiling the translation units
            - Can be defined as constexpr but forward declared elsewhere as const for linking if needed
                - But constexpr advantage is lost in such translation units

- extern and inline are two relevant keywords for this

Storage class specifier
- As part of the declaration, these set the storage duration and the linkage
- extern, static, thread\_local and mutable
    - Not sure why mutable is treated as a storage class specifier TODO

## Keywords
### extern
- TODO https://www.learncpp.com/cpp-tutorial/external-linkage-and-variable-forward-declarations/
- TODO as a storage class specifier extern => static (or thread\_local) storage duration and external linkage

### static
- TODO In classes
- TODO In Block scope
- TODO In Global scope
   - static (or thread\_local) storage duration and internal linkage 

### thread\_local
- TODO What is this?
- TODO `thread storage duration`

### mutable
- TODO https://stackoverflow.com/questions/105014/does-the-mutable-keyword-have-any-purpose-other-than-allowing-a-data-member-to

### inline
- TODO For functions
- TODO For variables, Circumventing the ODR issues for static data member needing to be defined in a seperate file and header only libraries with global variable
