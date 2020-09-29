# Functions

Functions are ways re-using blocks of code. This tutorial has already shown you a few examples of functions, but lets look at a more complex example

```clojure
var main: fn() => {
  val := test:(1, 2, 3])
}

var test: fn(number -> a, number -> b, number -> c) => {
  return a + b + c
}
```

Now you may notice two things in Tusk that are significantly different than in other languages. First, To call a function, we use `func_name:()`, instead of `func_name()`. This operation is `:` which means synchronous call. Tusk also has asynchronous functions. To call an function asynchronously, you can use the `?` operator as mentioned before.

```clojure
test?(1, 2, 3)
; instead of
test:(1, 2, 2)
```
The `?` operator returns a thread type. If you want to get the value of a thread type, you can use the `await` function

```clojure
value := await:(test?(1, 2, 3))
; or you can do
val1 := test?(1, 2, 3)
; do stuff
val2 := await:(val1)
```

Second, parameter lists in tusk look like
```
(string -> a, string -> b)
```
Whereas in javascript, and python they look more like
```
(a, b)
```
The key difference is that tusk names a type before an argument. This is because tusk allows something called overloading. If you want an argument to have any type you can use `any ->`.
```clojure
fn(any -> a, any -> b) ;accepts any type for a and b
```

But the tusk compiler can automatically assume the type:

```clojure
fn(a, b) ;automatically gets converted to fn(any -> a, any -> b)
```

Now lets look at the previous example, but with wrong types

```clojure
var main = fn() => {
  ;pass bool, string, and array
  val := test:(true, "hi", (1, 2, 3))
}

var test: fn(number -> a, number -> b, number -> c) => {
  return a + b + c
}
```

This would cause an error, where the function with that type list does not exist. Now let's overload this function!

To overload, you can use the built in `ovld` keyword.

```clojure
var main = fn() => {
  ;pass bool, string, and array
  val := test:(true, "hi", (1, 2, 3))
}

var test = fn(number -> a, number -> b, number -> c) => {
  return a + b + c
}

;create an overloaded `test` with the type list of bool, string, and array
ovld test = fn(bool -> a, string -> b, array -> c) => {

  log a
  log b
  log c

  return false
}
```
