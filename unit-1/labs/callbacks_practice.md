# Callbacks Practice

### Exercise: callback me maybe

1. create a function called `telephone` that logs "867-5309" when called.
2. write a separate function called `blondie` that takes a callback function as a parameter and executes it.
3. `blondie` should log "call me on the line at " when called, and then execute `telephone`.

### Exercise: repeater

1. Create a function called `repeater` that takes an integer and a string as arguments.
2. When called, the function should log the string to the console as many times as indicated by the integer.
3. Write a separate function called `repeaterSetUp` that takes an integer, a string, and a callback function as arguments.
4. When called, `repeaterSetUp` should log "HERE WE GO" to the console, and then pass the integer and string to the callback function passed to it, which then executes.
5. Run `repeaterSetUp` with `repeater` as the callback function, so if `repeaterSetUp` is passed 3 and "oi!", the terminal should print: 

```
HERE WE GO
oi!
oi!
oi!
```
