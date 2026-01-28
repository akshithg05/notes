## What Kind of Language Is Go?
- Go is a **systems programming language**
- **Statically (strictly) typed**
- **Compiled** language with **fast compilation**
- Designed for **simplicity, performance, and concurrency**

---

## Compilation Model
- Go code is compiled **directly into native machine code**
- The compiled binary includes **OS-specific system calls**
- Go uses a **single compiler toolchain** (`go` command)
- Supports **cross-compilation** out of the box (compile for other OS/architectures)

### Key Point
> Go always produces **executables**, not intermediate artifacts like `.jar` files.

---

## Executables vs Libraries
- Go **does not compile libraries into separate binary artifacts**
- Go libraries (packages) are **source code only**
- Your code + imported packages are **compiled together into one executable**

### Result
- Produces a **single, self-contained binary**
- No runtime dependency on external Go libraries

---

## Tooling Philosophy
- Go uses **one tool (`go`)** for:
  - Compilation
  - Dependency management
  - Testing
  - Formatting
- No need for extra build tools (like Maven, Gradle, etc.)

---

## Standard Library
- Go ships with a **very comprehensive standard library**
- Covers:
  - Networking
  - HTTP servers
  - Cryptography
  - File I/O
  - Concurrency primitives
  - CLI tooling

### What Go Standard Library Lacks
- No official support for **Graphical / Desktop UI applications**
- Go is primarily used for:
  - CLI tools
  - Backend services
  - Networking systems
  - Distributed systems

### Best Practice
> Prefer the **standard library** whenever possible.  
> Most Go programs do **not** require third-party libraries.

---

## Third-Party Libraries
- Third-party libraries exist but should be used **judiciously**
- Over-reliance on external packages is generally discouraged

### Web Frameworks
- Popular web frameworks (e.g., Gin) exist
- **Idiomatic Go encourages using `net/http` (standard library)**
- Heavy frameworks are often considered **unnecessary** for many use cases

---

## Go Installation
- Download from the official site: https://go.dev/dl/
- Go installs as a **self-contained toolchain**

---

## Important Environment Variables

### `GOPATH`
- Workspace directory used by Go tooling
- Historically used to store:
  - Source code
  - Compiled packages
  - Binaries
- Default location:

```
<user-home>/go
```


- Modern Go (modules) **does not require** you to work inside `GOPATH`, but it still exists

---

### `GOBIN`
- Directory where compiled **Go binaries** are installed
- Contains executables built via `go install`
- Typically **no need to modify or touch**

---

### `GOOS`
- Specifies the **target operating system**
- Examples:
- `linux`
- `windows`
- `darwin`

---

### `GOARCH`
- Specifies the **target CPU architecture**
- Examples:
- `amd64`
- `arm64`

---

## Cross Compilation
- Changing `GOOS` and `GOARCH` allows you to compile for **different platforms**
- Example:
```bash
GOOS=linux GOARCH=amd64 go build
```


### Key Idea

> Go compiler generates **native machine code** for the target OS + architecture.

---

## Summary

- Go is fast, simple, and production-oriented
    
- Single compiler, single binary output
    
- Strong standard library reduces dependency sprawl
    
- Excellent for backend, systems, CLI, and distributed applications


# Go Modules & Packages – Notes

## Go Modules
- All Go code is organized into modules
- A module is a single unit of versioned Go code
- A module starts at the directory containing the go.mod file

### Purpose of a Module
- Groups code that belongs together for a specific purpose
- Example: a backend service, CLI tool, or system like Docker
- A module is named, versioned, and downloaded entirely as source code

## Module Name
- Usually a repository URL without protocol
- Typically points to a source control system, most often Git
- Used by the Go toolchain to locate and download the module

Example:
github.com/user/project

## Module Versioning
- Go modules follow Semantic Versioning
- Version format: vX.Y.Z
  - X → Major version
  - Y → Minor version
  - Z → Patch version
- Versions are strictly enforced in Go
- If no version is specified, Go selects the latest compatible version

## Semantic Versioning Rules

### Patch Version
- Bug fixes only
- No new features
- Fully backward compatible
- Example: v1.2.3 → v1.2.4

### Minor Version
- New features added
- No breaking changes
- Backward compatible
- Example: v1.2.0 → v1.3.0

### Major Version
- Breaking changes
- Backward compatibility not guaranteed
- In Go, major versions v2 and above must be included in the module path
- Example: github.com/user/project/v2

