
# Functional Programming with Scala

## About the Functions
* Will will cover the essentials
  * `map`
  * `filter`
  * `flatMap`
  * `foreach`
* There are many more, but these are the core functions that you will find in both Scala and Spark

## `map` function

* `map` applies a higher order function to every element in a collection or container
* Available on nearly every collection or container in Scala
* The structure and properties for `map` are nearly identical across all collections

## `List` and `map`

* This is the API Signature of `map` for `List`
* Note that the parameterized type of the List in this case is `[A]`

![list_map_function.png](../images/list_map_function.png)


```scala
List(1,2,3,4).map(x => x + 1)
```




    res4: List[Int] = List(2, 3, 4, 5)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/List.html

## `Set` and `map`

* This is the API Signature of map for Set
* Note that the parameterized type of the Set in this case is `[A]`
* Important to note to not expect a certain order when dealing with a `Set`

![list_map_function.png](../images/set_map_function.png)


```scala
Set(5,10,13,12).map(x => x + 1)
```




    res5: scala.collection.immutable.Set[Int] = Set(6, 11, 14, 13)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/Set.html

## `Map` and `map`

* This is the API Signature of `map` for `Map`
* Note that the parameterized type of the Map in this case is `[K,V]`
* `K` is the key parameterized type
* `V` is the value parameterized type

![list_map_function.png](../images/map_map_function.png)


```scala
Map(1 -> "One", 2 -> "Two").map(t => (t._1 + 100, t._2 + " Hundred"))
```




    res6: scala.collection.immutable.Map[Int,String] = Map(101 -> One Hundred, 102 -> Two Hundred)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/Map.html

## `String` and `map`

* This is the API Signature of map under the `StringOps` wrapper
* Note that the parameterized type of the `StringOps` in this case is actually `Char`

![string_map_function.png](../images/string_map_function.png)


```scala
"Hello".map(c => (c + 1).toChar)
```




    res7: String = Ifmmp
    



### `Option` and `map`

* This is the API Signature of map under the `Option` wrapper
* Note that the parameterized type of the `Option` in this case is `[A]`
* It keep the same construct, `Some` or `None`, and in the case of `Some` apply the function.

![option_map_function.png](../images/option_map_function.png)


```scala
Some(10).map(x => x * 10)
```




    res41: Option[Int] = Some(100)
    




```scala
Option.empty[Int].map(x => x * 10)
```




    res42: Option[Int] = None
    



## `map` Conclusion
* `map` takes a function, and applies that function in every element in a collection.
* `map` can be applied to `List`, `Set`, `Map`, `Stream`, `String`, even `Option`!

## `filter` function

* Using the `filter` function
* `filter` removes elements from a collection based on a function or predicate
* A predicate is a function that returns `true` or `false`
* Available on nearly every collection in Scala
* The structure and properties for filter are nearly identical across all collections

### `List` and `filter`

* This is the API Signature of filter for List
* Note that the parameterized type of the List in this case is `[A]`

![list_filter_function.png](../images/list_filter_function.png)


```scala
List(1,2,3,4).filter(x => x % 2 == 0)
```




    res1: List[Int] = List(2, 4)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/List.html

### `Set` and `filter`

* This is the API Signature of `filter` for `Set`
* Note that the parameterized type of the Set in this case is `[A]`

![set_filter_function.png](../images/set_filter_function.png)


```scala
Set(1,2,3,4).filter(x => x % 2 == 0)
```




    res2: scala.collection.immutable.Set[Int] = Set(2, 4)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/Set.html

### `Map` and `filter`

* This is the API Signature of filter for Map
* Note that the parameterized type of the Map in this case is `[K,V]`
  * `K` is the key parameterized type
  * `V` is the value parameterized type
  
![map_filter_function.png](../images/map_filter_function.png)


