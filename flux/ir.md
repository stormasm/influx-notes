In this document: https://github.com/influxdata/flux/blob/master/docs/CompilationExecution.md is the IR or Intermediate Representation the AST Abstract Syntax Tree or ASTPackage https://github.com/influxdata/flux/blob/master/ast/ast.go ? (edited)

docs/CompilationExecution.md
<https://github.com/influxdata/flux|influxdata/flux>influxdata/flux | Added by GitHub


##### So here is where I am getting confused:
https://github.com/influxdata/flux/blob/master/examples/library/library_example_test.go

examples/library/library_example_test.go
package library_test

import (
    "bytes"
    "context"
Show more
<https://github.com/influxdata/flux|influxdata/flux>influxdata/flux | Added by GitHub

```
astPkg := parser.ParseSource(t)
the parser creates the AST
program, err := compiler.Compile(ctx)
the compiler creates the program and takes as input the AST
```
Is the astPkg the IR or is the program the IR ??
What is the difference between the askPkg and the Program ?

https://github.com/influxdata/flux/blob/master/lang/compiler_test.go#L320
program, err := lang.Compile(src, now, opt)
https://github.com/influxdata/flux/blob/master/compiler.go#L14
// Compile produces a specification for the query.
	Compile(ctx context.Context) (Program, error)
So in this case the Program which is returned from Compile is the IR ?

compiler.go:14
https://github.com/influxdata/flux|influxdata/flux>influxdata/flux
The specification for the Query is the IR ?
