We start from scratch, gradually introducing more advanced packages.
## R Basics
R is an interpreted language (NOT compiled).
A vector is made by items of the same type.
But if the vector is mixed, it will be upcasted to the more generic type of the vector.
An integer is more generic than a bool, a string is more generic than an integer.
*Vectors are 1-based.*
In `[4:10]` he end position is included.

*Named vectors* are like dictionaries in python. But they can be accessed both with keys and indexes.
```R
> # named vectors 
> x <- c(red="Huey", blue="Dewey", green="Louie") 
> x["red"]
   red 
"Huey" 
> x[1]
   red 
"Huey" 
> x
    red    blue   green 
 "Huey" "Dewey" "Louie" 
> names(x)
[1] "red"   "blue"  "green"
> unname(x) # vector without names
[1] "Huey"  "Dewey" "Louie"
> names(x) = c() # discard names
> x
[1] "Huey"  "Dewey" "Louie"
> names(x) = c("first", "second", "third")
> x
  first  second   third 
 "Huey" "Dewey" "Louie" 
```