## Pre-release Versions
- Used for testing and early access
- Not selected by default unless explicitly requested
- Examples: v1.2.0-beta.1, v1.2.0-rc.1

## Modules vs Packages
- A module is a collection of packages
- The module version applies to all packages inside it
- Any change to a package requires a new module version

## Packages
- A package is a directory containing Go source files
- Each package represents one logical responsibility
- Every directory inside a module is a separate package
- Sub-directories are also separate packages

## Fully Qualified Package Name
- Consists of the module name followed by the package path
- Example: github.com/user/project/utils

## Source Code Organization
- The directory containing go.mod is the module root
- All subdirectories belong to the same module
- Each directory corresponds to exactly one package

Example structure:
project1
- go.mod
- main.go (package main)
- utils
  - helper.go (package utils)
- api
  - server.go (package api)

## Main Package and Executables
- A package named main produces an executable
- Program entry point is the main function
- Only one main function per main package
- A single module can contain multiple main packages in different directories
- Each main package produces a separate executable

## Package Contents
A package can contain:
- Variables
- Constants
- Functions
- Types such as structs and interfaces

### Scope Rules
- Package-level variables, constants, and functions are accessible anywhere within the same package

## Exported vs Unexported Identifiers
- Identifiers starting with a capital letter are exported
- Identifiers starting with a lowercase letter are package-private
- Go does not use public or private keywords
- Visibility is controlled by naming

## Using Standard Library Packages
- Standard library packages do not need to be listed in go.mod
- They are imported directly and always available

## Dependency Resolution
- Go resolves dependencies at the module level
- Packages are downloaded and cached automatically
- Dependency resolution is deterministic and reproducible

## Strings in Go
- Interpreted strings use double quotes and support escape characters
- Raw strings use backtick syntax
- Raw strings do not process escape sequences
- Raw strings can contain newlines and special characters
- Raw strings cannot contain backticks

## Compilation Rules
- Go compiler compiles entire packages, not individual files
- Single file compilation is not supported
- All files in a package are compiled together as a unit

## Key Takeaways
- Modules are the unit of versioning
- Packages are the unit of organization
- One directory equals one package
- Capitalization controls visibility
- Go enforces strict and predictable dependency management


# go run vs go build – Notes

## go run
- go run executes **only the main package**
- It is meant for **quick local testing**
- go run **hides the compilation step**
- The compiled binary is placed in a **temporary location**
- The location of the compiled output is **not exposed or controlled**
- The binary is deleted after execution

### Best Practice
- Do **not** use go run in production workflows
- Avoid go run for serious development or debugging
- It should not be relied upon for understanding build behavior

---

## go build
- go build is the **recommended command**
- It explicitly compiles Go code into a binary
- go build works at the **package level**

### Build Behavior
- By default, go build builds the package in the **current directory**
- It does **not** automatically build subdirectories
- Only the package in the current directory is built

### Dependencies
- go build automatically compiles **all referenced packages**
- Dependency packages are compiled as needed
- Only the final binary for the target package is produced

---

## Output Location
- The compiled binary is created in the **current working directory**
- Output location is predictable and controlled
- Makes debugging and inspection easier

---

## Multiple Packages
- go build can build multiple packages if explicitly specified
- Otherwise, it builds exactly **one package at a time**

---

## Summary: go run vs go build

go run:
- Executes main package only
- Hides compilation
- Temporary binary
- Not recommended for real development

go build:
- Explicit compilation
- Predictable output
- Builds dependencies
- Recommended for development and production

---

## Go Package Registry
- https://pkg.go.dev/
- Central index of all **published Go packages and modules**
- Includes:
  - Standard library
  - Third-party modules
  - Documentation
  - Version history
- Packages listed here are published and accessible worldwide


#### Session 2


### Comments in go 

Comments placed above the package statement with starts with Package capital P , is package documentation. It is placed in the packers docs. packages should always be documented

If the top level package name has the same name as the last part of the module name then module name and package name is the same.


### Variables
Vars in go can be declared at package level, function level and block level

Package level vars are available in the entire package, in functions and block.

Outside the package depends on the name of the variable. Capital letter means it will be available outside the package as well. small letter means .

vars can be written as -

```
var <name> <type>

or

var <name> = <value>  // Array literal 
```

Variables must have a type

Go is a very strict language, other types cannot be assigned to other types at all.

