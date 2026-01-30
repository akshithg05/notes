
For errors use errors.New("category not found") or fmt.Errorf()
Errorf allows formatting, errors.New will not allow the same.

%v - format for anything 
fmt.Errorf("category id %v does not exist", id)

```go
// package categoryRepository

  

// import (

//  "fmt"

//  "time"

  

//  "github.com/akshithg05/expensetracker/internal/model"

// )

  

// var categories = map[int64]model.Category{

//  0: {Id:0, Name: "Uncategorized"},

//  1: {Id:1, Name: "Food"},

//  2: {Id:2, Name: "Travel"},

// }

  

// // Below is example of slice of expense

// // Slice is like an array.

// var expenselist = make([]model.Expense,5,10)

  
  

// // NewCategory adds another category and returns it.

// func NewCategory(name string) (model.Category, error){

//  newId := len(categories) + 1

//  NewCategory := model.Category{

//      Id: int64(newId),

//      Name: name,

//  }

//  categories[int64(newId)] = NewCategory // creates a 2nd copy of Newcategoty

//  return NewCategory, nil //creates a 3rd copy while returning Newcategoty

// }

  

// //GetCategory gets a specific category by iD

// func GetCategory(id int64)(model.Category, error){

//  category , ok := categories[id]

//  if !ok{

//      return model.Category{}, fmt.Errorf("category id %v does not exist", id)

//  }

//  return category, nil //creates a copy while returning category

// }

  
  

// // GetAllCategories returns a map of all categories

// func GetAllCategories()(map[int64]model.Category, error){

//  return categories, nil

// }
```

Ideally try and control capacity of an array , and not size 
Once capacity is allocated it stays allocated.

We are careful while using pointers as pointers can be used to change values directly. Instead we sent copies directly.


```go
func GetAllCategories()([]model.Category, error){
    results:= make([]model.Category, 0 ,len(categories))
    // results:= make([]model.Category ,len(categories)) - 
    //results:= []model.Category{} - Do not use this as good practice, good to keep fixed capacity to avoid creating copies when size increases beyond capacity.
    // In general avoid unnecessary allocations
    for _, value := range categories{
        results = append(results, *value)
    }
    return results, nil
}
```


Experimental packages are stored in  - golang.org/x/exp.
example - maps was part of this until go 1.22, maps is part of standard library since go 1.23.

maps values retunrs values of a map
results := maps.Values(categories)


if the package name and testing package name is same then we can also access the private variables of a package. Hence naming of the testing package is important to set.

go test takes package name , does not take directory name.

go test . - means current package.

go test -v -  verbose will show logs or errors

go test ./... - all packages in module.

go test .\internal\categoryRepository\ -v -coverprofile categoryRepository.cover -  For coverage report and % coverage

go tool cover -html categoryRepository.cover - to run the coveragr report and convert it into an html file

go tool cover -html categoryRepository.cover -o coverage.html - create a html file as well for the coverage report.


## Methods // Reciever functions 

Are a way in go of giving the illusion of Object oreinted prog
it is a function associated with a type.
Any var of that type can call a method by saying variable.methodName.

It is like any other function parameters and return values.

Method can access the members of the type . If the type is a struct, it can access any field.
Method can access pub and prov fields of the type.

Encapsultaion can be achieved by creating a struct with private fields but public methods.

regular functions are chieved directly package.function.
methods cannot be accessed without creating the object.


0 value of slice is nil.


a pointer to a type or type can call the reciever method, both are allowed.
This happens automatically.

If reciever function take a type , and not a pointer it can be called only on the type not pointer to that type.