```scala
Map(1 -> "One", 2 -> "Two", 3 -> "Three").filter(t => t._2.startsWith("T"))
```




    res6: scala.collection.immutable.Map[Int,String] = Map(2 -> Two, 3 -> Three)
    



Link: https://www.scala-lang.org/api/current/scala/collection/immutable/Map.html

### `String` and `filter`

* This is the API Signature of filter for StringOps
* Note that the type for `StringOps` in this case is actually `Char`

![string_filter_function.png](../images/string_filter_function.png)


```scala
"Hello".filter(c => List('a', 'e', 'i', 'o', 'u').contains(c))
```




    res17: String = eo
    



### `Option` and `filter`

* This is the API Signature of `filter` for `Option`
* Note that the parameterized type of the `Option` in this case is `[A]`
* Note what happens when a filter operation returns false in the predicate.

![option_filter_function.png](../images/option_filter_function.png)

Link: https://www.scala-lang.org/api/current/scala/Option.html


```scala
Some(4).filter(x => x % 2 == 0)
```




    res44: Option[Int] = Some(4)
    




```scala
Some(313).filter(x => x % 2 == 0)
```




    res43: Option[Int] = None
    



## `foreach`

* Like `map`, we apply a function to each element
* Unlike `map`
  * The return type for foreach function is `Unit`
  * The function applied must also return a `Unit`
  * `Unit` is an indication of a side effect
* Using `map` instead of `foreach`

If we ran the following:


```scala
val a = (1 to 10)
val list = a.map(x => println(x))
println(list)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    Vector((), (), (), (), (), (), (), (), (), ())
    




    a: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    list: scala.collection.immutable.IndexedSeq[Unit] = Vector((), (), (), (), (), (), (), (), (), ())
    



### Cleaner output with `foreach`

* Use `foreach` so that we don’t have to see that messy end result
* Each item is given to the function returns a Unit (not mandatory)
* Here is the `foreach` function for `List`

![list_foreach_function.png](../images/list_foreach_function.png)

### Change `map` to `foreach`

Changing the previous slide contents this will look like:


```scala
val a = (1 to 10)
val list = a.foreach(x => println(x))
println(list)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    ()
    




    a: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    list: Unit = ()
    



There we get the response we were looking for and the return is a `Unit`. We typically don't print out the result of the `foreach`. Below is the typical invocation.


```scala
val a = (1 to 10)
a.foreach(x => println(x))
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    




    a: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    



### Refactoring foreach

Clearing out the assignment we just have:


```scala
val a = (1 to 10)
a.foreach(x => println(x))
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    




    a: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    



Let’s just refactor foreach further using `_` placeholder

val a = (1 to 10)
a.foreach(println _) //println is a perfect candidate, it returns Unit.

The place holder `_` is the last item within the parenthesis, and if you remember the postfix operations of a function. We can remove the placeholder

val a = (1 to 10)
a.foreach(println) //println is a perfect candidate, it returns Unit.

### Final Refactoring with `foreach`

Since `foreach` takes one argument we can call it as infix:


```scala
val a = 1 to 10
a foreach println
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    




    a: scala.collection.immutable.Range.Inclusive = Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
    



Inlining the whole thing:


```scala
1 to 10 foreach println
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    

### `Set` and `foreach`

This is the API Signature of foreach for Set
Note that the parameterized type of the Set in this case is `[A]`

![set_foreach_function.png](../images/set_foreach_function.png)

Link: http://www.scala-lang.org/api/current/scala/collection/immutable/Set.html


```scala
Set(4,10,50,40,22,12,19,50).foreach(x => println(x))
```

    10
    22
    12
    50
    40
    19
    4
    


```scala
Set(4,10,50,40,22,12,19,50).foreach(println)
```

    10
    22
    12
    50
    40
    19
    4
    

### `Map` and `foreach`
This is the API Signature of foreach for Map

* Note that the parameterized type of the Map in this case is `[K, V]`
  * `K` is the key parameterized type
  * `V` is the value parameterized type

