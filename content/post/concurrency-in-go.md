+++
categories = ["golang"]
date = "2016-05-16T21:04:53+02:00"
description = ""
keywords = ["golang"]
title = "First try with concurrency in Go"

+++

It's been a while I'm practicing with Go, but I had still never tried its concurrency features so far. My bad.

Fortunately [exercism.io](http://exercism.io) has just introduced me to this topic with the exercise ["Parallel Letter Frequency" exercise"](http://exercism.io/exercises/go/parallel-letter-frequency/readme).

The core of my solution is here (I let you read the comments).

Basically the exercise asks you to count the frequency of the letters in 3 different strings. They provide you with already a function that counts the frequency, but you are asked to call that function with 3 calls in parallel (one call for each string) and to collect the result (the total frequencies from all the 3 strings).

``` go
func Frequency(s string) map[rune]int {
  //DO SOMETHING
}
func ConcurrentFrequency(words []string) map[rune]int {
  // (buffered)channel if type map[run]int with capacity of the lenght of the input (3)
	channel := make(chan map[rune]int, len(words))

	for _, value := range words {
		// anonymous function that calls Frequency() 3 times in parallel
		// and puts the three different results in the channel of capacity 3
		go func(v string){
			channel <- Frequency(v)
		}(value)
	}

  // Now use the values inside the channel.
  frequency := map[rune]int
	// loops 3 times because channel of size 3
	for range words {
		for key, value := range <-channel {
			frequency[key] += value
		}
	}
  return frequency
}
```

In this solution I am basically looping over the array of strings in input and call the Frequency() function on every iteration. The interesting thing is here:

``` go
go func(v string){
  channel <- Frequency(v)
}(value)
```

Here I'm starting a **goroutine** on an **anonymous function** (the _go_ prefix before _func_) inside of which I call Frequency(). The Frequency function sends its returned value in a **channel** (of the same type returned from the function). The channel is the way goroutines communicates with each other and so it's also the way to send values back.

Once the channel contains the returned values, you can loop over the channel itself (not sure here if it's because it's a _buffered channel_ and so with a specified capacity or I can do this every time, I still have to understand this).
The channel is of type _map[rune]int_ and so I can fetch <key, value> from it, like so:

``` go
for range words {
  for key, value := range <-channel {
    frequency[key] += value
  }
}
```

Working with channels is very simple and powerful. There are plenty of things that I still have to learn, but this was a good start. **Thanks Exercism.io**!
