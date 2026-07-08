- Modern programming language developed by Google, designed for building fast and reliable applications, especially in cloud, DevOps, and distributed systems.
- Compiled & fast, statically typed, readable syntax, strong open-source ecosystem
- Identifiers/Variables
	-  ```go
	  package main //package
	  import "fmt" //package
	  const siteName = "GeeksforGeeks" //constant
	  type Student struct { //type
		  Name string
	  }
	  func display() { //function
		  fmt.Println(siteName)
	  }
	  func main() {
		  var age int = 20 //variable
		  height := 10 //short variable declaration
		  const PI = 3.14 //Constant can't be declared using :=
		  var str1 string = "string" //variable
		  display()
		  fmt.Println(age)
	  }
	  ```
	-  Rules for Naming
		- It must start with a letter (A-Z or a-z) or an underscore _.
		- It can contain letters, digits (0-9) and underscores.
		- It cannot start with a digit.
		- Identifiers are case-sensitive.
		- Go keywords cannot be used as identifiers.
			- break, case, chan, const, continue, default, defer, else, fallthrough, for, func, go, goto, if, import, interface, map, package, range, return, select, struct, switch, type, var
		- Valid: name, _name, user123, total_marks, Geeks
		- Invalid: 123name, if, for, switch
	- Exported identifiers begin with an uppercase letter and can be accessed from other packages. Non-exported identifiers start with a lowercase letter and can only be accessed within the same package.
- Data Types
	- Basic type: 
		- numbers
			- both signed(int) and unsigned integers(uint) in four different sizes.
			- floating-point - float32 and float64
			- complex - complex64 and complex128
				- complex(6,2) = (6+2i), real(), imag()
		- strings
			- Immutable bytes and can be concatenated using +
		- booleans
			- true or false
	- Aggregate type: array and structs
	- Reference type: pointers, slices, maps, functions, channels
	- Interface type
- Variable Declaration
	- var variable_name type = expression
	- type and expression can not both be omitted
		- If there is no type, it is assumed by the expression.
		- If there is no expression, it is 0, false, "", or nil.
	- Multiple var of same type -> var a, b, c int = 2, 3, 4
	- Multiple var of diff type -> var a, b, c = 2, "hi", 4.5
	- Multiple var with := has same syntax
	- Multiple return values from a function
		- ```go
		  package main
		  import "fmt"
		  func getNumbers() (int, int) {
			  return 5, 10
		  }
		  func main() {
		      a, b := getNumbers()
		  }
		  ```
	- 