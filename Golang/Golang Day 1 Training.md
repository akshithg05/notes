
### [[2026-01-27]]
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

How Other Packages Are Handled

- **Utility Packages**: Packages with any name other than `main` are considered utility or library packages. These packages contain reusable functions and code that can be imported by other programs, but they cannot be built into a standalone executable themselves because they lack the necessary entry point (`func main()`).
- **Compilation**: When you use the `go build` command on a non-`main` package, Go compiles it and stores the results in a build cache for use by other projects, but it does not produce an executable binary file.
- **Multiple Executables in a Project**: A single Go project or module can contain multiple executables, provided each one is in its own separate directory and each of those directories declares `package main` and includes a `main()` function. A common convention is to place these in a `cmd/` directory, e.g., `cmd/cli/main.go` and `cmd/web/main.go`.
## Go Package Registry
- https://pkg.go.dev/
- Central index of all **published Go packages and modules**
- Includes:
  - Standard library
  - Third-party modules
  - Documentation
  - Version history
- Packages listed here are published and accessible worldwide


#### Session 2 - Post lunch




## Comments and Documentation
- Comments placed above the package statement starting with the word Package (capital P) are treated as package documentation
- These comments appear in package docs
- Packages should always be documented

Example:

```go
// Package mathutils provides helper math functions
package mathutils
```

- If the top-level package name matches the last part of the module name, the module and package names are effectively the same

---

## Variables
- Variables can be declared at:
  - Package level
  - Function level
  - Block level
- Package-level variables are accessible throughout the package
- Export rules:
  - Capitalized → exported
  - Lowercase → package-private

### Variable Declarations

```go
var count int
var name = "Go"
```

- Variables always have a type (explicit or inferred)
- Go is strictly typed; incompatible assignments are not allowed

---

## Data Types
- Integers: signed and unsigned
  - int and uint are architecture-dependent
- Floating point: float32, float64
- Complex: complex64, complex128
- Boolean: bool
- String:
  - Unicode by default
  - Represents Unicode code points (runes)
- Rune:
  - Alias for int32
  - Represents a single Unicode character

---

## Memory and Zero Values
- Go is garbage collected
- Memory is allocated at declaration time
- Package-level variables are allocated at program start
- Memory is released only when the program terminates

Zero values:
- int → 0
- string → empty string
- bool → false
- float and complex → 0

Example:

```go
var x int
var s string
var b bool
```
- Variables automatically receive zero values if not initialized
- Avoid package-level variables unless required

---

## Arrays
- Array size is part of the type
- Assigning arrays copies all elements

Example:

```go
var x = [10]int
x[0] = 1
x[1] = 2

var y = [10]int
y = x
```
- Arrays of different sizes are incompatible

  ```GO
var a = [10]int
var b = [11]int
b = a   // compile-time error
  ```

- Partial initialization fills remaining values with zero

 ```go
var z = [10]int{22, 23, 24}
 ```
---
## Constants
- Constants are immutable
- Exported constants must be documented

Example:

```go
// MaxNumber is the largest number supported
const MaxNumber = 9999
```

---

## Functions
- Functions can return multiple values
- error is conventionally returned as the last value
- Early returns improve clarity and performance

Example:

```go
func Convert(number int) (string, error) {
	if number < 0 {
		return "", errors.New("number not in valid range")
	}
	return "ok", nil
}
```
Rules:
- All return values must be returned
- Error messages should be lowercase and have no punctuation

---

## Variable Declaration Inside Functions
- := creates a new variable
- = assigns to an existing variable

Example:

```go
result := ""
result = "done"
```

- Variable shadowing is allowed
- Unused return values can be ignored using _

```go
    value, _ := Convert(10)
```

---

## Control Flow
- If statements can declare variables scoped to the block

Example:

```go
if x := 10; x > 5 {
	fmt.Println(x)
}
```
- Go has no ternary operator
- Prefer early returns instead of else blocks

---

## nil
- nil represents absence of value
- Allowed for:
  - pointers
  - slices
  - maps
  - interfaces
  - functions
  - channels
- Not allowed for int, string, bool

---

## Pointers
- Pointers are typed
- No void pointers
- Pointer zero value is nil

Example:

```go
var x *int
y := 42
x = &y
z := *x
*x = *x + 1
```

- Used to:
  - Refer to shared data
  - Avoid copying large values
  - Modify data in-place

---

## Testing in Go
- Test files end with _test.go
- Package name can match the source package or use _test suffix
- Test functions:
  - Start with Test
  - Accept *testing.T

Example:

```go
func TestAdd(t *testing.T) {
	if Add(2, 3) != 5 {
		t.Fail()
	}
}
```
- t.Fatal stops execution
- t.Fail marks failure but continues
- If neither is called, the test passes
- go test compiles tests into a temporary executable and runs them

---

## Maps
- Maps store key-value pairs
- Key type must be comparable
- Value type can be anything

Example:

```go
var xx map[int]string
xx = make(map[int]string)

xx = make(map[int]string, 5)
xx[22] = "Go"
```
Lookup with ok idiom:

```go
yy, ok := xx[23]
```

Delete entry:

```go
delete(xx, 22)
```

Map literal:

```go
xx := map[int]string{
	22: "Twenty two",
	23: "Twenty three",
}

```
---

## Loops
- Go has only one loop: for

Infinite loop:

```go
for {
}
```

Condition-only loop:

```go
for x < 10 {
	x++
}
```

Classic loop:

```go
for i := 0; i < 10; i++ {
}
```

Range loop:

```go
for key, value := range tests {
}
```
---

## go run vs go build
- go run:
  - Runs only main package
  - Hides compilation
  - Uses temporary binary
  - Not recommended for real development

- go build:
  - Explicit compilation
  - Builds current package only
  - Compiles dependencies
  - Produces predictable binary

---

## go.sum
- Stores cryptographic hashes of module versions
- Ensures dependency integrity
- Prevents tampering
- Similar to package-lock.json
- Must always be committed

---

## Project Structure Best Practices
- Only main packages produce executables
- Multiple executables:
  - Use cmd directory with subdirectories
- Non-main packages:
  - Use subdirectories directly
- internal directory:
  - Packages cannot be imported outside the module

---

## Structs and Custom Types

Example:

    type expense struct {
        Id          int64
        Description string
        Amount      complex64
    }

    var a expense
    var b = expense{
        Id:          1,
        Description: "Breakfast",
        Amount:      200.00,
    }

    var c = expense{0, "Taxi", 234.345}

---

## Slices
- Slices are dynamic views over arrays
- Slice type does not include size

Example:

    s := []int{1, 2, 3}
    s = append(s, 4)

- If capacity allows, append reuses memory
- If capacity exceeded, new array is allocated
- Length changes when elements are removed
- Capacity remains until reallocation occurs

---

## Imports and Aliases

Example:

    import (
        "fmt"
        n2 "github.com/rajch/numbertowords"
    )

    func main() {
        result, _ := n2.Convert(1234)
        fmt.Println(result)
    }

---

## Go Proxy
- Default proxy:
  GOPROXY=https://proxy.golang.org,direct
- Modules are published to source control, not directly to proxies
- pkg.go.dev lists all publicly available Go modules and packages
