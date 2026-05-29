# Learning Go - An Idiomatic Approach To Real World Go Programming

## Chapter 1 - Setting Your Go Environment
The first thing you need to do is create a directory to hold your program. Call it Proj1.  On the command line, enter the new directory. Inside the directory, run the go mod init command to mark this directory as a Go module.

```bash 
mkdir Proj1
cd Proj1
go mod init hello_world
```

The go.mod file declares the name of the module, the minimum supported version of Go for the module, and any other modules that your module depends on. You can think of it as being similar to the requirements.txt file used by Python or the Gemfile used by Ruby. You shouldn’t edit the go.mod file directly. Instead, use the go get and go mod tidy  commands to manage changes to the file. The main package in a Go module contains the code that starts a Go program. All Go programs start from the main function in the main package. You declare this function with func main() and a left brace. Like Java, JavaScript, and C, Go uses braces to mark the start and end of code blocks.

```bash
go build
```

This creates an executable called as the name of the module (here is hello_world. remember `go mod init hello_world`). then run it like this:
```bash
./hello_world
```

The Go development tools include a command, go fmt, which automatically fixes the whitespace in your code to match the standard format. Using ./... tells a Go tool to apply the command to all the files in the current directory and all subdirectories.
```bash 
go fmt ./...
```


In one class of bugs, the code is syntactically valid but quite likely incorrect. The go tool includes a command called go vet to detect these kinds of errors. One of the things that go vet detects is whether a value exists for every placeholder in a formatting template.
```bash
go vet ./... 
```

## Chapter 2 - Predeclared Types and Declerations
