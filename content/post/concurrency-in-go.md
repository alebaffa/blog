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

Working with channels is very simple and powerful. There are plenty of things that I still have to learn, but this was a good start. **Thanks Exercism.io**!
