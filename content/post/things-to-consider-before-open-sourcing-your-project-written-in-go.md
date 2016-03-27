+++
date = "2016-03-27T11:56:13+02:00"
description = ""
title = "Things to consider before open sourcing your project written in go"

+++
so, you want to finally release your _preciousss_ written in Go to the open source community. Great! And thank you.
Though, there are few things you may want to consider before doing the big step. Things that you may have missed perhaps because you are not yet 100% comfortable with Go (but “_I will improve later. Now let me just put this gem on Github._”).
You have to know that the Go community can be quite strict when it comes to its idioms and conventions. And they are right, in my opinion. So, in order to avoid hundred of issues and pull requests on Github focused mainly on code style and best practices, and not on the real core of your project, check these following few things before pushing your code.

## Be sure you read Effective Go

[Effective Go](https://golang.org/doc/effective_go.html) contains all the tips you need to know in order to write clear and idiomatic Go code. You will learn all the best practices and the conventions used and followed by the Go community.
Effective Go is essential not only for newbies programmers, but also (and foremost) for those coming from other programming languages.

>A straightforward translation of a C++ or Java program into Go is unlikely to produce a satisfactory result — Java programs are written in Java, not Go.

## Avoid common mistakes
The Go community over the years has identified some common mistakes made in Go projects, and so common comments in the code reviews. These comments are now collected in the [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments) page.
Be sure not to make these common mistakes yourself, so give a read to that page.

## Use all the tools
Go comes with some amazing tools that allow you to write idiomatic Go with less effort. Be sure to check all your code with, at least, these few ones:

* [gofmt](https://golang.org/cmd/gofmt/): to automatically formats Go source code.
* [golint](https://github.com/golang/lint): to print out code style mistakes.
* [govet](https://golang.org/cmd/vet/): to examine the code and report suspicious constructs.

Only by using at least these 3 tools you can manage to write clear and idiomatic Go code and avoid a lot of issues and pull requests. And they also help you to learn Go in the proper way :) .
**Good news**. The Go community is so good that there are plugins for the most used IDE: [GoSublime](https://github.com/DisposaBoy/GoSublime) and the [official Google plugin](https://forum.golangbridge.org/t/beta-testers-wanted-sublimetext-go/1282) (in test) for SublimeText, [GoPlus](https://atom.io/packages/go-plus) for Atom, [vim-go](https://github.com/fatih/vim-go) for Vim and, incredibly enough, VisualStudio has a lot of good reviews for Go.
There are a lot of other IDE, but these ones, apparently, are the most used ones by the community.

## Stay up-to-date with the Go development
If you are open sourcing a Go project chances are that you may be impacted by changes in the Go libraries, or whatever can happen with the development of Go in general. It’s better to stay up-to-date with what happens and follow the discussions on these Google Groups:

* [golang-dev](https://groups.google.com/forum/#!forum/golang-dev): discussions of the development of the Go project.
* [golang-nuts](https://groups.google.com/forum/#!forum/golang-nuts): general discussion list for the Go Programming Language.

## Be part of the community
The Go community is super active. Just go [here](https://github.com/golang/go/wiki#the-go-community) to choose how you want to follow it. It’s important to follow the discussions if you’re seriously working with Go, you may discover useful things, or you could get to know important developments or projects that can impact your work.
And don’t forget the [Code of Conduct](https://golang.org/conduct).

---
Good! Now that you know what to check .. just to do it and let us know when your preciousss will be available for us to enjoy! :)