func (er ExpenseRepository) NewExpense(date time.Time,

This can be only called on the ExpenseRepository.

```go
func (er *ExpenseRepository) NewExpense(date time.Time,
```

This can be only called on the ExpenseRepository type as well as point er to ExpenseRepository type.

every type has a default string representation.


arrays show as [elements] ,
even slices as [elemenst comma seperated]

structs - {0 Expense 1 125.51 2026-01-29 12:07:06.4565714 +0530 IST m=+0.002743801}


### Polymorphism in Go

Interface is not a type in go , its a pointer to something , generally mothds

```go
type ExpenseRepository interface {
    NewExpense(date time.Time, description string, amount float32) (Expense, error)
    GetExpense(id int64) (Expense error)
    GetAllExpenses() ([]Expense, error)
    UpdateExpense(item Expense) (Expense, error)
    DeleteExpense() error
}
```

ExpenseRepository defining a behaviour that a type has all these methods , only these or these 5 and more methods. It can have other, but it should have all these methods with same names.

Same method names, parameter datatypes and return types and order needs to be same to be compatible.
Parameters name does not matter

we can leave the names of the parameters.

Who can implement this interface ?
In go we create interface and methods. If the interface has same methods  , parameters and return types, then that is compatible with  this interface.

Interface is a pointer with extra checks. It points to an object, we dont know which object it points to. Whatever object it points to will have the methods we defined, else code will no compile itself.

Interfaces are a big part of idiomatic golang implemntation


## Function type

again a pointer type which maches functions by paramter types and return types.

Allows us to design functions where we can pass other functions and accept functions as parameters. first class functions , similar to JS, callback functions.

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")

	var f1 func(int) string
	f1 = someFunction1

	fmt.Println(f1(5))
}

func someFunction1(num int) string {
	return fmt.Sprintf("Number was: %v", num)
}

func someFunction2(num int) int {
	return num * 2
}

```


## Defer in go

Defer key word in go is used to defer execution of a function.

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
	function1()
}

func function1() {
	defer function2()
	fmt.Println("function1")
}

func function2() {
	fmt.Println("function2")
}

func function3() {
	fmt.Println("function3")
}

```

Here the output will be first function1 then function2 because we are defering function2 to be executed after function1 execution. then function2 will get executed

Also defers are stacked, so in the below coding example case output will be -
function1
function3
function2

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
	function1()
}

func function1() {
	defer function2()
	defer function3()
	fmt.Println("function1")
}

func function2() {
	fmt.Println("function2")
}

func function3() {
	fmt.Println("function3")
}

```

The uses of defers are -
to close connections, open connections, db transactions, etc.

## Panic in go

It is much worst than error, it means code does not know what to do. It is catastrophic. Application crash.

Only place panic will not stop is in deferred function

recover can only be called in deferred function.

```go
// You can edit this code!
// Click here and start typing.
package main

import "fmt"

func main() {
	fmt.Println("Hello, 世界")
	function1()
}

func function1() {
	defer function2()

	fmt.Println("function1")
}

func function2() {
	defer function4()
	function3()
	fmt.Println("function2")
}

func function3() {
	panic("life has ended")
	fmt.Println("function3")
}

func function4() {
	recover()
	fmt.Println("function4")
}
```

### Web applications in Go

A go web application in itself a web server. your application is the server.

we have to use the package net/http

```
package main

  

import (

    "fmt"

    "net/http"

)

  

func main() {

    defer shutdown()

    if err := http.ListenAndServe("0.0.0.0:8080", nil); err != nil {

        fmt.Printf("Could not start server. Error: %v", err)

        return

    }

  

    fmt.Printf("Server stopped")

}

  

func shutdown() {

    fmt.Printf("Shutting down server")

}
```

Above is old way of doing things, below is better way of doing things 

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    server := &http.Server{
        Addr:    "0.0.0.0:8080",
        Handler: nil,
    }

    err := server.ListenAndServe()


    if err != nil {
        fmt.Printf("Could not start server. Error: %v", err)
        return
    }
    fmt.Printf("Server stopped")
}
```



anything ending with "er" is generally an interface in golang
if an interface name ends in writer, also implements an interface called writer.

A lambda becomes a closure, when it uses a variable declared in teh defining/enclosing function and the enclosing function finishes before the lambda function finishes.
Similar to JS closures.



