#VARIADIC FUNCTION

`accepts variable number of parameters` and `use three dots in front of an input type` makes it variadic;

              variadic
func foo(names ...string)
         will passed as a slice

#A SIMPLE VARIADIC FUNCTIOIN
func foo(names ...string) returnvalue {
    // do something;
}

`can pass zero or more parameters;`
foo("param1", "param2")
foo("param")
foo()

#WHEN USE VF?
1. skip create a temporary slice to pass to function;
2. numnber of params are unknow;
3. increase readablity;

#EXAMPLE