![map_foreach_function.png](../images/map_foreach_function.png)

Link: http://www.scala-lang.org/api/current/scala/collection/immutable/Map.html


```scala
Map(1 -> "One", 2 -> "Two", 3 -> "Three", 4 -> "Four").foreach(x => println(x))
```

    (1,One)
    (2,Two)
    (3,Three)
    (4,Four)
    

### `String` and `foreach`

* This is the API Signature of foreach for String
* Note that the parameterized type of the `StringOps` in this case is `[A]` but is usually `Char`

![string_foreach_function.png](../images/string_foreach_function.png)

Link: http://www.scala-lang.org/api/current/scala/collection/immutable/StringOps.html


```scala
"Hello, There".foreach(println)
```

    H
    e
    l
    l
    o
    ,
     
    T
    h
    e
    r
    e
    

### `Option` and `foreach`

* This is the API Signature of `foreach` for Option
* Note that the parameterized type of the `Set` in this case is `[A]`

![option_foreach_function.png](../images/option_foreach_function.png)

Link: http://www.scala-lang.org/api/current/scala/Option.html


```scala
Option(40).foreach(println)
```

    40
    

`Option.empty[Int]` will return a `None` with parameterized type of `Int`


```scala
Option.empty[Int].foreach(println)
```

### `foreach` Conclusion

* `foreach` is a method that takes a higher order function that will take an element and return `Unit`
* Perfect if you want to take an element and perform a side effect like print to screen
* `foreach` can be done to `List`, `Set`, `Stream`, `String`, `Array`, and more

## `flatMap`

### Using `flatMap`

* One of the most important functions/methods in functional programming
* Takes the value or values of one "container" and creates another "container" using the value.
* This is also important for for comprehensions

### Starting from `map`
Let’s say that we wish to `map` every element of a `List` into another `List`, seen below:


```scala
val a = List(1,2,3,4,5)
println(a.map(x => List(-x, 0, x)))
```

    List(List(-1, 0, 1), List(-2, 0, 2), List(-3, 0, 3), List(-4, 0, 4), List(-5, 0, 5))
    




    a: List[Int] = List(1, 2, 3, 4, 5)
    



This is just a plain map that returns a `List[List[Int]]`

### Avoiding the `List[List[_]]` with `flatten` and `map`

But let’s say that given all that we want to take that and flatten all that, this is where the `flatten` method can be used.


```scala
val a = List(1,2,3,4,5)
println(a.map(x => List(-x, 0, x)).flatten)
```

    List(-1, 0, 1, -2, 0, 2, -3, 0, 3, -4, 0, 4, -5, 0, 5)
    




    a: List[Int] = List(1, 2, 3, 4, 5)
    



That works out great, we see that we not longer have a list of list, we have a single list.

`flatten` is available in nearly all "containers", `List`, `Set`, `Map`, `Option`, `String`, `Stream`, etc.

### Avoiding the `List[List[_]]` with flatMap

* Here is a memory trick that you may find helpful:
* If you see a `Collection` in a `Collection` like we saw and you don’t want it like that, use `flatMap`.


```scala
val a = List(1,2,3,4,5)
println(a.flatMap(x => List(-x, 0, x)))
```

    List(-1, 0, 1, -2, 0, 2, -3, 0, 3, -4, 0, 4, -5, 0, 5)
    




    a: List[Int] = List(1, 2, 3, 4, 5)
    



The previous result looks exactly the same as the flatten and map combination

### `List` and `flatMap`

* Here is the API Signature of `flatMap` for `List`
* Note that the parameterized type of the `List` in this case is `[A]`
* Notice the signature of flatMap: `(A) ⇒ GenTraversableOnce[B]`
* Other `GenTraversableOnce[T]` subtypes include:
  * `Set`
  * `Map`
  * `Array`
  * `String`

![list_flatmap_function.png](../images/list_flatmap_function.png)

### `flatMap` with multiple layers