### Data Types 
Integer, signed, unsigned. int/ uint - size based on architecture 64 or 32.
Float - float
Complex - complex
Boolean - bool ?
string - GO strings are unicode., not an array of chars, unicode code points, runes, fully internationalized. 
rune (not used much) , can use one single unicode character

Go is a garbage collected language. No difference between declaration and definition. As soon as declared it will declare memory for the variable.

The moment you run a program package level variable memory is allocated. Memory will be de allocated when the program terminates itself, not before. Because packages are unloaded only when program terminates.

0 value for integer is 0, for string ' ', 
For Boolean it is false 
zero value of float and complex is 0.00

if you declare a variable and dont give a value it will take the zero value.

When the var goes out of scope the memory will deallocate.

In terms of performance, declaring a variable is allocating memory in go lang.

Do not declare pkg level vars unless absolutely required

### Collections in golang

#### Arrays

Array - in go arrays data size is part of the data type , code -

```go
 var x = [10]int
 x[0] = 1
 x[1] = 2
 
 var y = [10]int
 
 y = x
```

Entire array of x is copied to y.

```go
 var x = [10]int
 x[0] = 1
 x[1] = 2
 
 var y = [11]int
 
 y = x
```

This will throw a compile error , because size is part of datatype in arrays

```go
var x = [10]int{22,23,24}
```

The above x variable is 10 element integer array where the first 3 elements are 22 23 and 24, and the rest of the elements are the default 0 value , which is 0.


### Constants

```go
// MaxNumber is the largest number that can be used in this go version
const MaxNumber = 9999
```


Capital MaxNumber means it is exported and can be used outside the package.
The moment we are exporting something , we need to document it. Best practice is to use the same name as the name as the constant name as starting word.

### Functions

```go
func Convert(number int) (string, error) {}
```

The function takes one argument of integer and can return either string or error. Go functions can return how many ever types of datatypes as needed.

The practice in go is to always include error as a return type and return an error. If any function is void and likely to cause an error , just then return error.

Early returns are a good practice, for better performance and memory allocation practices.

```go
return "", errors.New("number not in valid range")
```
We have to return all datatypes while returning.

In error messages, following the idiomatic go convention, we need to put error message in all lowercase and not have any punctuation marks.

Inside functions this is the convention of declaring and defining variables. All variables are function scoped if declared inside the function and not inside a block

```go
result := ""
```

Similar documentation rules for exporting functions.

Variable shadowing occurs in golang as well.

= means assigning a variable
:= means creating a new variable

if we are not going to use a returned value we can use __

### If else blocks

```go
if var x= 0, v=1; condition1
```

We can define variables in the if else block condition , and the scope is only the if else block. 

Slices: Dynamic arrays
Maps: key value pairs

Slices and maps internally use ararys only.

### nil
Nil means there is no error. Nil can be assigned only to certain data types. It can be used with error.
It cannot be used with int , str, bool as they have a default 0 value.

Go does not have ternery operator or single line if statement. If has to be written in full, no other value.
As far as possible do not write else statements. Try and avoid else. Makes logic clear.



## Pointers in Go

Less flexible, more powerful than C pointers

Pointers are data types in go. There is nothing as void pointer. Pointer points to a particular data type only.
They point to some reference variable

```go
var x *int
```
This can only point to a block of memory which is an integer

Any pointer based data type has 0 value nil.

```go
var x *int
y: = 42
x  = &y
z: = *x
*x = *x + 1
return x
```

Explain above code

Error is a type pointer.

When do we use pointers - 
When we want to refer to a single object in memory.
To conserve memory and want to change these objects.

```go
a := &[2]int{33,44}
z :=a[1]
a = &[2]int{55,66} // Allowed
a = &[3]int{1,2,3} // Compilation error
```

## Go internal testing library

Use same package name with underscore test or same package name as package.
Name file with undesrcore test.

Package name can be same package name of what we are building or it can be that of the (underscore)test package we named.

order is not guaranteed.

Name of the test starts with Test and it should have a data type with ``` *testing.T```


### Map - collection data structure

A map is a dictionary, collection of key value pairs. We need to give unique key and corresponding value.

There is no such thing as only map, it is map of some key and some value.

Example - 
```go
map[int]string
```

The keys will be integer and values will be string.
Value can be any data type whatsoever. Key can be any datatype which is comparable (integers, boolean, strings). No pointers, as they cant be keys and non comparable, pointers can be values.

```go
var xx map[int]string

xx = make(map[int]string)
```

Make is a function given by go language itself, rare function.

when we use make , there is some memory allocated to hold N number of keys and values

