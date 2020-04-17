In this document:

https://github.com/influxdata/flux/blob/master/docs/CompilationExecution.md

is the IR or Intermediate Representation the AST Abstract Syntax Tree or ASTPackage

https://github.com/influxdata/flux/blob/master/ast/ast.go ?

## Case I

From here we see:

https://github.com/influxdata/flux/blob/master/compiler.go#L14

```
// Compiler produces a specification for the query.
type Compiler interface {
	// Compile produces a specification for the query.
	Compile(ctx context.Context) (Program, error)
	CompilerType() CompilerType
}
```

So in this case the Program which is returned from Compile is the IR ?


## Case II

https://github.com/influxdata/flux/blob/master/examples/library/library_example_test.go#L19

```

ctx, cancelFunc := context.WithCancel(context.Background())
	defer cancelFunc()

	astPkg := parser.ParseSource(t)
	if ast.Check(astPkg) > 0 {
		panic(ast.GetError(astPkg))
	}
	compiler := lang.ASTCompiler{
		AST: astPkg,
	}

	program, err := compiler.Compile(ctx)
	if err != nil {
		panic(err)
	}

	ctx = executetest.NewTestExecuteDependencies().Inject(ctx)
	alloc := &memory.Allocator{}
	q, err := program.Start(ctx, alloc)
	if err != nil {
		panic(err)
	}

```

Is the astPkg the IR or is the program the IR ??

What is the difference between the astPkg and the Program ?

## Case III

https://github.com/influxdata/flux/blob/master/lang/compiler_test.go#L320

```
  program, err := lang.Compile(src, now, opt)
	if err != nil {
		t.Fatalf("failed to compile script: %v", err)
	}

	// start program in order to evaluate planner options
	ctx := executetest.NewTestExecuteDependencies().Inject(context.Background())
	if _, err := program.Start(ctx, &memory.Allocator{}); err != nil {
		t.Fatalf("failed to start program: %v", err)
	}
```
