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

### PHP - Deal with Memory Gently using `Yield`

Look at this example:
* Without using `yield`
```
<?php
function getValues() {
   $valuesArray = [];
   // get the initial memory usage
   echo round(memory_get_usage() / 1024 / 1024, 2) . ' MB' . PHP_EOL;
   for ($i = 1; $i < 800000; $i++) {
      $valuesArray[] = $i;
      // let us do profiling, so we measure the memory usage
      if (($i % 200000) == 0) {
         // get memory usage in megabytes
         echo round(memory_get_usage() / 1024 / 1024, 2) . ' MB'. PHP_EOL;
      }
   }
   return $valuesArray;
}
$myValues = getValues(); // building the array here once we call the function
foreach ($myValues as $value) {}
```
Output :
```
0.34 MB
8.35 MB
16.35 MB
32.35 MB
```

* Using `yield`
```
<?php
function getValues() {
   // get the initial memory usage
   echo round(memory_get_usage() / 1024 / 1024, 2) . ' MB' . PHP_EOL;
   for ($i = 1; $i < 800000; $i++) {
      yield $i;
      // let us do profiling, so we measure the memory usage
      if (($i % 200000) == 0) {
         // get memory usage in megabytes
         echo round(memory_get_usage() / 1024 / 1024, 2) . ' MB'. PHP_EOL;
      }
   }
}
```
Output:
```
0.34 MB
0.34 MB
0.34 MB
0.34 MB
```
* Reference: https://medium.com/tech-tajawal/use-memory-gently-with-yield-in-php-7e62e2480b8d