```go
xx = make(map[int]string, 5)
```
Here we are initially allocating memory for 5 keys and 5 values.

Then we can do this -

```go
x[22] = "Go"
```

Unless actually memory is required it will not allocate more than required memory. If key already exists value will be over written.
```go
yy, ok:=xx[23]
```
If 23 key exists then yy will have the value and ok will be true, else if 23 index does not exist , ok will contain false and yy will contain the 0 value of string which is empty string.

ok is not a keyword, its a variable.

```go
xx=delete(xx,22)
```
Deleting the 22 index


We can also use the map literal
```go
xx:= map[int]string{
	22: "Twenty two",
	23: "Twenty three"
}
```

### Go has only 1 loop: For loops

1. Simplest form of for loop

Infinite loop
```go
for {
	}
```

2. For condition

```go
for <condition>{

}
```

Until condition is true keep executing 

3. For condition statement
```go
for <int>;<condition>; <statement>{
}
```

4. For with iterator
```go
for <variable>:= condition
   
```

For arrays and maps -

```go
for key,value := range tests{
}
```


t.Fatal() vs t.Fail()

t.Fatal() - full test fails.
t.Fail() - that particular iteration in the loop failed.

If there is no t.Fatal() or t.Fail() called, it means that the test case has passed.


go test complies all the tests into an executables and puts them in a certain location and executes them and returns a pass fail result.


Steps to run go files - 

Write code
run go mod tidy to get all packages in go.mod file
then run go build
run the .exe file

If we want a package manually , run - go get (package name)


Go proxy server collects , and servers go packages.
we can run our own go proxy server as well.
GOPROXY=https://proxy.golang.org,direct - this is the global proxy


Aliases for package names

```go
package main

import (
    "fmt"
    n2 "github.com/rajch/numbertowords"
)


func main(){
    result ,_ := n2.Convert(1234)
    fmt.Println(result)
}
```


We can only publish to src control, not publish to a proxy

We can read docs with the following command - go doc github.com/rajch/numbertowords.Convert


# go.sum – Notes

## What is go.sum
- go.sum is a file used for **dependency integrity verification**
- It is automatically maintained by the Go toolchain
- It records **cryptographic hashes** of module versions that your project depends on

---

## How go.sum is Generated
- go.sum is updated when you run:
  - go mod tidy
  - go get
  - go build (if new dependencies are introduced)
- Hashes are fetched from the module source (usually a source control system)

---

## What go.sum Contains
- Hashes of:
  - Direct dependencies
  - Indirect (transitive) dependencies
- Each entry ensures that the **exact same source code** is used every time

---

## Security Guarantee
- If a dependency’s source code is **tampered with** or altered:
  - The hash will not match
  - Go will **fail the build**
- This prevents:
  - Supply chain attacks
  - Silent dependency modification
  - Inconsistent builds across machines

---

## Why go.sum Exists
- Ensures **reproducible builds**
- Guarantees **dependency integrity**
- Makes builds deterministic across:
  - Developers
  - CI systems
  - Production environments

---

## Comparison to Other Ecosystems
- go.sum is conceptually similar to:
  - package-lock.json in npm
- Both lock down dependency integrity
- Difference:
  - go.sum stores **hashes**, not a full dependency tree
  - Version selection logic remains in go.mod

---


The moment our module has multiple packages, use subdirectories, avoid root directory.

If we are creating one or more executables, create a folder cmd and create subdirectories there and each of the package there will have a main package.
Only main package can create executables (.exe).

For library packages, create a directory called pkg, then create subdirectories for every package.

This was the old practice, now just create sub directories directly for non main packages.

If we publish our module and do not want some of the packages to be published or available to everyone put those packages inside internal


### Composite data types

struct
struct of something

typedef can be used to create a new data type of the existing type.

```go
package model

type expense struct {
    Id          int64
    Description string
    Amount      complex64
}

var aa expense
var xx = expense{
    Id:          1,
    Description: "Breakfast",
    Amount:      200.00,
}

var yy = expense{0, "Taxi", 234.345}
```

### Slices

Slice is like array, does not have size as part of its size definition.
Slice is like a pointer, it points to some array or some part of an array.
I can append to a slice, add another entry to the slice, slices length will increase by 1.

When we append to a slice, if appending does not exceed capacity, then no extra memory allocation. 

When we exceed capacity, the slice is copied to a new array with new capacity and slice points to that.

Only length will change when we delete , capacity remains the same.

