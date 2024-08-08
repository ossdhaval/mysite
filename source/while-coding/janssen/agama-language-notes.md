# Agama notes

## Data types

- there is no strict type enforcement in Agama.

- Strings: are surrounded by double quotes. Examples: "Agama", "blah", "" (empty string)

- Strings: Backslash can be used to escape chars, like "Hello\nGluu" (line feed), "Hi\u0040" (unicode character)

- Strings: Including double quotes in strings requires unicode escaping, like "\u0022". Using "\"" won't work

- Numbers are allowed, signed or unsigned
- Boolean is `true` or `false` in lower case
- Null is represented by `null`
- lists: They are finite sequences. Elements are separated by commas. Examples: [ 1, 2, 3 ], [ "bah!", "humbug" ], [ ] (empty list).
Elements of a list do not have to be of the same type
- maps: Example: { brand: "Ford", color: null, model: 1963, overhaulsIn: [ 1979, 1999 ] }. 

## Variables:

Variable names follow the pattern: [a-zA-Z]( _ | [a-zA-Z] | [0-9] )*

camelCase naming is recommended

Variables are not declared, just used freely. Variables are always global in a given flow

They can be assigned a value using the equal sign. Example: colors = [ "red", "blue" ]

They can be assigned several times in the same flow

## General notes

- flow properties vs flow inputs: Flow properties are configuration values given to the flow. Flow inputs are inputs provided by caller flow (if there are any).
- flow properties can be accessed by a variable defined by `Configs` header. 
- flow inputs are listed in the header of the flow using `Inputs`
- Note the difference between properties and inputs. Properties are parameters that callers of the flow should not control or be interested in. On the other hand, inputs are parameters that callers supply explicitly to make the flow exhibit certain behaviors.
-  Agama does not support the concept of subroutines/procedures; this is not needed because functional decomposition is carried out by calling subflows.
- Comparisons are limited to equality (is) or inequality (is not). For other forms of comparison you can resort foreign routines
- As expected and has higher priority than or when evaluating expressions. There is no way to group expressions to override the precedence: there are no parenthesis in Agama. Assigning the result of a boolean expression to a variable is not supported. These restrictions are important when writing conditionals
- Agama's Match ... to is a construct similar to C/Java switch
- Finish is used to terminate a flow's execution. A flow can finish successfully or failed
