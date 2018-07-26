# Fundamental theories and tips

## Fundamental theories

### SOLID

#### Single responsibility principle
`A class should have only a single responsibility (i.e. changes to only one part of the software's specification should be able to affect the specification of the class).`
#### Open/closed principle
`"software entities … should be open for extension, but closed for modification."`
#### Liskov substitution principle
`"objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program." See also design by contract.`
#### Interface segregation principle
`"many client-specific interfaces are better than one general-purpose interface."`
#### Dependency inversion principle
`one should "depend upon abstractions, [not] concretions."`

## Tips

### Avoiding == Versus = Confusion
##### Solution
Use: `if (12 == $dwarves) { ... }`

instead of : `if ($dwarves == 12) { ... }`
Assigning 12 to the variable `$dwarves`: `$dwarves = 12` always return `true` while `12 = $dwarves` causes error when compiling.
