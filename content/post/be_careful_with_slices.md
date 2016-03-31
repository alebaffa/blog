+++
categories = ["golang"]
date = "2016-03-31T06:56:10+02:00"
description = "Bad things happen when you don't take care of the capacity of the slice"
keywords = ["golang", "slices"]
title = "Be careful with slice"

+++

[Slices](https://blog.golang.org/slices) are a great tool in Go, but sometimes they can be confused with arrays.
A small reminder: slices are a pointer into an underline array. Let's take this example:

```go
array := []int{1, 2, 3, 4, 5, 6}
slice := array[1:3]

// let's print both
fmt.Println("array: ", array)
fmt.Println("slice: ", slice)

// array:  [1 2 3 4 5 6]
// slice: [2 3]
```
Since the slice is only a pointer to the underline array, if you do some operations with the elements of the array you are also changing the elements of the slice. Like this example:

```go
// let's double the first element of the array
array[1] *= 2

// let's print the array and the slice
fmt.Println("array: ", array)
fmt.Println("slice: ", slice)

// array:  [1 4 3 4 5 6]
// slice: [4 3]
```
A slice have two important properties:

```go
fmt.Println("length of the slice: ", len(slice))
fmt.Println("capacity of the slice: ", cap(slice))

// length of the slice: :  2
// capacity of the slice: 5
```
The length is the number of elements that the slice contains, while the capacity is the max number of elements it can contain.

It's important to take care of what happens when the slice fulfills its capacity. Let's continue the example by adding new things in the slice (and so in the array):

```go
middle = append(slice, 100)
middle = append(slice, 101)
middle = append(slice, 102)
middle = append(slice, 103)

// slice:  [4 3 99 100 101 102 103]
// array:  [1 4 3 99 100 101]
// capacity of slice:  10
```

The array has reached its length (6 elements), but the slice has been extended. It is actually been copied and moved and it became a new slice with double capacity (10. It was 5 before).

At this point the slice is not pointing anymore to that array. So, now if you do some operations to the underline array, the elements of the slice won't change anymore. Example:

```go
// let's double the first element of the array
array[1] *= 2

// let's print the array and the slice now:
fmt.Println("array: ", array)
fmt.Println("slice: ", slice)

//array:  [1 8 3 99 100 101]
//slice:  [4 3 99 100 101 102 103]
```
As you can see, the _array[1] = 8_, but the corresponding element in the slice is still 4.

This is an important thing to take care of when you're using slices. It can be really confusing. Always take care of the capacity in case your program is managing a lot of elements.