* Given the known signature of `flatMap`
* Even if the `Collection` are stacked in multiple layers we can `flatMap` until we get the collection we need.

val b:List[List[List[Int]]] =
   List(List(List(1,2,3), List(4,5,6)),
   List(List(7,8,9), List(10,11,12)))

* So what is the result of performing a flatMap on a `List[List[List[Int]]]`?
* Depends on the function

### The `Identity` Function

* The `identity` function is take the input and make it the output
* Instead of writing `x ⇒ x`, you can opt for `identity(x)`
* `identity` comes from the `Predef`

### The `identity` function and `flatMap`


```scala
val list:List[List[List[Int]]] =
    List(List(List(1,2,3), List(4,5,6)),
    List(List(7,8,9), List(10,11,12)))
list.flatMap(x => x)
```




    list: List[List[List[Int]]] = List(List(List(1, 2, 3), List(4, 5, 6)), List(List(7, 8, 9), List(10, 11, 12)))
    res32: List[List[Int]] = List(List(1, 2, 3), List(4, 5, 6), List(7, 8, 9), List(10, 11, 12))
    



### `Set` and `flatMap`

* This is the API Signature of `flatMap` for `Set`
* Note that the parameterized type of the `Set` in this case is `[A]`

![set_flatmap_function.png](../images/set_flatmap_function.png)

Link: https://www.scala-lang.org/api/current/scala/collection/Set.html


```scala
Set(2, 4, 10, 11).flatMap(x => Set(x, x*5))
```




    res33: scala.collection.immutable.Set[Int] = Set(10, 20, 2, 50, 11, 55, 4)
    



### `Map` and `flatMap`

* This is the API Signature of `flatMap` for `Map`
* Note that the parameterized type of the Map in this case is `[K, V]`
  * `K` is the key parameterized type
  * `V` is the value parameterized type

![map_flatmap_function.png](../images/map_flatmap_function.png)

Link: https://www.scala-lang.org/api/current/scala/collection/Map.html

### **Lab:** Map with `flatMap`

**Step 1:** Given what you know about `flatMap`, replace `???` with what you think it would take to produce the following output?

```
Map(1 -> "One", 2 -> "Two", 3 -> "Three",
    300 -> "Three Hundred", 200 -> "Two Hundred",
    100 -> "One Hundred")
```


```scala
val origMap = Map(1 -> "One",
    2 -> "Two",
    3 -> "Three")

val result:Map[Int, String] = ???
println(result)
```


    scala.NotImplementedError: an implementation is missing

      at scala.Predef$.$qmark$qmark$qmark(Predef.scala:230)

      ... 36 elided

    


### `flatMap` Conclusion

* `flatMap` is the combination of `flatten` and `map`.
* `flatMap` can be used with `List`, `Set`, `Map`, `String`, `Stream`, and `Option`
* Your cue is when you see a `List[List[A]]`, `Set[Set[A]]`, etc.
* `flatMap` can also be used with massive layering, `List[List[List[A]]]`

### `mkString`

* Concatenates all elements into one string given a delimiter
* Can be given a before and after `String` to flank the result string


```scala
List(1,2,3,4).mkString(":")
```




    res36: String = 1:2:3:4
    




```scala
Vector('z','a','b','c').mkString("~~")
```




    res35: String = z~~a~~b~~c
    




```scala
Set("Seattle", "Los Angeles", "Denver").mkString("$$", "#", "$$")
```




    res37: String = $$Seattle#Los Angeles#Denver$$
    



### **Lab:** Doing a better `isPrime`

*Step 1:* Knowing what you know now, is there a better `isPrime`? If so implement it!

Hint: Start with a range like `(1 to n)` and work from there. Look at the range API, specifically at the method `forall` and see if that will work! You can also try something else, lots of methods to choose from! **_There should be no for loops!_**. We want you to do your own research on this using the documentation at https://www.scala-lang.org/files/archive/api/current/scala/


```scala


```
