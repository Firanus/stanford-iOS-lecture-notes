# Lecture 3, Part 3: Tuples

Tuples are just groupings of types. You can use them anywhere you can use a type. You can name the elements when *accessing* the tuple e.g.

```Swift
let x: (String, Int, Double) = ("hello", 5, 0.85) //The type of x is "a tuple"
let (word, number value) = x //This names the tuple elements when accessing the elements
print(word) //prints hello
print(number) //prints 5
print(value) //prints 0.85 
```
or when you're *declaring* the tuple (which is strongly preferred). You can even then rename the elements e.g.

```Swift
let x: (w: String, i: Int, v: Double) = ("hello", 5, 0.85)
print(x.w) //prints hello
print(x.i) //prints 5
print(x.v) //prints 0.85
let (wrd, num, val) = x //This is legal and renames the tuple's elements on access
```
### Tuples as Return Values

You can use tuples to return multiple values from functions, e.g. 
```Swift
func getSize() -> (weight: Double, height: Double) { return (250,80) }
```

[Previous Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%202%20-%20Ranges.md) | [Back To Contents](https://github.com/Firanus/stanford-iOS-lecture-notes) |  [Next Note](../Lecture%203%20-%20The%20Swift%20Programming%20Language/Part%204%20-%20Computed%20Values.md)